# HomeCare+ — Tenant Operations Guide

A step-by-step walkthrough of every screen in your HomeCare+ admin dashboard. Use it when onboarding a new home-care tenant or training a new operator.

> HomeCare+ tenants deliver care **at the patient's home**. The dashboard helps you configure mobile doctors, define service prices, monitor visits, run financials, and manage marketing — all from one place. Location-related fields (doctor service radius, patient address) are first-class citizens because every visit needs an address to dispatch to.

---

## Table of contents

1. [Signing in](#1-signing-in)
2. [Choosing your organization](#2-choosing-your-organization)
3. [Getting started wizard](#3-getting-started-wizard)
4. [Analytics dashboard](#4-analytics-dashboard)
5. [Doctors & Staff](#5-doctors--staff)
   - [Doctors](#51-doctors)
   - [Specialities](#52-specialities)
   - [Ratings](#53-ratings)
6. [Clinics & Centers](#6-clinics--centers)
   - [Clinics](#61-clinics)
   - [Medical Centers](#62-medical-centers)
7. [Patients & Encounters](#7-patients--encounters)
   - [Patients](#71-patients)
   - [Encounters (Visits)](#72-encounters-visits)
8. [Pricing & Ranks](#8-pricing--ranks)
   - [Rank Types](#81-rank-types)
   - [Rank Prices](#82-rank-prices)
9. [Integrations](#9-integrations)
   - [Apps](#91-apps)
   - [Messages](#92-messages)
10. [Financial](#10-financial)
    - [Invoices](#101-invoices)
    - [Insurance Claims](#102-insurance-claims)
    - [Payout Transactions](#103-payout-transactions)
    - [Provider Settings](#104-provider-settings)
11. [Marketing](#11-marketing)
    - [Coupons](#111-coupons)
    - [Banners](#112-banners)
12. [Administration](#12-administration)
    - [Users](#121-users)
13. [Account recovery (forgot / reset password)](#13-account-recovery)
14. [Things worth knowing](#14-things-worth-knowing)

---

## 1. Signing in

![HomeCare login](screenshots/homecare/01-login.png)

- Open the URL provided by Codelines (e.g. `https://<your-tenant>.homecare.codelines.sa/system/login`).
- Enter your **Email** and **Password** and click **Sign in**.
- Use the globe icon in the top right to switch between English and العربية. The whole dashboard is bilingual and switches RTL/LTR automatically.
- Forgot password? Click **Forgot Password?** under the form. See section 13 for the recovery flow.
- After a successful password reset, you'll see a green confirmation banner the next time you reach this screen.

---

## 2. Choosing your organization

![Select organization](screenshots/homecare/02-select-organization.png)

If your account spans multiple tenants (e.g. one corporate operator running several home-care brands), you'll land here right after sign-in.

- Each card shows the **tenant name**, **App ID**, your **role** (`root_admin`, `super_admin`, `medical_center_admin`), and any medical centers you're scoped to.
- Filter the list with the search bar (matches name or App ID).
- Click **Select** to enter that tenant's dashboard.
- **Back to login** clears your session and returns to the sign-in page.

The tenant you pick is remembered for the rest of the browser session and can be switched any time from the header dropdown in the top-right.

---

## 3. Getting started wizard

![Getting started wizard](screenshots/homecare/03-getting-started.png)

Every new HomeCare+ tenant has to complete eight setup steps before patients can book visits. The wizard walks you through them in order and shows progress on a stepper at the top.

| Order | Step | What you provide |
|-----:|------|------------------|
| 1 | Medical center | EN/AR name, MOH license, contact details, address, status |
| 2 | Clinic type | E.g. "Home Care", "Wound Care" — the kind of service unit |
| 3 | Speciality | Specialities your nurses / doctors cover |
| 4 | Rank type | Provider levels: Consultant, Specialist, Nurse, etc. |
| 5 | Consultation type | "Home Visit", "Phone Follow-up", etc. |
| 6 | Clinic | Concrete service unit = clinic-type × medical-center |
| 7 | Doctor | A practitioner with name, gender, clinic, rank, speciality and **service location** |
| 8 | Rank price | Price per (rank × clinic × consultation type) |

- The **progress bar** shows how many of the eight steps are complete.
- **Save and Continue** advances to the next step. **Save and Add Another** is offered after a step is satisfied — useful when you have several doctors or rank prices to register.
- **Skip** defers a step (it can be completed later from its dedicated page).
- **View** opens the full list page for the resource so you can sanity-check what you've added.
- When all required steps are satisfied, a success card appears with a **Go to Dashboard** button (links to Analytics).

> The page is always reachable from the left sidebar — use it to finish setup later or to audit what's still missing.

---

## 4. Analytics dashboard

![Analytics dashboard](screenshots/homecare/04-analytics.png)

Your operations homepage. It pulls real-time KPIs from `GET /api/management/analytics` and recent encounters.

Sections, top to bottom:

1. **Organisation Overview** — three clickable KPI cards: total **Patients**, **Doctors**, **Total Appointments**. Click any to jump to the matching list.
2. **All Appointments** — today vs. all-time, broken down into **Upcoming / Ongoing / Completed / Canceled**.
3. **Finance & Payments** — four cards (Total Billed, Collected, Pending, Canceled) plus a **Recent Payments** table. **View All Transactions** jumps to *Payout Transactions*.
4. **Appointment Insights**
   - **Appointment Status** — rose chart of status distribution.
   - **Appointment Breakdown** — column chart.
5. **Appointments by Doctor** — bar chart of the top providers, with a **Today / This Week / This Month / Year to Date** segmented control that refetches `analytics?period=...`.
6. **Top Performers** — two leaderboards (Top Doctors, Top Patients) with medal badges. Clicking a row navigates to that record.

For HomeCare+ tenants the Top Doctors leaderboard usually reflects who's been **completing the most home visits**, not just consultations — useful for scheduling, bonuses, or vacation planning.

---

## 5. Doctors & Staff

### 5.1 Doctors

![Doctors list](screenshots/homecare/10-doctors-list.png)

The full roster of providers who deliver home visits. Columns: ID, bilingual name, email, gender, clinic type, rank, status, NPHIES practice code (⚠️ icon if missing — NPHIES claims won't work without it).

- Filter by **gender** and **status** with the column dropdowns.
- Row actions:
  - **Show** profile
  - **Edit**
  - **Delete** (with confirmation)
  - **📅 Manage Availability** — opens the scheduling iframe to set this doctor's working hours / shift template.
  - **🌴 Manage Vacations** — block off days when this doctor isn't available.

#### Creating a doctor

![Doctors create](screenshots/homecare/11-doctors-create.png)

Fields:

- **Names** (EN + AR), **Email**, **Contact info**, **Gender**.
- **Clinic**, **Rank**, **Speciality** — pick from the lookups you set up earlier.
- **NPHIES practice code** — required if you submit insurance claims.
- **Subspecialties**, **Description** (EN + AR), **Avatar**, **Status**.
- **Location** — for HomeCare+ this section is normally **enabled** by the tenant's booking config (`requiresLocation = true`). Set:
  - **Latitude / longitude** (use the embedded map picker)
  - **Address** (autofilled from the map)
  - **Radius (km)** — the maximum distance this doctor will travel from the pinned location. The booking app uses this to match doctors to incoming visit requests.

> Getting the location right is the single most important step for home care. Patients only see doctors whose service radius covers their address. A wrong pin or an unrealistic radius means missed bookings.

### 5.2 Specialities

![Specialities list](screenshots/homecare/12-specialities-list.png)

Lookup table of medical specialities used to tag doctors and filter the patient app.

![Speciality create](screenshots/homecare/13-specialities-create.png)

- Fields: **Name (EN)**, **Name (AR)**.
- Add one row per service you offer (wound care, geriatric care, post-op visit, IV therapy, etc.).

### 5.3 Ratings

![Ratings list](screenshots/homecare/14-ratings-list.png)

Patient feedback collected after each completed visit. Columns: encounter ID, star rating (rendered 0–5 from a 1–10 score), review text, created date.

- Filter the list by encounter ID or score.
- Ratings are read-only in the dashboard — moderation lives in the back-end.

For HomeCare+, this is your primary signal on **field experience** (punctuality, hygiene, bedside manner). Watch for trends, not single reviews.

---

## 6. Clinics & Centers

### 6.1 Clinics

![Clinics list](screenshots/homecare/20-clinics-list.png)

A clinic is one operating unit inside a medical center (e.g. "Home Care – Riyadh North"). Columns: clinic type, medical center, contact number, status, doctor count, NPHIES specialty code.

![Clinic create](screenshots/homecare/21-clinics-create.png)

- **Clinic type** — from your seeded list.
- **Medical center** — the parent facility.
- **NPHIES clinic specialty code** — required for insurance claims.
- **Contact number** — usually the dispatch line.

Row actions: Show / Edit / Delete.

### 6.2 Medical Centers

![Medical centers list](screenshots/homecare/22-medical-centers-list.png)

Top-level facilities — usually one per city / branch.

- Columns: bilingual name, address, contact, MOH license, status.
- Edit a center to update EN/AR name, address, MOH license, official phone/email, website URL, logo URL, digital stamp URL, latitude / longitude, and status.

> The medical center carries the **MOH license** that anchors your tenant to regulatory and NPHIES integrations, plus the **digital stamp** that appears on patient-facing PDFs (prescriptions, lab orders, invoices). Keep both current.

---

## 7. Patients & Encounters

### 7.1 Patients

![Patients list](screenshots/homecare/30-patients-list.png)

Everyone who has registered or been registered for a home visit.

- Columns: ID, English name, email, phone, national ID.
- Filter by email or phone via the column headers; use the top **search** for free-text match.
- **Show** opens the profile; **Edit** lets you correct the name, email, phone, national ID, or add a free-form note (e.g. "patient prefers female nurse").

> Patient records are created from the booking app, not the dashboard. Keep the patient list edits limited to corrections.

### 7.2 Encounters (Visits)

![Encounters list](screenshots/homecare/31-encounters-list.png)

Every booked, completed, or canceled home visit.

- Columns: ID, patient name, doctor name, clinical notes count, start time, "is canceled" flag.
- Filters: patient, doctor, status (Confirmed / Canceled), plus free-text top **search**.
- **+ Add Appointment** opens a modal that lets you pick an available doctor and book on their calendar via an embedded scheduling iframe. On save the list refreshes automatically.
- The **Show** view of an encounter has its own action bar:
  - **Booking Details** — shows the underlying booking record (patient address, slot, total).
  - **Reschedule** — opens the scheduling iframe pre-loaded with this encounter.
  - **Cancel Booking** — prompts for a reason then cancels.
  - Tabs for **Prescriptions** and **Lab Investigations** authored during this visit.

> Each booking carries the **patient address** captured in the booking app. The doctor app uses this address to navigate to the patient's home. Always verify the address with the patient if you reschedule from this dashboard.

---

## 8. Pricing & Ranks

### 8.1 Rank Types

![Rank types list](screenshots/homecare/40-rank-types-list.png)

Provider seniority tiers that price differently (Consultant / Specialist / Nurse / Physiotherapist…).

![Rank type create](screenshots/homecare/41-rank-types-create.png)

- Fields: **Name (EN)**, **Name (AR)**.

### 8.2 Rank Prices

![Rank prices list](screenshots/homecare/42-rank-prices-list.png)

The pricing matrix: one entry per (rank × clinic × consultation type).

![Rank price create](screenshots/homecare/43-rank-prices-create.png)

- **Rank**, **Clinic**, **Consultation type** from the seeded lookups.
- **Price** in your tenant's currency.
- **Duration (minutes)** — typical length of the visit; used to size the booking slot.
- **Description** — visible on the patient app's pricing screen.

> If the tenant runs on `leastFirst` booking policy, the **Rank** field is hidden — the system always picks the cheapest applicable rank for the patient. For home care that's common when several nurses can do the same wound-care visit at different price points.

---

## 9. Integrations

These pages embed the scheduling-platform UI that powers the patient/doctor apps. Each fetches a tenant-specific config from `/api/management/organization/scheduling-iframe?action=<feature>` and renders an iframe.

### 9.1 Apps

![Apps page](screenshots/homecare/50-apps.png)

Manage the **add-ons** enabled for this tenant (notification providers, custom integrations, optional flows).

### 9.2 Messages

![Messages page](screenshots/homecare/51-messages.png)

Configure SMS / email / WhatsApp templates and channels via the scheduling messages module. For HomeCare+, the templates here typically drive **arrival notifications** ("Your nurse is 10 minutes away") and **reminders**.

---

## 10. Financial

### 10.1 Invoices

![Invoices page](screenshots/homecare/60-invoices.png)

Embedded invoice management. Issue invoices for visits, track paid/unpaid status, attach to encounters.

### 10.2 Insurance Claims

![Insurance claims](screenshots/homecare/61-insurance-claims.png)

Embedded NPHIES claims workflow: eligibility checks, pre-authorizations, and reimbursement claims for insured patients.

> Claims will only succeed if the doctor's **NPHIES practice code** and the clinic's **NPHIES specialty code** are filled in. The doctors and clinics pages show a ⚠️ icon next to any record that's missing one.

### 10.3 Payout Transactions

![Payout transactions](screenshots/homecare/62-payout-transactions.png)

Batch payouts to your providers (nurses, doctors, physiotherapists). Each row is one payout for a period.

- Columns: ID, period start, period end, total, total before revenue cut, status (draft / processing / completed / failed / cancelled).
- Filter by status; cursor-based pagination via **Load More**.
- **Create** opens a modal for the period start/end dates and creates a draft batch.
- Row actions:
  - **View** — opens a detail modal listing the per-provider lines.
  - **Cancel** — only when status is `draft`.
  - **Execute** (inside the detail modal, draft only) — actually fires the payment.
  - **Export Excel** — for completed batches, downloads a spreadsheet.

### 10.4 Provider Settings

![Provider settings](screenshots/homecare/63-provider-settings-list.png)

Per-provider payout configuration.

- Columns: provider user ID, display name, email, phone, bank name, IBAN, revenue percentage, automated-payout flag.
- Edit a provider to set:
  - **Bank Full Name**, **IBAN** — for transfers.
  - **Revenue Percentage** — share of each booking that goes to the provider (0–1, e.g. 0.6 = 60%).
  - **Automated Payout** — toggle automatic execution at period end.

Provider records are created automatically when you add a doctor. You can't create or delete them from here — only configure their banking and revenue split.

---

## 11. Marketing

### 11.1 Coupons

![Coupons page](screenshots/homecare/70-coupons.png)

Embedded promotion-management. Issue discount codes (e.g. "first home visit 30% off"), set redemption windows, scope to specific clinics or services.

### 11.2 Banners

![Banners list](screenshots/homecare/71-banners-list.png)

Promotional banners that appear on the patient app's home screen.

![Banner create](screenshots/homecare/72-banners-create.png)

- Single-field form: **Image URL**.
- Use it for seasonal campaigns ("Ramadan home care offer"), service launches, or service notices.

---

## 12. Administration

### 12.1 Users

![Users list](screenshots/homecare/80-users-list.png)

Tenant admin users (everyone who can sign into this dashboard).

- Columns: name, email, role, assigned medical centers.
- Filter by name (top search) or by role/email at the column header.
- Click **Show** for the user profile.

> Users are read-only in the dashboard. To add or remove an admin, contact Codelines or use the management API.
>
> Role meanings:
>
> - **root_admin** — full access across all medical centers of the tenant.
> - **super_admin** — manage clinical and operational resources for assigned medical centers.
> - **medical_center_admin** — scoped to a single medical center, useful when you run multiple city branches.

---

## 13. Account recovery

### Forgot password (`/forgot-password`)

- Enter your **email** and submit.
- The system sends a password-reset link to that mailbox. The form turns into a confirmation message.

### Reset password (`/reset-password?token=...`)

- Open the link from the email.
- Enter a new **password** (minimum 6 characters) and **confirm** it.
- On success you're redirected to `/login?reset=success` and see a green confirmation banner.

If the link is missing the `token` query parameter, you'll see an "invalid token" alert — request a new reset from the Forgot Password page.

---

## 14. Things worth knowing

- **Bilingual everywhere.** Every list, form and confirm dialog ships in EN and AR. The globe icon in the top-right toggles language and direction.
- **Tenant switcher** lives in the page header (top-right) and lists the same organizations you saw at sign-in.
- **App URL chip** at the top of every page (left side of the header) shows the public domain for the patient-facing app, with a copy-to-clipboard icon — handy for training new dispatchers or sharing the booking link.
- **Unsaved changes** in forms trigger a confirmation if you try to navigate away.
- **Location matters most.** HomeCare+ tenants nearly always run with `requiresLocation = true`. That means the patient app filters doctors by service radius — if a doctor's pin is wrong or radius is too small, the doctor will never appear for that patient.
- **Resource & API endpoint mapping.** Every list/create/edit page in this guide maps to a Refine resource that calls `GET /api/<resource>`, `POST /api/<resource>`, `PATCH /api/<resource>/:id`, `DELETE /api/<resource>/:id`. Embedded webview pages (Apps, Messages, Invoices, Insurance Claims, Coupons) load a `scheduling-iframe?action=<feature>` config first.
- **Hidden resources accessed via Encounter.** Prescriptions, lab investigations, recommendations, and private notes are intentionally not in the main sidebar — they live under each Encounter's Show page (Prescriptions and Lab Investigations tabs). You can download them as PDFs from there.
- **NPHIES warnings.** A ⚠️ next to a doctor or clinic means a NPHIES code is missing; fix it before submitting claims.
- **Service radius hygiene.** Recommend revisiting each doctor's location pin and radius every quarter — staff move, traffic conditions change, and an overly generous radius leads to no-shows.
- **Platform infrastructure.** If you are a Codelines platform-root operator you'll see an extra link in the header to manage all tenants (`/organizations`). Normal tenant admins won't see this.
