# Qunjee/QuFree — Development Timeline (`feat/appobook`)
> Full history of this branch: first commit to today. 135 commits, 2026-07-04 → 2026-08-03, ~1 month.
> Three contributors on this branch: **Silverado313** (101 commits — Aneel, CTO/main dev),
> **webify-cx** (32 commits), **Tech Peer** (2 commits). Grouped into phases below by what actually
> shipped, not by calendar week — some phases run a single day, some run several.

---

## Milestones at a glance

| Phase | Dates | Theme |
|---|---|---|
| [0](#phase-0--origin-appobookmedibook-2026-07-04--07-05) | Jul 4–5 | Origin: AppoBook/MediBook PWA foundation |
| [1](#phase-1--qufree-rebrand--core-booking-engine-2026-07-06--07-08) | Jul 6–8 | QuFree rebrand + transactional booking engine |
| [2](#phase-2--qunjeeeats--multi-brand-architecture-2026-07-09--07-12) | Jul 9–12 | QunjeeEats launch, multi-brand architecture |
| [3](#phase-3--booking-flow-rebuild--csr-module-2026-07-13--07-14) | Jul 13–14 | Booking flow rebuild, CSR/Support module |
| [4](#phase-4--self-pickup-afo-prepay--qunjee-rebrand-rollout-2026-07-15--07-17) | Jul 15–17 | Self-pickup/AFO prepay, Qunjee rebrand rollout |
| [5](#phase-5--vertical-expansion-hotels--restaurants-2026-07-19--07-20) | Jul 19–20 | Hotel & Padel verticals, FCM background push |
| [6](#phase-6--legal-compliance--sehatkamla-2026-07-21--07-24) | Jul 21–24 | Legal pages, SehatKamla module, admin growth infra |
| [7](#phase-7--ecosystem-hub--reliability-2026-07-26--07-30) | Jul 26–30 | Ecosystem hub expansion, kill-switch, Sentry, per-room-type hotels |
| [8](#phase-8--play-store-launch-prep-2026-07-31--08-03) | Jul 31–Aug 3 | Play Store policy + TWA packaging |

---

## Phase 0 — Origin: AppoBook/MediBook (2026-07-04 → 07-05)
*webify-cx*

- Transformed MediBook into AppoBook PWA (`qunjeebook`) — the seed this whole app grew from.
- Applied Qunjee blue theme (#1A56DB) across the app.
- Public/admin auth, homepage redesign, footer fix.
- Customer profile CRUD, booking cancel flow, mobile nav fix.
- FCM push notification client-side prep.

## Phase 1 — QuFree rebrand + core booking engine (2026-07-06 → 07-08)
*Silverado313*

- Rebranded MediBook/AppoBook → **QuFree**; dropped the GitHub link from the footer.
- Built the **transactional booking engine** — no double-booking, duration-aware, with per-slot
  capacity in the business model.
- Hardened Firestore rules — PII, role, ownership, capacity.
- Guarded admin Google sign-up; pointed deploy at qufree / `qunjee-com`.
- Visible PWA install banner + longer error toasts.
- Human-friendly Booking ID shown everywhere.
- QuFree-branded PWA icons/favicon, wordmark logo, warm cream theme, rounded app icons, social
  share (OG) image with "Powered by qunjee.com".
- 12-hour time display, day-part hover icons, grouped slot picker.
- Aligned theme/typography/nav layout with qunjee.com.
- Shipped **SuperAdmin console v1** with full Firestore CRUD.
- Docs: session log, SuperAdmin design & compliance plan, system usage workflow + architecture assets.

## Phase 2 — QunjeeEats + multi-brand architecture (2026-07-09 → 07-12)
*webify-cx, Silverado313*

- Redirected `/` and `/index` to qunjee.com in prod (moved to hosting-edge redirect after a client-side
  attempt), extended reminder timer to days.
- Excluded `/` and `/index` from the service worker's navigation fallback.
- Added `orderRef` util (`QE-` prefix) for Qunjee Eats orders.
- **Launched QunjeeEats** — ops-managed food ordering segment at `/qunjeeats`.
- Fixed internal navigation to never target `/index` directly.
- Gave QunjeeEats its own navbar identity instead of inheriting QuFree's logo; same for
  `EatsAdminLayout`'s sidebar.
- Renamed Dhaba → **FoodVend** across UI/code, added FoodVend edit.
- Real-time My Orders (was reload-only before).
- Docs: `BRANDING.md` (brand architecture), `NavigationRoutes.md`, `UAT.md`, allowlist-onboarding notes.
- Docs: SaaS evolution roadmap + Eats flow notes; package renamed to `qunjee-saas`; migration-safety
  section added to the roadmap.
- Repo cleanup: `docs/` structure, `.docx` → markdown, untracked `dev-dist`; README rewritten for
  Qunjee SaaS (replacing stale MediBook content).
- Dine-in pre-orders (F1) + owner-managed vendors (F2) + standalone PWA; Delivery/Dine-in choice at
  Eats checkout + "Book a Table" bridge.

## Phase 3 — Booking flow rebuild + CSR module (2026-07-13 → 07-14)
*Silverado313*

- Rebuilt booking flow (3-step, earlier sign-in) + advance-payment anti-spam for bookings and food
  orders.
- Needs-review dashboard, inline proof lightbox, booking-flow cleanup, business logo upload (1:1 crop).
- Menu-item photo CRUD + grid redesign with click-to-enlarge lightbox.
- Service photo CRUD (1:1 crop) across the booking flow; multi-service booking + click-to-zoom badges
  + per-service Book button.
- **CSR (Customer Support) module** + Support ID caller verification.
- Fixed booking slots to check real close-time instead of whole-slot-count (the rounding-waste bug).
- **Manual business subscription MVP** + invoicing + combined revenue reports.
- **Real-time support chat** via Realtime Database + CSR live queue.
- Password visibility toggle + forgot-password on all logins; read-only staff badges in Users.
- Docs: complete step-by-step user guide (every role), subscription + commission-settlement billing
  plans, Aroma Kitchen case study, SaaS readiness audit, master console-tasks reference, production
  data-cleanup plan, security & compliance audit.

## Phase 4 — Self-pickup, AFO prepay, Qunjee rebrand rollout (2026-07-15 → 07-17)
*Silverado313*

- Self-pickup, mandatory AFO prepayment, no-show policy.
- Fixed checkout crash on dine-in prepay, cart/chat overlap, live appointment status.
- Invoice printing/actions, configurable fee, CSR route rename.
- Stopped the service worker from caching Firebase's own API traffic.
- **Qunjee rebrand rollout** + ecosystem hub polish; fixed Lighthouse-flagged CLS/a11y/cache-header gaps.
- Added Q-Shua and Q-Tamerati cards to the ecosystem hub; footer credit now points at the hub.
- Page share menu, self-serve FAQ chat, SuperAdmin FAQ management + FAQ content drafts.

## Phase 5 — Vertical expansion: Hotels & Restaurants (2026-07-19 → 07-20)
*webify-cx, Silverado313*

- Rebranded meta to "Super Lifestyle Platform"; QunjeeEats navbar → image logo (softened corners).
- Renamed FoodVend → **Restaurant** in all user-facing text; per-restaurant Table Booking / Take Away
  switches.
- Added **Hotel and Padel Club** business types, dropped the "All" filter pill; pluralized browse
  filter labels, relabeled Clinic pill as Hospitals.
- Added Taa-ilm ecosystem card + email-domain typo-guard.
- **FCM background push** — status updates, welcome push, and broadcasts.
- **Hotel room-booking module** (date-range reservations, dashboard, screenshot proof).
- Manual push-notification guide added to docs.
- GA tag added; fixed room-booking capacity bug; expanded push-notification docs.
- Hardened booking-capacity rules, flagged price mismatches, added visitor counter.

## Phase 6 — Legal, compliance & SehatKamla (2026-07-21 → 07-24)
*Silverado313*

- **Terms of Service & Privacy Policy** pages; mobile **BottomNav** with docked support chat.
- Fixed Navbar/BottomNav visibility at bare root path `/`.
- Required signup phone; SuperAdmin login auto-redirect; Users-page date-range filter + charts.
- Fixed SuperAdmin role-badge color and a staff-label string mismatch.
- Google-login superAdmin redirect parity; home-page register menu; nav fixes.
- Routed customer-facing sign-out and legal-page back-links to `/index`.
- Labeled the type filter, dropped "appointment" wording, defaulted to Hotels.
- **SehatKamla** multi-vendor booking module added; unified customer/admin login pages; moved
  SehatKamla to 3rd position in the `/index` ecosystem grid.
- Allowed `sehatkamla` business type in Firestore rules; added bottom-nav + badge styling.
- Added "Latest Updates" scrolling ticker to the home page.
- Docs: DCE v2.0 cost evaluation covering post-v1 development.
- Hotel booking polish + SuperAdmin console improvements; CSV export for Users/Businesses tables;
  SehatKamla brand logo added to navbar/page header.
- Unified grid-card styling across home, browse, and QunjeeEats; added Date of Join to business admin
  profile; fixed mobile header stacking (button/name overlap).
- RTDB-backed online/offline presence dot for SuperAdmin; fixed it sticking "online" ~60s post-logout.

## Phase 7 — Ecosystem hub & reliability (2026-07-26 → 07-30)
*webify-cx, Silverado313*

- Added Dhaal ecosystem card; replaced Shopping card with **Qunjee Mall** on the ecosystem hub.
- Docs: PWA → Play Store/App Store roadmap (`PWA2TWA_ROADMAP.md`) — the decision point for TWA over
  native.
- iOS install step-by-step guide; added Dhaal + Qunjee Mall cards; merge-reconciled with upstream
  Dhaal/Qunjee Mall commits.
- Fixed Chrome/Firefox/Edge-on-iOS detection to point users at Safari for install; extracted
  `detectIOSBrowser()`.
- Temporarily hid the Qunjee Mall card; persistent "Install App" link on login pages, fixed a missed
  install-prompt bug; fixed the install banner reappearing every few seconds after dismiss.
- **Emergency shutdown kill-switch** (`config/appStatus`).
- Added Sentry error tracking (no-op until `VITE_SENTRY_DSN` is set).
- Fixed the live URL for QuFree in the README.
- PWA perf pass + business-card UX tweaks; business stat cards + live user count on the SuperAdmin
  Businesses page (then fixed a filtering/hook-order crash there).
- SuperAdmin push-campaigns UI, grouped sidebar, broader push reach.
- **Per-room-type hotel booking** (own price + own inventory pool per room type).
- Show/Hide Working Hours toggle for the public business page.
- Bell icon for RTDB-backed announcements (no push permission needed).

## Phase 8 — Play Store launch prep (2026-07-31 → 08-03)
*Silverado313, webify-cx, Tech Peer*

- Docs: Play Store policy protocols reference (reviewed against the actual codebase, not a generic
  checklist).
- Temporarily hid the Qunjee Kaam card from the ecosystem hub.
- Added **Nayasaa** (bridal & groom wear rental) card to the ecosystem hub.
- Added Digital Asset Links (`assetlinks.json`) for the Play Store TWA.
- Docs: TWA build/update pre & post instructions runbook (`TWA_PrePostInstructions.md`).
- Fixed the business-type filter resetting on browse navigation — back button/link now returns to the
  category actually being browsed instead of defaulting to Hotels.
- Docs: `BestPOV.md` — why TWA over native for this project, with a full head-to-head comparison.

---

## Reading this timeline

The shape of the last month: **rebrand three times** (MediBook→AppoBook→QuFree→Qunjee ecosystem),
**four verticals shipped** (booking/appointments, QunjeeEats food ordering, hotel rooms, SehatKamla),
one full support/CSR system, one SuperAdmin console with growing ops tooling, and — as of this week —
the first steps toward an actual Play Store listing via TWA. Two people carried most of the load
(Silverado313 and webify-cx working largely in parallel, occasionally on the same features — see the
2026-07-29 merge commit reconciling upstream Dhaal/Qunjee Mall work).
