# Indian exam demand and CBT capacity: evidence ledger

**Checked 9 November 2026.** This note separates measured participation, official infrastructure proposals, and capacity assumptions. It does not estimate a national shortage from the number of venues used by one exam.

## What the numbers actually say

| Year and population | Registered people | Appeared people | Meaning and primary source |
| --- | ---: | ---: | --- |
| NEET (UG) 2025 | 22,76,069 | 22,09,318 | One annual exam cohort. [NTA historical data, p. 1](https://cdnbbsr.s3waas.gov.in/s37bc1ec1d9c3426357e69acd5bf320061/uploads/2026/07/202607161539405935.pdf). |
| JEE Main 2025 **Paper 1** | 15,39,848 | 14,75,103 | Unique people across January and April, not the sum of both sessions. Excludes Paper 2 and JEE Advanced. [NTA result release dated 18 April 2025, p. 3](https://nta.ac.in/Download/Notice/Notice_20250419125449.pdf). |
| NEET (UG) 2026 | 22,79,743 | 19,99,895 | The published 2026 attendance accompanies the **21 June re-examination**. It must not be treated as a clean forecast of future attendance or evidence that underlying demand fell. [NTA historical data, p. 1](https://cdnbbsr.s3waas.gov.in/s37bc1ec1d9c3426357e69acd5bf320061/uploads/2026/07/202607161539405935.pdf), [16 July result release](https://cdnbbsr.s3waas.gov.in/s37bc1ec1d9c3426357e69acd5bf320061/uploads/2026/07/20260716477215762.pdf). |
| JEE Main 2026 **Paper 1** | 16,04,854 | 15,38,468 | Published unique people across January and April, with a minor arithmetic discrepancy noted below. [NTA result release, 20 April 2026, p. 3](https://nta.ac.in/Download/Notice/Notice_20260420194021.pdf). |

**Derived, matched-year comparison:** NEET/JEE Main Paper 1 registrations were **1.48× in 2025** and **1.42× in 2026**. Appeared-person ratios were **1.50×** and **1.30×**, respectively. The statement “NEET is twice JEE” is not supported by these annual unique-person figures. Dividing NEET by one JEE session produces a different denominator and must be labelled that way.

The harder capacity problem is **simultaneity**. The 2026 JEE release says Paper 1 used ten January shifts and nine April shifts; April used 584 unique CBT centres in 319 cities, including 15 cities abroad. The release reports 13,04,653 January and 10,34,330 April appearances: **23,38,983 candidate sittings** in total, including repeat participants. A machine may serve different candidates in successive shifts. These totals reveal neither the peak simultaneous attendance nor a national inventory of usable computers. [NTA JEE 2026 release, pp. 1 and 3](https://nta.ac.in/Download/Notice/Notice_20260420194021.pdf).

The NEET 2026 result release reports **5,440 centres** across 551 Indian cities and 14 overseas cities. The re-examination notice explicitly specifies **pen-and-paper mode**. Those centres cannot be counted as CBT-ready labs. The original 3 May plan and the 21 June re-examination also have different operational records; do not combine their venue or attendance figures. [NTA result release](https://cdnbbsr.s3waas.gov.in/s37bc1ec1d9c3426357e69acd5bf320061/uploads/2026/07/20260716477215762.pdf), [19 June re-examination notice, p. 1](https://cdnbbsr.s3waas.gov.in/s37bc1ec1d9c3426357e69acd5bf320061/uploads/2026/06/20260619440433404.pdf).

**Source-quality check:** the JEE 2026 table's session appearances minus common appearances give `13,04,653 + 10,34,330 − 8,00,516 = 15,38,467`, one below its published unique total of `15,38,468`. This note preserves the published unique figure and flags the discrepancy. It does not affect the ratios rounded to two decimals. Exact operational sizing requires the adopting authority's reconciled roster.

## Centre scarcity: supported concern, unmeasured national gap

The [9 October 2026 parliamentary committee release, paragraphs 10.6–10.7](https://www.pib.gov.in/PressReleasePage.aspx?PRID=2321420&lang=1&reg=3) recommends mapping and expanding government CBT facilities, investment in smaller cities and rural areas, a phased NEET transition, candidate mocks, and audited score normalisation for multiple sessions. It refers to a proposed 1,000 secure government centres and district coverage. These are recommendations and targets; they are not an inventory of completed facilities, installed seats, or a binding announced NEET conversion date. The cited 2026 operational record remains paper based. No future NEET mode should be inferred from this recommendation alone.

The [NTA EOI issued 7 November 2026](https://nta.ac.in/Download/Notice/Notice_20261107181531.pdf) invites both CBT and paper centres. It specifies 285 functioning CBT workstations including buffer per shift, allows smaller sites where supply is limited, and separately requires at least 5% spare workstations beyond declared candidate capacity. It also requires declared availability, accessibility, power backup, wired networking, and evaluation before empanelment. Thus an expression of interest or a count of buildings is not verified service capacity. Its buffer wording should be reconciled with the eventual contract before converting declared workstations into candidate places.

The reviewed sources support **uneven readiness and a need for expansion**. They do not supply a reconciled district-by-district inventory of seats that are secure, accessible, staffed, power-backed, independently inspected, and available on the same exam date. That missing inventory is a proposal checkpoint, not a number to invent.

## The capacity model Muhar should require

For region `r` and shift `s`, count `C(r,s)` as **audited usable candidate places after reserving spares**, considering centre availability, transport reach, language delivery, accessibility, staffing, power, network, and security exclusions. Demand `N(r,s)` is the scheduled cohort, with approved accommodations and late-centre policy. Require `N(r,s) ≤ C(r,s)` for every feasible assignment. A large national total cannot repair a shortage where candidates actually live.

For a simplified equal-capacity illustration, if one candidate takes one sitting and `C` usable places can be reused each shift, `minimum shifts = ceil(N/C)`. This is a mathematical lower bound, not a deployment plan: turnover, accommodation extensions, geography, staff rest, outages, and form fairness can require more time.

| Illustrative usable simultaneous capacity | Lower-bound shifts for 22,79,743 registered candidates |
| ---: | ---: |
| 2,00,000 | 12 |
| 3,00,000 | 8 |
| 4,00,000 | 6 |

These capacities are **hypothetical**, not measured Indian supply. A single simultaneous CBT sitting at this demand needs roughly 22.8 lakh usable candidate places before physical spare machines are added. If 10% of installed functioning machines were reserved as spares, a purely illustrative physical requirement would be `ceil(22,79,743 / 0.90) = 25,33,048`; the 10% is an example assumption, not an NTA rule.

More shifts ease machine demand but increase the need for reviewed equivalent forms, transparent normalisation, bank separation, leak response, and candidate travel protection. Copying JEE's software does not by itself establish NEET's assessment or infrastructure readiness. Muhar should support exam-specific delivery profiles while the adopting authority owns these choices.

## Mandatory evidence before any scale claim

1. **Capacity and reach:** obtain a dated centre/seat roster with measured usable seats, reserved spares, region, language/accommodation support, date availability, ownership/operator, inspection results, and travel-time distribution. Keep sensitive device details private.
2. **Failure-adjusted capacity:** rehearse full-duration demand, one failed centre, regional power loss, lost connectivity, and replacement seating without double-counting machines or assuming every rostered seat survives.
3. **Candidate fairness:** predeclare maximum journey and reporting burden, accessible mocks, score-equating method for multiple forms, delay/retest policy, and reimbursement or other remedy authority where applicable.
4. **Mode-specific custody:** treat CBT, encrypted local printing, and centrally printed papers as different adapters with different exposure points. Local printing still produces plaintext, spool files, waste copies, and staff access.
5. **Evidence hygiene:** preserve cohort/year/paper/session definitions in every dashboard. Report registrations, unique people, candidate sittings, and simultaneous usable seats as separate measures. Never use an attendance decline in a re-exam to justify undersizing the next normal cohort.

**Validation:** official PDFs and pages were inspected; scanned count tables and schedule pages were rendered and read visually; ratios and the table arithmetic were recalculated. No centre inventory, capacity test, procurement contract, or partner roster was available. No national shortage estimate or adoption forecast is claimed.
