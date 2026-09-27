# Mandi — PRD summary

The full, living PRD is a shared document: **Mandi — Product Requirements Document** (https://claude.ai/code/artifact/b6940333-ce97-4d41-9e3e-f331fd1cd919). This file is the frozen summary that tasks reference; if the two disagree, the living PRD wins and this file must be updated.

## Product in one line

Keep each household's usual items, price the basket across Zepto, Swiggy Instamart, Blinkit, BB Now and FirstClub with every fee included, and get it into the cheapest set of carts in the fewest taps each store allows.

## Launch

Bengaluru and Hyderabad (the two cities where all five stores, including FirstClub, operate). Closed pilot of 300 households, then public beta.

## Features (IDs are used by tasks)

| ID | Feature | MVP priority |
| --- | --- | --- |
| F1 | Onboarding: phone OTP, location, store serviceability, link Zepto, import usuals, health goals | P0 |
| F2 | Usuals list: cadence, due dates, per-item store and brand rules, pause | P0 (pause P1) |
| F3 | Search and compare across stores, product page with health grade and store prices | P0 |
| F4 | Basket planner: cheapest / fewest taps / single store, all fees included | P0 |
| F5 | Checkout: tier A direct order (Zepto), tier C guided hand-off; tier B cart fill | P0 (tier B P1) |
| F6 | Order confirmation and tracking; substitutions | P0 |
| F7 | Health grades, basket grade, insights | P0 grades, P1 insights |
| F8 | Profile: addresses, payment method display, linked stores, preferences, data export and deletion | P0 |
| F9 | Notifications: basket due, price drops, order status | P0 due, P1 others |
| F10 | Platform: auth, observability, flags, analytics, CI/CD, infra | P0 |

## MVP success metrics

Week-4 retention 35%; 1.2 baskets planned per active user per week; 60% hand-off completion; median saving ₹20 or 5% per basket after fees; ≤ 4 taps from open to all carts ready for a two-store basket.
