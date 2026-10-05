# Decision Log

Every judgment call made during this engagement, with the reasoning and the trade-off accepted. Feeds the assumptions and limitations section of the assessment report.

| ID | Date | Decision | Alternatives considered | Rationale | Trade-off accepted |
|---|---|---|---|---|---|
| D1 | 2026-09 | Use a fictional business | Assess a real local business | A real assessment requires written permission, and publishing another business's weaknesses would be irresponsible. A mock allows full publication. | No real stakeholder pushback. Mitigated by modeling constraints on real local business types. |
| D2 | 2026-09 | Model an independent hair salon | Med spa, fitness studio, bakery | Beauty and personal care is the most common independent business type opening locally. Carries real PII, payment, vendor, and physical risk without HIPAA complexity. | Less regulatory depth than a health-adjacent business. |
| D3 | 2026-09 | Assess against CIS Controls v8.1 IG1 | Full CIS Controls, ISO 27001, NIST SP 800-53, CSF alone | IG1 is explicitly scoped to small organizations without dedicated IT. Proportionality is the point. | Less recognized in enterprise interviews than ISO or NIST. Mitigated by CSF structure. |
| D4 | 2026-09 | Use NIST CSF 2.0 functions as the report's structure | Organize by CIS control number, or by risk severity | CSF functions are readable by a non-technical owner and expose imbalance across Detect, Respond, and Recover. | Adds a second framework to explain. Handled in one README section. |
| D5 | 2026-09 | Address PCI DSS scope rather than exclude payments | Scope payments out entirely | The business takes cards, so the obligation exists. Ignoring it would be the most obvious gap to a compliance reviewer. | Cannot determine the applicable SAQ without processor confirmation. Documented as a finding rather than assumed. |
| D6 | 2026-09 | No technical testing; policy, process, and configuration only | Include vulnerability scans of a lab environment | For a six-person business with no infrastructure, nearly all risk is in access, process, and vendor management. Scan output would pad the report without informing decisions. | No technical depth demonstrated. Acceptable: the target audience is a compliance hiring manager. |
| D7 | 2026-09 | Three deliverables, no tooling | Scripts to generate the matrix, a dashboard, automation | Three well-reasoned documents demonstrate judgment. Tooling would demonstrate effort spent on the wrong thing. | None material. |
