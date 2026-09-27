# LLD — Health grades

Package `packages/health` (`@mandi/health`), pure TypeScript. Grades are guidance, not medical advice; every screen that shows a grade links to how it was computed.

## Product grade

Inputs per 100 g/ml from `nutrition_facts`. Points (rules version `2026.1`, tunable in the database):

| Driver | Worse (adds points) | Better (removes points) |
| --- | --- | --- |
| Energy | 0–10 pts over 335 kJ steps | — |
| Sugar (added if known, else total) | 0–10 pts over 4.5 g steps | — |
| Saturated fat | 0–10 pts over 1 g steps | — |
| Sodium | 0–10 pts over 90 mg steps | — |
| Ultra-processed flag | +3 | — |
| Fibre | — | 0–5 pts over 0.9 g steps |
| Protein | — | 0–5 pts over 1.6 g steps |
| Fruit/veg/legume share | — | 0–5 pts |

Score → grade: ≤ 0 A, 1–5 B, 6–11 C, 12–17 D, ≥ 18 E. Categories with their own logic: plain milk, curd and eggs are capped at B minimum; water and unsweetened tea/coffee are A; oils use a fat-quality table.

User goals shift the displayed grade by at most one step and always show why (e.g. "More protein: +1").

## Basket grade

Quantity-weighted mean of product scores mapped to A–E, plus shares by grade for the Insights chart.

## Swaps

A swap candidate is the same category, grade at least one step better, price ≤ current price at the same store (or the plan's store), and not in the user's avoid-list. At most one swap card per basket.

## Data

Nutrition comes from package labels (feed data, partner data, or manual entry for the top 2,000 staples before launch). Every fact row keeps its `source`; a product without facts shows "No grade yet" instead of guessing.
