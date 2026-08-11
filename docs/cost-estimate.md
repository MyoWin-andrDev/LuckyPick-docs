#  Development Cost Estimate

Outsourcing cost analysis for building LuckyPick EuroMillions (iOS + Android) — based on the complete 11-document specification.

---

##  Executive Summary

| Outsourcing Tier | Hourly Rate | Estimated Total |
| :--- | :---: | :--- |
| **Budget** — South/SE Asia, India (junior–mid teams) | $25 – $40 / hr | **$41,000 – $57,000** |
| **Mid-Tier** — Eastern Europe, Latin America (experienced) | $50 – $70 / hr | **$77,000 – $107,000** |
| **Premium** — Western Europe, US/Canada (senior agencies) | $100 – $160 / hr | **$166,000 – $231,000** |

Estimated scope: **1,280 – 1,775 hours** total across all disciplines.
Estimated timeline: **5 – 6 months** with a full team of 4–5 people.

---

##  Work Breakdown by Component

### Mobile App — Flutter (iOS + Android)

| Component | Hours (Min) | Hours (Max) |
| :--- | ---: | ---: |
| Project setup, architecture, CI/CD | 20 | 30 |
| Design system & component library (Dark Blue/Gold) | 30 | 40 |
| Splash, onboarding, home screen | 25 | 35 |
| 5-tab navigation structure | 15 | 20 |
| Lucky Modes browser screen + free/premium gating | 25 | 35 |
| **Generation Engine — 10 Lucky Modes + Quick Pick** | **155** | **211** |
| — Quick Pick (random) | 8 | 12 |
| — Birthday Mode (date → numerical profile) | 15 | 20 |
| — Horoscope Mode (zodiac sign mapping) | 12 | 18 |
| — Pet Mode (name + animal type hashing) | 12 | 18 |
| — Family Mode (multi-member aggregate) | 18 | 25 |
| — Lucky Color Mode (10 colors with profiles) | 10 | 15 |
| — Lucky Number Mode (mandatory inclusion) | 15 | 20 |
| — Hot Numbers Mode | 12 | 18 |
| — Cold Numbers Mode | 10 | 15 |
| — Trending Mode (20-draw vs 100-draw) | 15 | 20 |
| — Smart Mix Mode (sequential exclusion) | 18 | 25 |
| — Validation engine + duplicate protection | 20 | 30 |
| — Number reveal animation (1–1.5s) | 10 | 15 |
| **My Picks & Saved Sets** | **60** | **80** |
| — Add/remove/replace with mode snapshots | 25 | 35 |
| — SQLite / Hive persistence | 15 | 20 |
| — UI screens + archived sets | 20 | 25 |
| **Results & Draw History** | **40** | **50** |
| — Latest draw + 13 prize tiers | 20 | 25 |
| — 100-draw history browser | 20 | 25 |
| **Statistics Screens** | **35** | **47** |
| — Hot/Cold/Trending/Frequency display | 25 | 35 |
| — Free vs Premium access gating | 10 | 12 |
| **Notifications** | **50** | **65** |
| — Local scheduler (Mon/Thu 19:00 local) | 15 | 20 |
| — Remote push handler (FCM + APNs) | 20 | 25 |
| — Settings + deep link routing | 15 | 20 |
| **Premium & In-App Purchases** | **90** | **125** |
| — Premium discovery screen & UX | 15 | 20 |
| — StoreKit 2 integration (iOS) | 25 | 35 |
| — Google Play Billing integration (Android) | 25 | 35 |
| — Entitlement management + restore | 25 | 35 |
| **Social Sharing** | **45** | **65** |
| — Branded card generator (in-app canvas) | 20 | 30 |
| — Native share sheet (7 platforms) | 10 | 15 |
| — Firebase Dynamic Links / deep links | 15 | 20 |
| Settings / More screen | 25 | 35 |
| Free-tier daily limit UX | 15 | 20 |
| **Mobile Subtotal** | **625** | **858** |

### Design — UI/UX + Visual Assets

| Component | Hours (Min) | Hours (Max) |
| :--- | ---: | ---: |
| UX wireframes + user flows | 20 | 30 |
| High-fidelity screen designs (all screens) | 60 | 80 |
| Premium ball/star visual assets | 20 | 30 |
| App icon + store assets | 10 | 15 |
| Sharing card template | 10 | 15 |
| App Store + Google Play screenshots | 10 | 15 |
| **Design Subtotal** | **130** | **185** |

### Backend — Server, API & Scraper

| Component | Hours (Min) | Hours (Max) |
| :--- | ---: | ---: |
| Server setup, PostgreSQL, Redis, CI/CD | 20 | 30 |
| REST API (draws, stats, users, subscriptions) | 60 | 80 |
| JWT authentication system | 15 | 20 |
| Scraper engine (Belgian National Lottery) | 30 | 45 |
| Draw validation logic (5+2 rules, duplicates) | 15 | 20 |
| 100-draw rolling management | 10 | 15 |
| Statistics calculator (Hot/Cold/Trending) | 20 | 30 |
| Push notification backend (FCM + APNs) | 30 | 40 |
| IAP receipt verification (Apple + Google) | 25 | 35 |
| Subscription lifecycle management | 15 | 20 |
| Admin control panel (owner web UI) | 50 | 70 |
| Error handling + monitoring | 15 | 20 |
| **Backend Subtotal** | **305** | **425** |

### Landing Page (luckypick.eu)

| Component | Hours (Min) | Hours (Max) |
| :--- | ---: | ---: |
| Promotional landing page | 15 | 20 |
| Privacy Policy + Terms & Conditions pages | 8 | 12 |
| Smart deep link integration | 7 | 10 |
| **Landing Page Subtotal** | **30** | **42** |

### QA & Testing

| Component | Hours (Min) | Hours (Max) |
| :--- | ---: | ---: |
| Unit tests — generation algorithms (all 10 modes) | 25 | 35 |
| API integration tests | 15 | 20 |
| Manual testing — iOS devices | 25 | 35 |
| Manual testing — Android devices | 25 | 35 |
| IAP sandbox testing (all 3 plans + restore) | 15 | 20 |
| Live scraper automation (minimum 3 consecutive draws) | 15 | 20 |
| Privacy / sharing QA | 10 | 15 |
| Performance + edge case testing | 10 | 15 |
| **QA Subtotal** | **140** | **195** |

### Project Management & Handover

| Component | Hours (Min) | Hours (Max) |
| :--- | ---: | ---: |
| Sprint planning, communication, revisions | 40 | 60 |
| Technical handover + Owner Guide (9 items) | 15 | 20 |
| **PM & Handover Subtotal** | **55** | **80** |

---

##  Total Scope Summary

| Discipline | Min Hours | Max Hours | % of Project |
| :--- | ---: | ---: | ---: |
| Mobile App (Flutter) | 625 | 858 | ~48% |
| Backend + API + Scraper | 305 | 425 | ~23% |
| Design & Assets | 130 | 185 | ~10% |
| QA & Testing | 140 | 195 | ~11% |
| Project Management | 55 | 80 | ~5% |
| Landing Page | 30 | 42 | ~3% |
| **TOTAL** | **1,285** | **1,785** | 100% |

---

##  Timeline Estimate

Assumes a full team: 2 Flutter developers, 1 backend developer, 1 designer, 1 QA (part-time).

| Phase | Duration | Key Deliverables |
| :--- | :---: | :--- |
| 1. Design & Architecture | Weeks 1–3 | All screen designs, system architecture, DB schema |
| 2. Foundation + Core Screens | Weeks 3–6 | Navigation, home, mode browser, quick pick |
| 3. Generation Engine (10 Modes) | Weeks 6–12 | All Lucky Modes with full validation |
| 4. My Picks + Results + Stats | Weeks 10–15 | Saved sets, draw history, statistics screens |
| 5. Backend + Scraper + Admin | Weeks 4–16 | REST API, scraper, admin panel, push backend |
| 6. Premium + IAP + Notifications | Weeks 14–18 | StoreKit 2, Play Billing, push system |
| 7. Social Sharing + Deep Links | Weeks 17–19 | Share card, 7 platforms, dynamic links |
| 8. QA + Automation Testing | Weeks 18–22 | Full test pass including 3 live draws |
| 9. Store Submission + Handover | Weeks 22–24 | App Store, Google Play, owner guide |
| **Total** | **~24 weeks** | **Production-ready iOS + Android** |

---

##  Ongoing Costs (Post-Launch, Monthly)

| Service | Cost |
| :--- | :--- |
| Cloud server hosting (API + DB + Redis) | $50 – $150 / month |
| Firebase (push notifications) | Free tier at launch |
| Error monitoring (Sentry) | $0 – $26 / month |
| Apple Developer Account | $99 / year |
| Google Play Developer Account | $25 one-time |
| Domain (luckypick.eu) | ~€15 / year |
| Data source / commercial API (if required) | $0 – $200 / month |
| **Estimated monthly running cost** | **~$100 – $400 / month** |

---

##  Procurement Recommendations

!!! tip "Before Signing a Contract"
    1. **Get at least 3 competitive quotes** using this document as the specification brief.
    2. **Verify Flutter + IAP experience** — specifically StoreKit 2 (not StoreKit 1) and Google Play Billing v6+.
    3. **Ask for live scraper samples** — the automated draw ingestion is a critical, testable deliverable before final payment.
    4. **Clarify legal compliance** of scraping the Belgian National Lottery — ensure the chosen method is within permitted use.
    5. **Milestone-based payment** — tie payments to tested, approved deliverables (e.g., 20% on design approval, 30% on generation engine, 30% on full QA pass, 20% on live launch).
    6. **Consider a phased MVP approach** if budget is constrained: launch with Quick Pick + Results + Basic Stats first, then add all 10 Lucky Modes + Premium in version 1.1.

!!! warning "Risk Items"
    - The **Trending Mode** (20-draw vs 100-draw comparison) requires careful statistical implementation — test it explicitly.
    - **StoreKit 2 receipt verification** requires Apple's server-to-server API — budget extra time if the team is unfamiliar with this.
    - **Live automation testing** requires waiting for 3 real EuroMillions draws (≈ 1.5 weeks real time) — account for this in the QA timeline.
    - **Social sharing privacy** rules are strict — the QA checklist must specifically verify that no generated numbers or personal data appear in shared content.
