# LLD — Data model

PostgreSQL 16 with extensions `postgis`, `pg_trgm`, `pgvector`, `pg_partman`, `pgcrypto`. Schema managed by Drizzle migrations in `services/api/src/db/migrations`. All tables have `created_at timestamptz default now()` and `updated_at` (trigger), omitted below. IDs are UUIDv7 (time-ordered) unless noted. Money is stored in paise as `integer`.

## Identity and users

| Table | Key columns | Notes |
| --- | --- | --- |
| `users` | `id`, `phone_e164` unique, `display_name`, `status` (`active`,`deleted`), `locale` | Phone is the only login identifier |
| `otp_challenges` | `id`, `phone_e164`, `code_hash`, `attempts`, `expires_at` | TTL 5 min; max 5 attempts; also rate-limited in Valkey |
| `sessions` | `id`, `user_id`, `refresh_hash`, `device_id`, `platform`, `expires_at`, `revoked_at` | Refresh tokens rotate on every use |
| `devices` | `id`, `user_id`, `platform` (`ios`,`android`), `push_token`, `app_version` | One row per install |
| `consents` | `user_id`, `purpose` (`order_history_import`,`email_orders`,`analytics`,`marketing`), `granted_at`, `withdrawn_at`, `notice_version` | DPDP consent ledger; append-only |

## Places and stores

| Table | Key columns | Notes |
| --- | --- | --- |
| `addresses` | `id`, `user_id`, `label` (`home`,`work`,`other`), `line1`, `line2`, `city`, `pincode`, `location geography(Point)`, `is_default` | |
| `stores` | `id` text (`zepto`,`instamart`,`blinkit`,`bbnow`,`firstclub`), `name`, `app_scheme`, `web_base_url` | Static reference data |
| `store_capabilities` | `store_id`, `tier` (`A`,`B`,`C`), `can_search`, `can_order`, `can_track`, `enabled`, `updated_by` | Runtime switch per store (ADR-0007) |
| `store_serviceability` | `store_id`, `pincode`, `serviceable`, `typical_eta_min`, `checked_at` | Refreshed daily |
| `store_links` | `id`, `user_id`, `store_id`, `status` (`active`,`expired`,`revoked`), `token_ciphertext bytea`, `data_key_ciphertext bytea`, `scopes`, `expires_at`, `last_sync_at` | Tokens envelope-encrypted with KMS (see security-privacy.md) |
| `memberships` | `user_id`, `store_id`, `kind` (e.g. `zepto_pass`), `valid_until` | Affects fee rules |
| `fee_rules` | `id`, `store_id`, `city`, `kind` (`delivery`,`handling`,`small_cart`,`surge`,`platform`), `min_subtotal`, `max_subtotal`, `amount_paise`, `waived_by_membership`, `valid_from`, `valid_to`, `source` | Versioned; plans reference the rule ids they used |

## Catalogue and prices

| Table | Key columns | Notes |
| --- | --- | --- |
| `products` | `id`, `brand`, `name`, `variant`, `pack_qty numeric`, `pack_unit` (`g`,`ml`,`pc`), `category`, `barcode`, `name_tsv tsvector`, `embedding vector(384)` | Canonical product; one per brand+variant+pack |
| `store_products` | `id`, `store_id`, `store_sku`, `product_id` nullable, `title`, `pack_qty`, `pack_unit`, `image_url`, `deep_link`, `match_status` (`auto`,`review`,`confirmed`,`rejected`), `match_score` | Store listing mapped to a canonical product |
| `offers` | `store_product_id`, `pincode_cluster`, `price_paise`, `mrp_paise`, `in_stock`, `observed_at`, `source` (`mcp`,`feed`,`partner`) | Partitioned by day with pg_partman; 90-day retention; latest offer cached in Valkey |
| `nutrition_facts` | `product_id`, `per` (`100g`,`100ml`), `energy_kcal`, `protein_g`, `fat_g`, `sat_fat_g`, `sugar_g`, `added_sugar_g`, `fibre_g`, `sodium_mg`, `ultra_processed bool`, `allergens text[]`, `source` | |
| `health_grades` | `product_id`, `rules_version`, `grade` (`A`–`E`), `score`, `drivers jsonb` | Recomputed when rules or facts change |

## Usuals, baskets and orders

| Table | Key columns | Notes |
| --- | --- | --- |
| `usuals` | `id`, `user_id`, `product_id`, `quantity`, `cadence_days`, `next_due_on date`, `store_rule` (`cheapest`,`fixed`), `fixed_store_id`, `brand_rule` (`exact`,`same_grade`), `auto_add`, `paused_until`, `source` (`import`,`manual`,`search`) | Unique (`user_id`,`product_id`) |
| `usual_events` | `usual_id`, `kind` (`bought`,`skipped`,`edited`), `at`, `order_id` | Feeds cadence inference |
| `baskets` | `id`, `user_id`, `address_id`, `status` (`draft`,`planned`,`checking_out`,`done`,`abandoned`) | One active basket per user |
| `basket_items` | `basket_id`, `product_id`, `quantity`, `usual_id` nullable, `included bool` | |
| `plans` | `id`, `basket_id`, `kind` (`cheapest`,`fewest_taps`,`single_store`), `total_paise`, `saving_paise`, `taps`, `input_hash`, `fee_rule_ids uuid[]`, `computed_at`, `expires_at` | Expires after 10 minutes |
| `plan_legs` | `plan_id`, `store_id`, `tier`, `subtotal_paise`, `fees_paise`, `eta_min` | One per store in a plan |
| `plan_lines` | `plan_leg_id`, `product_id`, `store_product_id`, `quantity`, `unit_price_paise` | |
| `orders` | `id`, `user_id`, `plan_id`, `store_id`, `tier`, `store_order_ref`, `status` (`pending`,`placed`,`confirmed_by_user`,`out_for_delivery`,`delivered`,`cancelled`,`failed`), `amount_paise`, `placed_at`, `delivered_at` | One row per store leg |
| `order_items` | `order_id`, `product_id`, `quantity`, `unit_price_paise`, `substituted_by_product_id` | |
| `outbox` | `id bigserial`, `topic`, `payload jsonb`, `created_at`, `relayed_at` | Transactional outbox; relayed by workers |
| `idempotency_keys` | `key`, `user_id`, `route`, `response_hash`, `response jsonb`, `expires_at` | 24-hour TTL |

## Health, notifications, audit

| Table | Key columns | Notes |
| --- | --- | --- |
| `health_profiles` | `user_id`, `goals text[]`, `diet`, `avoid text[]` | |
| `notifications` | `id`, `user_id`, `kind` (`basket_due`,`price_drop`,`order_status`), `payload jsonb`, `sent_at`, `opened_at` | |
| `audit_log` | `id bigserial`, `actor_user_id`, `action`, `entity`, `entity_id`, `at`, `meta jsonb` | Append-only; store links, orders, consent and deletion events |

## Indexes that matter

- `products (name_tsv) GIN`, `products (name gin_trgm_ops)`, `products (embedding) HNSW` for search.
- `offers (store_product_id, pincode_cluster, observed_at desc)` inside each partition.
- `usuals (user_id, next_due_on)` for the due scheduler.
- `addresses (location) GIST` for serviceability lookups.

## Deletion

Account deletion (PRD F8) hard-deletes `users`, `sessions`, `devices`, `addresses`, `store_links`, `usuals`, `health_profiles` and anonymises `orders` (user id replaced) within 30 days, keeping the `audit_log` entry of the deletion itself.
