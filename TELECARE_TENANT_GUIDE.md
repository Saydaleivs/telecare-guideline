# Telecare Plus — Tenant Operations Guide

A step-by-step walkthrough of every screen in your Telecare Plus admin dashboard. Use it as a reference when onboarding a new tenant or training a new operator.

> Telecare Plus tenants typically deliver **video / phone consultations**. The dashboard helps you configure doctors, set prices, monitor appointments, run financials, and manage marketing — all from one place. Pages that depend on a physical address (e.g. doctor location, patient address) are still available but usually not required for telecare workflows.

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
   - [Encounters (Appointments)](#72-encounters-appointments)
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

![Telecare login](screenshots/telecare/01-login.png)

- Open the URL provided by Codelines (e.g. `https://<your-tenant>.telecare.codelines.sa/system/login`).
- Enter your **Email** and **Password** and click **Sign in**.
- Use the globe icon in the top right to switch between English and العربية. The whole dashboard is bilingual and switches RTL/LTR automatically.
- If you forgot your password, click **Forgot Password?** at the bottom of the card. See section 13 for the recovery flow.
- After a successful password reset, you'll see a green confirmation banner above the form on your next visit.

---

## 2. Choosing your organization

![Select organization](screenshots/telecare/02-select-organization.png)

If your account is linked to more than one tenant (e.g. you administer several clinics for the same group), you'll land on this screen right after sign-in.

- Each card shows the **tenant name**, **App ID**, your **role** for that tenant (`root_admin`, `super_admin`, `medical_center_admin`), and any medical centers you're scoped to.
- Type into the **search bar** to filter by name or App ID.
- Click **Select** on the tenant you want to manage. The dashboard then loads with that tenant's data.
- **Back to login** clears the local session and returns you to the sign-in page.

Once selected, your tenant is remembered for that browser session. You can switch tenants any time from the header dropdown in the top-right corner.

---

## 3. Getting started wizard

![Getting started wizard](screenshots/telecare/03-getting-started.png)

New tenants land here automatically until every required setup step is complete. The wizard configures the eight things every Telecare tenant needs before booking can work:

| Order | Step | What you provide |
|-----:|------|------------------|
| 1 | Medical center | EN/AR name, MOH license, contact details, address, status |
| 2 | Clinic type | E.g. "General", "Dermatology" — the type of clinic |
| 3 | Speciality | E.g. "Cardiology", "Family Medicine" |
| 4 | Rank type | Doctor levels: Consultant, Specialist, GP, etc. |
| 5 | Consultation type | "Video", "Voice", "Chat" — the modalities you support |
| 6 | Clinic | One concrete clinic = clinic-type × medical-center |
| 7 | Doctor | A practitioner with name, gender, clinic, rank, speciality |
| 8 | Rank price | Price per (rank × clinic × consultation type) |

- The **progress bar** at the top shows how many steps are complete (e.g. `3 / 8`).
- **Save and Continue** moves to the next step. **Save and Add Another** is offered after a step is satisfied so you can register multiple medical centers, doctors, etc.
- **Skip** lets you defer a step (it can still be completed later from its dedicated page).
- **View** jumps to the full list page for the resource (e.g. to see all medical centers you've added).
- When every required step is satisfied, the wizard shows a success card and a **Go to Dashboard** button that takes you to Analytics.

> You can revisit `/getting-started` at any time from the left sidebar.

---

## 4. Analytics dashboard

![Analytics dashboard](screenshots/telecare/04-analytics.png)

Your daily operations homepage. It pulls real-time KPIs from `GET /api/management/analytics` and recent encounters.

The page is organized top to bottom:

1. **Organisation Overview** — Three clickable KPI cards: total **Patients**, **Doctors**, and **Total Appointments**. Click any of them to jump to that resource's list.
2. **All Appointments** — Today vs. all-time breakdown by status:
   - Today: Upcoming / Ongoing / Completed / Canceled
   - All-time: same four buckets
3. **Finance & Payments** — Four colored cards (Total Billed, Collected, Pending, Canceled) followed by a **Recent Payments** table with patient, doctor, date, amount and status. **View All Transactions** links to *Payout Transactions*.
4. **Appointment Insights**
   - **Appointment Status** — rose chart of status distribution
   - **Appointment Breakdown** — column chart comparing categories
5. **Appointments by Doctor** — bar chart of top doctors by volume. Switch the time window with the segmented control (**Today / This Week / This Month / Year to Date**).
6. **Top Performers** — Two leaderboards: Top Doctors and Top Patients, each with medal badges. Clicking a row navigates to that doctor/patient's profile.

---

## 5. Doctors & Staff

### 5.1 Doctors

![Doctors list](screenshots/telecare/10-doctors-list.png)

Lists every practitioner in the tenant. Columns: ID, name (EN/AR), email, gender, clinic type, rank, status, NPHIES practice code (⚠️ icon if missing — NPHIES claims won't work without it).

- Filter by **gender** and **status** with the column headers.
- Row actions: **Show** profile, **Edit**, **Delete** (confirms first), **📅 Manage Availability** (opens the scheduling iframe for shifts/working hours), **🌴 Manage Vacations**.

#### Creating a doctor

![Doctors create](screenshots/telecare/11-doctors-create.png)

Fields:

- **Names** (English + Arabic), **Email**, **Contact info**, **Gender**
- **Clinic**, **Rank**, **Speciality** (dropdowns sourced from the matching lookups)
- **NPHIES practice code** — required if the tenant participates in NPHIES claims
- **Subspecialties**, **Description** (EN + AR), **Avatar** upload, **Status**

> The **Location** section (latitude, longitude, address, radius) only appears when the tenant's booking config has `requiresLocation = true`. Telecare tenants normally don't need this. If your tenant occasionally dispatches doctors to homes, it can be turned on; otherwise leave it off.

### 5.2 Specialities

![Specialities list](screenshots/telecare/12-specialities-list.png)

A lookup table of medical specialities used to tag doctors and filter the patient-facing booking app.

![Speciality create](screenshots/telecare/13-specialities-create.png)

- Fields: **Name (EN)**, **Name (AR)**.
- Add one entry per speciality you offer; the patient app uses this list to filter doctors.

### 5.3 Ratings

![Ratings list](screenshots/telecare/14-ratings-list.png)

Read-only feedback that patients submit after a completed encounter. Columns: encounter ID, star rating (out of 5, rendered from a 1–10 score), free-text review, created date.

- Use the filters at the column headers to find ratings by encounter or score.
- Ratings cannot be edited or deleted from here — this is purely a review screen.

---

## 6. Clinics & Centers

### 6.1 Clinics

![Clinics list](screenshots/telecare/20-clinics-list.png)

A clinic is one concrete department inside a medical center (e.g. "General Medicine at TeleCare HQ"). Columns: clinic type, medical center, contact number, status, doctor count, NPHIES specialty code.

![Clinic create](screenshots/telecare/21-clinics-create.png)

- **Clinic type** — pick from the seeded list (set up via Getting Started).
- **Medical center** — the parent facility.
- **NPHIES clinic specialty code** — used in claims.
- **Contact number**.

Row actions: Show / Edit / Delete.

### 6.2 Medical Centers

![Medical centers list](screenshots/telecare/22-medical-centers-list.png)

Top-level facilities under your tenant — usually one per branch.

- Columns: bilingual name, address, contact, MOH license, status.
- Edit a center to update its EN/AR name, address, MOH license, contact phone, official email, website, logo URL, digital stamp URL, latitude/longitude, status.

> Even for telecare, a medical center carries the **MOH license** that links your tenant to regulatory and NPHIES integrations, plus the **digital stamp** used on PDFs (prescriptions, lab orders). Keep these accurate.

---

## 7. Patients & Encounters

### 7.1 Patients

![Patients list](screenshots/telecare/30-patients-list.png)

Every patient who has registered or been registered for an appointment.

- Columns: ID, English name, email, phone, national ID.
- Filter by email or phone via the column headers, or use the top **search** for free-text matches.
- Click **Show** for the profile or **Edit** to update the name, email, phone, national ID, or a free-form note.

> Patients can only be created from the booking app or via the API. The dashboard view is intentionally read-mostly — keep edits to corrections.

### 7.2 Encounters (Appointments)

![Encounters list](screenshots/telecare/31-encounters-list.png)

Every booked, completed, or canceled appointment.

- Columns: ID, patient name, doctor name, clinical notes count, start time, "is canceled" flag.
- Filters: patient, doctor, status (Confirmed / Canceled), plus a top **search** by patient or doctor name.
- **+ Add Appointment** opens a modal: the dashboard fetches the list of available doctors, lets you pick one, and renders the scheduling iframe to book in their calendar. On save, the list refreshes.
- The **Show** view (eye icon) of an encounter has its own action bar:
  - **Booking Details** — opens the underlying booking record.
  - **Reschedule** — opens a scheduling iframe pre-loaded with the encounter's date.
  - **Cancel Booking** — collects a reason and calls the cancel endpoint.
  - Tabs for **Prescriptions** and **Lab Investigations** scoped to this encounter.

> Telecare appointments will typically be **Online** consultation type. The patient and the doctor join from the patient/doctor mobile apps; this dashboard is for back-office monitoring, not the call itself.

---

## 8. Pricing & Ranks

### 8.1 Rank Types

![Rank types list](screenshots/telecare/40-rank-types-list.png)

Doctor seniority levels you charge differently for (Consultant / Specialist / GP / etc.).

![Rank type create](screenshots/telecare/41-rank-types-create.png)

- Fields: **Name (EN)**, **Name (AR)**.

### 8.2 Rank Prices

![Rank prices list](screenshots/telecare/42-rank-prices-list.png)

The pricing matrix: one entry per (rank × clinic × consultation type).

![Rank price create](screenshots/telecare/43-rank-prices-create.png)

- **Rank**, **Clinic**, **Consultation type** — pick from the seeded lookups.
- **Price** in your tenant's currency.
- **Duration (minutes)** — how long this consultation slot is.
- **Description** — visible in the patient app.

> When a tenant's booking policy is `leastFirst`, the **Rank** field is hidden — the system always books the cheapest applicable rank automatically. You'll see this on tenants where the patient picks "I want the cheapest" instead of a specific seniority.

---

## 9. Integrations

These pages embed the same scheduling-platform UI that the patient and doctor apps consume. The dashboard fetches a tenant-specific config from `/api/management/organization/scheduling-iframe?action=<feature>` and renders an iframe.

### 9.1 Apps

![Apps page](screenshots/telecare/50-apps.png)

Manage the **add-ons** enabled for this tenant on the scheduling backend (e.g. notifications, integrations, custom flows).

### 9.2 Messages

![Messages page](screenshots/telecare/51-messages.png)

Configure SMS/email/WhatsApp templates and channels via the scheduling messages module.

---

## 10. Financial

### 10.1 Invoices

![Invoices page](screenshots/telecare/60-invoices.png)

Embedded invoice management from the scheduling platform: issue invoices, view paid/unpaid status, attach to encounters.

### 10.2 Insurance Claims

![Insurance claims](screenshots/telecare/61-insurance-claims.png)

Embedded NPHIES claims workflow. You can submit eligibility checks, pre-authorizations, and reimbursement claims for encounters where the patient has insurance.

> Claims will only work if the doctor's **NPHIES practice code** and the clinic's **NPHIES specialty code** are filled in (you'll see ⚠️ icons on the doctors and clinics list when they're missing).

### 10.3 Payout Transactions

![Payout transactions](screenshots/telecare/62-payout-transactions.png)

Batch payments to your providers (doctors). Each row is a payout for a period.

- Columns: ID, period start, period end, total, total before revenue cut, status (draft / processing / completed / failed / cancelled).
- Filter by status. Pagination is cursor-based — click **Load More** for older batches.
- **Create** opens a modal for the period dates and creates a draft batch.
- Row actions:
  - **View** — opens a detail modal listing the per-provider lines.
  - **Cancel** — only when status is `draft`.
  - **Execute** (inside the detail modal, draft only) — fires the payment.
  - **Export Excel** — completed batches export the line items.

### 10.4 Provider Settings

![Provider settings](screenshots/telecare/63-provider-settings-list.png)

Per-provider payout configuration.

- Columns: provider user ID, display name, email, phone, bank name, IBAN, revenue percentage, automated-payout flag.
- Edit a provider to set:
  - **Bank Full Name**, **IBAN** — for transfers.
  - **Revenue Percentage** — share of each booking that goes to the provider (0–1, e.g. 0.7 = 70%).
  - **Automated Payout** — toggle automatic execution at period end.

Creation/deletion are intentionally disabled — providers are auto-created when a doctor is added.

---

## 11. Marketing

### 11.1 Coupons

![Coupons page](screenshots/telecare/70-coupons.png)

Embedded promotion-management page. Create discount codes, set redemption windows, scope to specific clinics or services.

### 11.2 Banners

![Banners list](screenshots/telecare/71-banners-list.png)

Promotional banners that appear in the patient app's home screen.

![Banner create](screenshots/telecare/72-banners-create.png)

- Single-field form: **Image URL**.
- The list shows a thumbnail per banner; reorder by deleting/re-adding (sequence is creation order).
- Use this for campaigns, seasonal promotions, or notices.

---

## 12. Administration

### 12.1 Users

![Users list](screenshots/telecare/80-users-list.png)

Tenant admin users (everyone who can sign into this dashboard).

- Columns: name, email, role (super_admin / root_admin / medical_center_admin), assigned medical centers.
- Use the top **search** to find by name; column filters narrow by email or role.
- Click **Show** to inspect a user's full profile.

> This page is read-only by design. To invite or remove users, contact Codelines or use the API. Roles are:
>
> - **root_admin** — full access across all medical centers of the tenant.
> - **super_admin** — manage clinical and operational resources for assigned medical centers.
> - **medical_center_admin** — scoped to a specific medical center.

---

## 13. Account recovery

### Forgot password (`/forgot-password`)

- Enter your **email** and submit.
- The system sends a password-reset link to that mailbox. The form turns into a success confirmation.

### Reset password (`/reset-password?token=...`)

- Open the link in the email.
- Enter a new **password** (minimum 6 characters) and **confirm** it.
- On success you're redirected to `/login?reset=success` and see a green confirmation banner.

If the link is missing the `token` query parameter, you'll see an "invalid token" alert; request a new reset email from the Forgot Password page.

---

## 14. Things worth knowing

- **Bilingual everywhere.** Every list, form and confirm dialog ships in EN and AR. The globe icon in the top-right toggles language and the whole app switches direction automatically.
- **Tenant switcher** lives in the page header (top-right). It lists the same organizations you saw at sign-in.
- **Unsaved changes** in forms trigger a confirmation if you try to navigate away.
- **App URL chip** at the top of every page (left side of the header) shows the public domain for the patient-facing app, with a copy-to-clipboard icon — useful when training new staff or sending links to patients.
- **Resource & API endpoint mapping** — every list/create/edit page in this guide maps to a Refine resource that calls `GET /api/<resource>`, `POST /api/<resource>`, `PATCH /api/<resource>/:id`, `DELETE /api/<resource>/:id`. Embedded webview pages (Apps, Messages, Invoices, Insurance Claims, Coupons) load a `scheduling-iframe?action=<feature>` config first.
- **Where prescriptions, lab investigations, recommendations, and private notes live.** These are intentionally hidden from the main sidebar — they're authored by doctors in the doctor mobile app and surfaced under each Encounter's Show page (Prescriptions and Lab Investigations tabs). You can download them as PDFs from there.
- **Common warning icons.** A ⚠️ next to a doctor or clinic means a NPHIES code is missing; fix it before submitting claims.
- **Need infrastructure access?** If you are a Codelines platform-root operator you'll see an extra link in the header to manage all tenants (`/organizations`). Normal tenant admins won't see this.
