# Pre-enrolment (email list) — Support & Documentation

**Moodle plugin:** `enrol_preenrol` · Version 1.1.3 · Moodle 4.1–5.3 · GPL v3

![Status](https://img.shields.io/badge/version-1.1.3-blue) ![Support](https://img.shields.io/badge/Moodle-4.1%E2%80%935.3-success)

- 🐞 **Report a bug / request a feature:** use the [Issues tab](https://github.com/stadtschamane/enrol_preenrol-support/issues)
- 💬 **Questions and general discussion:** use [Discussions](https://github.com/stadtschamane/enrol_preenrol-support/discussions) — the Q&amp;A category for usage questions, *Ideas* to discuss possible features. Bug reports and concrete feature requests stay in the issue tracker so they can be triaged.
- 📦 **Buy the plugin:** Moodle Marketplace — licence model: *one-time payment, lifetime updates*
- 🔐 The plugin code repository is **private** (kept closed by the maintainer). Marketplace purchases ship the complete GPL v3 source code with the plugin. This public repository is the support and documentation point.

---

## What the plugin does

**Pre-enrolment (email list)** lets course managers enrol people into a course by importing a list of e-mail addresses before those people have a Moodle account. As soon as an account with a matching address is created for the first time (self-registration with admin confirmation, automated SAML/ADFS account creation, or web service), the person is enrolled automatically — a normal course enrolment, fully compatible with groups, activity restrictions, completion and grades.

**Key features:** bulk import via pasted list or CSV/TXT upload · detailed 5-category import report (pending / enrolled / already enrolled / invalid / duplicate) · idempotent re-import · enrolment duration, start and end date honoured (a future start date reserves the seat and activates automatically) · standard Edit/Unenrol controls for enrolled users · pending-list management with single-row deletion · course backup, restore and copy supported · Privacy API support · Moodle 4.1–5.3 (CI-verified: PHP 8.1–8.3, MariaDB + PostgreSQL).

| | |
|---|---|
| Plugin type | Enrolment method (`enrol_preenrol`) |
| Supported Moodle versions | 4.1 – 5.3 |
| Requirements | Moodle 4.1+ on PHP 8.1+ (Moodle 5.2+ itself requires PHP 8.3) |
| Licence | GPL v3 (full source ships with every purchase) |
| Data stored | E-mail addresses of the pending list until first account creation; deleted via Privacy API |
| Database table | `enrol_preenrol_pending` (unique per enrol-method + e-mail) |

---

## How it works — the flow

1. **Add the method** in your course (role, duration, dates — all standard Moodle fields).
2. **Import your list** via the + icon: paste one e-mail per line (comma/semicolon/tab also fine) or upload a .csv/.txt file.
3. **Read the report:** every import shows a 5-category result per address — *Pending / Enrolled / Already enrolled / Invalid / Duplicate*. Re-importing the same list changes nothing (idempotent).
4. **People get enrolled automatically** the moment their account is created — no manual step, ever.
5. **Manage afterwards:** enrolled people use the standard Edit/Unenrol icons; the pending table supports single-row deletion at any time.

### Screenshots

Enrolment methods page with the Pre-enrolment instance (pending counter + import icon):

![Enrolment methods](screenshots/new_09_methods_with_pending.png)

Import page with field-level help (?), CSV/TXT upload and the pending table:

![Import page](screenshots/new_06_pending_consumed.png)

Import report — all 5 categories, one line per address:

![Import report](screenshots/new_03_report_all5.png)

The automatic enrolment, live-verified with a real signup through the e-mail-confirmation flow:

![Auto enrol proof](screenshots/new_07_participants_after_signup.png)

The standard unenrol confirmation dialog — pre-enrolled users stay fully manageable:

![Unenrol dialog](screenshots/new_08_unenrol_modal.png)

---

## What's new in 1.1.x

- **Enrolment duration, start and end date are applied to the enrolment.** Previously an imported person was enrolled with defaults regardless of the times configured in the method. A start date in the future now reserves the seat — the enrolment exists but only becomes active on that date, exactly like a normal Moodle enrolment. A duration takes precedence over an end date, matching the behaviour of Moodle's own self-enrolment.
- **Case-insensitive e-mail matching with batched lookup.** Addresses match regardless of capitalisation (`Anna@Example.com` finds `anna@example.com`), and the importer looks addresses up in batches instead of one query per address — which matters on PostgreSQL, where e-mail comparison is case-sensitive and a second bulk import would otherwise rescan the user table row by row.
- **The method can be deleted and hidden/shown** through the standard controls on the enrolment methods page — those icons were missing before.
- **Course backup, restore and course copy are supported:** duplicating a course keeps the pre-enrolment method and its existing enrolments. Open reservations are not part of a course backup — a copy starts with the method and an empty pending list.
- **Marketplace review fixes:** every capability now ships its language string, and every PHP file carries the complete Moodle boilerplate header.

## Changelog

| Version | Date | Notes |
|---|---|---|
| 1.1.3 | 2026-10-22 | Enrolment duration / start / end date applied to the enrolment |
| 1.1.2 | 2026-10-22 | Case-insensitive account matching, batched address lookup |
| 1.1.1 | 2026-10-22 | Method can be deleted and hidden/shown |
| 1.1.0 | 2026-10-22 | Course backup, restore and copy support |
| 1.0.3 | 2026-10-19 | Capability language strings, complete boilerplate headers |
| 1.0.2 | 2026-10-09 | Field-level help on the import form; cancel redirect and breadcrumb fix |
| 1.0.1 | 2026-10-09 | UI polish: help texts, CSV/TXT only, no extra confirmation checkbox |
| 1.0.0 | 2026-10-09 | First release |

---

## Pricing

- **One-time payment, lifetime updates** — every future release of the plugin is included.
- Sold and transaction-handled through the official [Moodle Marketplace](https://marketplace.moodle.com).
- Purchases include the full GPL v3 source code.

## Issues & support

Please use the [issue tracker](https://github.com/stadtschamane/enrol_preenrol-support/issues) with the provided templates — bug reports get version numbers and Moodle/PHP details, feature requests are triaged by upvotes. Response window: usually within a few days.

---

*Pre-enrolment (email list) for Moodle — maintained by Stadtschamane.*
