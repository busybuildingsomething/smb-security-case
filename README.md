# Small Business Security Assessment — Luma Hair Studio

A mock GRC engagement for a fictional five-person hair salon in Celina, TX.

> **This business is fictional.** Luma Hair Studio does not exist. No real systems were tested and no real data appears in this repository. The scenario is modeled on the kinds of independent businesses opening in the area, and all findings are constructed to be realistic for a business of this size.

**Deliverables:** [Control Matrix](#) · [Risk Register](#) · [Assessment Report](#)

---

## The Business

Luma Hair Studio is an independent salon with one location and six people: an owner who makes every technology decision, two stylists, two booth-rental contractors, and a part-time receptionist. There is no IT staff, no security budget line, and no one whose job includes any of this.

The salon runs on a cloud booking platform, a card reader, social media, a shared front-desk tablet, and the owner's personal email account. It holds client contact details, appointment history, and cards on file for deposits.

That profile drives every scoping decision below.

## Why CIS Controls v8.1, Implementation Group 1

IG1 is defined as basic cyber hygiene for small organizations with limited expertise and no dedicated security staff. It is a subset of the full CIS Controls, scoped to what a business like this can realistically carry.

I considered and set aside:

| Framework | Why not |
|---|---|
| Full CIS Controls (IG2/IG3) | Assumes dedicated IT and security personnel. Recommending it to a six-person salon would produce a document nobody could act on. |
| ISO/IEC 27001 | Built around a certifiable management system. The salon has no certification requirement, no customer demanding one, and no capacity to run an ISMS. |
| NIST SP 800-53 | Scaled for federal systems. Vastly out of proportion. |
| NIST CSF 2.0 alone | Describes outcomes rather than specific controls. Strong for structure, but it wouldn't tell the owner what to actually do. |

**Choosing the smaller framework is the judgment this project is meant to show.** Over-scoping an assessment is a common failure: it produces an impressive-looking report that the business ignores because none of it is achievable. A proportionate assessment that gets implemented beats a comprehensive one that sits in a drawer.

## Why NIST CSF 2.0 as the organizing narrative

CIS IG1 is a list of safeguards. It tells you what to do but not how to explain the overall picture to an owner.

CSF 2.0's six functions — **Govern, Identify, Protect, Detect, Respond, Recover** — give the report a structure a non-technical reader can follow, and they expose imbalance. Small businesses typically concentrate everything in Protect and have almost nothing under Detect, Respond, or Recover. Grouping findings by function makes that visible in a way a flat control list does not.

So: **CSF supplies the narrative, IG1 supplies the controls.** Each finding in the report maps to a CSF function; each control in the matrix maps to a CIS safeguard.

## Why PCI DSS is addressed rather than ignored

The salon takes card payments, so PCI DSS applies. It is a contractual obligation through its payment processor and acquiring bank, not a law, and it applies regardless of size.

What that means in practice depends on how cards are actually accepted, which determines which Self-Assessment Questionnaire applies:

| How payments happen | Likely SAQ | Why it matters |
|---|---|---|
| Standalone card terminal on the salon's network, no card data stored electronically | SAQ B-IP | Short questionnaire covering the terminal, network, and physical handling |
| Validated point-to-point encryption terminal | SAQ P2PE | The shortest path; encryption at the terminal removes most of the environment from scope |
| Online deposits taken through the booking platform's hosted payment page | SAQ A | Applies to the e-commerce portion when all card handling is outsourced |

The salon takes cards both in person and online for deposits, so more than one of these may apply, and the processor and acquirer confirm which. **That confirmation is itself a finding**: an owner who cannot say which SAQ applies also cannot say whether the obligation is being met.

The practical recommendation is to keep scope as narrow as possible. Using a processor that tokenizes cards, never writing card numbers on paper or in appointment notes, and never storing them in the booking platform's free-text fields keeps the salon in the smallest questionnaire available.

**What is out of scope:** validating PCI compliance, completing an SAQ on the business's behalf, or assessing the processor's own environment. This engagement identifies the obligation, determines what likely applies, and recommends how to keep scope small.

## Methodology

1. Document the business, its assets, its data, and its constraints.
2. Assess current state against CIS Controls v8.1 IG1, recording status, evidence, and gap for each safeguard.
3. Translate gaps into risks, rated by likelihood and impact.
4. Recommend a treatment for each risk — mitigate, accept, transfer, or avoid — with effort and cost.
5. State residual risk after planned treatments, including risks the owner accepts.
6. Document assumptions and limitations.

Risk treatment decisions are recommendations. **The business owner is the risk owner** and accepts or rejects each one. Where this report records acceptance, that reflects a decision the owner would reasonably make given the constraints, and the rationale is written out.

## Limitations

- The business is fictional, so there is no real evidence to collect. Implementation status reflects constructed conditions documented in the business profile.
- No technical testing was performed. This is a policy, process, and configuration assessment, which is where most of the risk sits for a business this size.
- The assessment is a point-in-time snapshot.

## Repository Contents

| File | What it is |
|---|---|
| `00-business-profile.md` | The scenario: business, people, assets, data, constraints, and as-found conditions |
| `01-control-matrix.xlsx` | CIS IG1 safeguards with status, evidence, and gaps |
| `02-risk-register.xlsx` | Risks with ratings, treatment decisions, and residual risk |
| `03-assessment-report.pdf` | The written assessment |
| `decision-log.md` | Every judgment call made during the engagement and why |
