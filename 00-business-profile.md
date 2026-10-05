# 00 — Client Business Profile
**Luma Hair Studio** · Simulated Security Engagement

> **Disclaimer:** Luma Hair Studio is a fictional business created for a portfolio case study. Any resemblance to a real business is coincidental. All testing is done only on systems the consultant owns.

| | |
|---|---|
| **Consultant** | Tre |
| **Engagement type** | Website build + small-business security and GRC assessment |
| **Started** | September 2026 |
| **Framework references** | CompTIA Security+ (SY0-701), CIS Controls v8.1 Implementation Group 1 |
| **Document status** | Draft v0.2 |

---

## 1. Business Overview

Luma Hair Studio is an independent salon in a Celina, TX strip center. It opened in early 2025 and has grown mostly through Instagram and word of mouth. The owner wants a professional website with online booking to compete with the new chain salons opening nearby.

- **Services:** Cuts, color, balayage, extensions, blowouts, bridal and event styling
- **Hours:** Tuesday–Saturday; Saturdays are the busiest day and can't tolerate downtime
- **Size:** One location, six people, about 150 appointments per week
- **Revenue drivers:** Color and extension services, which require deposits

## 2. People and Roles

| Role | Count | Employment type | Notes |
|---|---|---|---|
| Owner / lead stylist | 1 | Owner | Makes all tech decisions; non-technical |
| Stylist | 2 | Employee | Uses front-desk tablet and own phone |
| Booth-rental stylist | 2 | Independent contractor | Runs own clientele but books through salon's system |
| Receptionist | 1 | Part-time employee | Handles check-in, checkout, phones, DMs |
| Bookkeeper | 1 | Outside vendor | Remote access to payment and payroll reports |

## 3. Technology and Vendor Inventory

| Asset / Service | What it does | Who manages it |
|---|---|---|
| Website (to be built) | Service menu, gallery, booking link, contact form | Consultant |
| Domain name | Business web address | Registered by owner's nephew on his personal account |
| Cloud booking platform | Appointments, client records, deposits, reminders | Owner |
| Card reader + POS | In-person payments, cards on file | Owner |
| Business email | Client and vendor communication | Owner's personal free email account |
| Instagram + Facebook | Marketing and most new-client bookings via DMs | Owner and receptionist |
| Front-desk tablet | Check-in, checkout, booking app | Shared by all staff |
| Owner's laptop | Bookkeeping exports, marketing, personal use | Owner |
| Staff personal phones | Booking app, Instagram posting | Each stylist |
| Wi-Fi router (ISP-provided) | Internet for devices, POS, and guests | ISP default setup |
| Security cameras | Cloud-recorded video of entrance and front desk | Owner |
| Front door keypad | After-hours entry for staff | Owner |

## 4. Data the Business Handles

| Data | Where it lives | Sensitivity |
|---|---|---|
| Client name, phone, email | Booking platform, staff phones | Moderate (PII) |
| Appointment history and color formulas | Booking platform | Low–Moderate |
| Payment cards on file (for deposits/no-shows) | Payment processor | High (PCI DSS scope) |
| Client notes (sometimes include scalp or skin sensitivities) | Booking platform | High (health-adjacent, over-collected) |
| Before/after photos | Staff phones, Instagram | Moderate (needs client consent) |
| Staff pay and contractor rent records | Bookkeeper, owner's laptop | High (confidential) |
| Camera footage | Cloud video service | Moderate |

## 5. As-Found Conditions

These are the conditions observed at the start of the engagement, before any changes.

1. **Shared login:** Everyone uses one booking platform account on the front-desk tablet.
2. **Former staff access:** A stylist who left in spring 2026 still has an active account.
3. **No MFA:** Instagram, email, and the booking platform use passwords only.
4. **Password reuse:** The owner uses the same password on email, Instagram, and the booking platform.
5. **Domain ownership:** The domain is on a family member's personal account, not the business's.
6. **Personal email as admin:** The owner's personal email is the recovery address for every business account.
7. **Flat network:** Guest Wi-Fi password is posted at the front desk, and guests share the network with the tablet and card reader.
8. **Unchanged door code:** The keypad code hasn't changed since opening, and former staff know it.
9. **Default camera credentials:** The camera system still uses its factory admin password.
10. **No backups:** Client records exist only inside the booking platform, with no export or backup.
11. **No written policies:** There's no acceptable use, password, or incident response guidance.
12. **Over-collection:** Staff type sensitivity details into free-text client notes.

## 6. Business Goals and Constraints

**Goals**
- Launch a mobile-friendly website with online booking and deposits
- Grow Instagram without risking account takeover
- Look established and trustworthy next to chain competitors

**Constraints**
- Limited budget; prefers free or low-cost tools
- Owner has little time and no technical background
- No downtime on Saturdays
- Booth renters are independent, so the salon can't dictate everything they do

## 7. Engagement Scope

**In scope**
- Website, domain, and hosting
- Business email and social media accounts
- Booking platform and payment configuration (settings only)
- Front-desk tablet and owner's laptop
- Salon Wi-Fi and network setup
- Physical access controls (door keypad, cameras)
- Policies, risk documentation, and staff guidance

**Out of scope**
- Active penetration testing or exploitation
- Staff personal devices, beyond how they access salon systems
- Booth renters' separate businesses
- The vendors' own internal systems

**Rules of engagement**
- All technical testing is performed only on consultant-owned lab systems that simulate this environment.
- Findings are documented for portfolio use; no real client data is collected.

## 8. Documented Assumptions

Each assumption notes what changes if it turns out to be wrong.

| ID | Assumption | If wrong |
|---|---|---|
| A1 | The booking platform supports individual user accounts and role-based permissions. | Shared login remains; compensating controls needed (see D-log and residual risk). |
| A2 | The payment processor tokenizes cards, so the salon never stores full card numbers. | PCI DSS scope expands significantly; payment setup must be redesigned. |
| A3 | The owner can give about one hour per week to security tasks. | Rollout slows; priorities narrow to the top three risks. |
| A4 | New security tooling must stay under $50/month total. | Paid options (managed Wi-Fi, business email suite) become viable. |
| A5 | All staff have smartphones that can run an authenticator app. | Hardware security keys or SMS as a weaker fallback. |
| A6 | The ISP router can run a separate guest network, or a low-cost replacement is acceptable. | Guest Wi-Fi is removed until segmentation is possible. |
| A7 | Booth renters will follow rules for salon-owned systems as a condition of their rental agreement. | Their access is restricted further, or they manage bookings outside salon systems. |
| A8 | The salon qualifies as a small business for Texas privacy law, but Texas breach notification rules still apply. | Additional privacy obligations; to be verified in Deliverable 10. |

## 9. Decision Log

| ID | Decision | Options considered | Justification | Trade-off accepted |
|---|---|---|---|---|
| D1 | Use a fictional business | Real local business; fictional business | Assessing a real business requires permission and risks exposing its weaknesses. A mock allows unrestricted lab testing. | Less authentic stakeholder input. Mitigated by basing the scenario on the types of businesses actually opening in Prosper/Celina in 2026. |
| D2 | Model a hair salon | Salon; med spa; fitness studio; bakery | Beauty and personal care was the most common independent opening type locally. Salons have real PII, payment, vendor, and physical risks without HIPAA complexity. | Less regulatory depth to showcase than a health-adjacent business. |
| D3 | Use CIS Controls IG1 as the baseline | CIS IG1; NIST CSF 2.0; ISO 27001 | IG1 is designed for small organizations with limited IT expertise and gives prescriptive, checkable safeguards. | Less recognized in enterprise settings than NIST CSF. Mitigated by a CSF crosswalk in the final summary. |
| D4 | Test only in a consultant-owned lab | Test real vendor systems; lab only | Keeps testing legal and within rules of engagement. | Scan results reflect a simulated environment, and the case study says so. |

## 10. Anticipated Challenges and Responses

| Challenge | Why it's likely | Planned response |
|---|---|---|
| Owner resists MFA because it could slow busy checkouts | Saturday revenue is the priority | Roll out on a Tuesday, start with owner and email accounts, and use authenticator push or passkeys to keep sign-ins fast. |
| Individual booking accounts cost more per seat | Many platforms charge per user | Compare seat cost against the risk of untraceable refunds and client data changes. If unaffordable, keep the shared login with a daily refund and edit review as a compensating control. |
| Booth renters push back on salon rules | They're independent and run their own clientele | Tie access requirements to the rental agreement and limit their permissions to their own clients. |
| Family member is slow to transfer the domain | Relies on someone outside the business | Request the transfer in writing. In the meantime, enable MFA on his registrar account and add the owner as a contact. |
| Staff keep typing sensitivity details into free-text notes | Habit and convenience | Replace with a standard "patch test required" flag and cover it in a short staff walkthrough. |

## 11. Expected Residual Risk

Residual risk is what remains after controls are applied. Each item has the owner as risk owner and will be finalized with ratings in the Risk Register (Deliverable 07).

| Risk | Why it can't be eliminated | Treatment | Expected residual level |
|---|---|---|---|
| Compromise of a booth renter's personal phone | The salon can't manage devices it doesn't own | Mitigate with MFA and least privilege, then accept | Medium |
| Breach at the booking platform vendor | Outside the salon's control | Transfer partially through vendor security commitments; mitigate with regular client list exports | Medium |
| Social engineering of the receptionist through DMs or calls | Training reduces but doesn't remove human error | Mitigate with a simple verification rule for refund and account requests | Medium |
| Shared tablet login, if per-user seats are unaffordable | Budget constraint (A4) | Accept with daily review as a compensating control | Medium–Low |

## 12. Deliverables Tracker

**Quality standard for every deliverable:** Each one includes the scenario and constraints it addresses, documented assumptions and trade-offs, explicit decisions with justifications, anticipated challenges and responses, and a clear statement of residual risk.

| # | Deliverable | Security+ section | Status |
|---|---|---|---|
| 00 | Business profile (this document) | Setup | Draft |
| 01 | Gap analysis and security requirements | 1.2 | Not started |
| 02 | Change management procedure | 1.3 | Not started |
| 03 | Cryptography and credential-handling standard | 1.4 | Not started |
| 04 | Threat profile | Domain 2 | Not started |
| 05 | Security architecture diagram | Domain 3 | Not started |
| 06 | Hardening checklist and scan results | Domain 4 | Not started |
| 07 | Risk register | Domain 5 | Not started |
| 08 | Vendor risk review | Domain 5 | Not started |
| 09 | Incident response plan | Domain 5 | Not started |
| 10 | Policies and privacy notice | Domain 5 | Not started |
| 11 | Final case study summary | Wrap-up | Not started |

## 13. Preview: Section 1.2 Concepts in This Environment

| Concept | Where it shows up at Luma |
|---|---|
| Confidentiality | Client PII, cards on file, staff pay records |
| Integrity | Booking records, deposit amounts, website content |
| Availability | Saturday booking uptime, no backups |
| Authentication | Shared login, no MFA, password reuse |
| Authorization | Former stylist access, everyone has admin rights |
| Accounting | Shared account means no way to tell who did what |
| Non-repudiation | Can't prove which staff member issued a refund |
| Zero trust | Flat Wi-Fi network, implicit trust of anyone on the tablet |
| Physical security | Unchanged door code, default camera password |
| Deception technology | Honeypot field on the new website contact form |
| Gap analysis | Deliverable 01 compares as-found state to CIS IG1 |
