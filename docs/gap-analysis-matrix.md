# Gap analysis matrix — current state vs. Epic Willow future state

This document compares current-state inpatient pharmacy operations against Epic Willow 
future-state workflows. Each row identifies a workflow area, the current-state process, 
the Epic future-state process, the gap between them, and the action required from the 
analyst and the organization.

---

## How to read this document

- **Current state:** How the workflow operates today, before Epic Willow go-live
- **Epic future state:** How the workflow will operate after go-live with proper build
- **Gap:** What is different, missing, or requires change
- **Analyst action:** What must be built or configured in Epic
- **Org action:** What training, policy, or process change is required from the organization

---

## Section 1 — Order entry and routing

| Workflow | Current state | Epic future state | Gap | Analyst action | Org action |
|---|---|---|---|---|---|
| Medication order entry | Verbal, telephone, or paper orders transcribed by pharmacy | Prescriber enters all orders directly in Epic CPOE | Prescribers must enter all own orders — no more verbal order transcription by pharmacy | Build order sets, preference lists, and formulary search to make entry fast and accurate | Prescriber training on CPOE; policy change requiring direct order entry |
| Stat medication request | Nurse calls pharmacy by phone for stat medications | Nurse marks order STAT in Epic; routes to top of pharmacy queue with visual flag | Nurses must know how to flag stat priority in Epic correctly | Build STAT routing logic and visual priority display in pharmacy queue | Nursing training on stat flag entry; phone call workflow retired |
| Order routing to satellite pharmacy | Paper or verbal routing based on pharmacist knowledge | Automated routing rules deliver orders to correct pharmacy queue by patient location | Routing rules must cover every patient care area — gaps cause misrouting | Build and test routing rules for every location, unit, and satellite pharmacy | Staff must understand orders route automatically — no manual handoff |
| Non-formulary drug request | Pharmacist contacts prescriber by phone; manual process | Non-formulary request workflow in Epic with electronic approval routing | Electronic approval workflow replaces phone-based process | Build non-formulary request and approval workflow | Prescribers and pharmacy must learn electronic approval process |

---

## Section 2 — Pharmacy verification

| Workflow | Current state | Epic future state | Gap | Analyst action | Org action |
|---|---|---|---|---|---|
| Drug-drug interaction checking | Manual review by pharmacist using clinical knowledge and reference tools | Epic CDS fires drug-drug interaction alerts at verification with severity ratings | CDS alerts must be calibrated — too many soft stops creates alert fatigue | Configure interaction alert severity levels; suppress low-clinical-value alerts | Pharmacist training on alert types and documentation requirements for overrides |
| Allergy cross-reactivity checking | Manual pharmacist review of allergy history | Epic CDS fires allergy alerts with cross-reactivity logic at order entry and verification | Cross-reactivity rules must reflect current clinical evidence | Build allergy CDS rules; validate against P&T committee-approved logic | Clinical informatics and pharmacy leadership must approve rule set before go-live |
| Renal dose adjustment | Pharmacist manually calculates dose based on lab values in separate system | Epic CDS fires renal dosing alert using live creatinine clearance calculated from current labs | Lab interface must be active and accurate for CDS to fire correctly | Build renal dosing CDS rules; validate lab interface feeds correct values | Pharmacy leadership validates dosing thresholds against institutional protocols |
| High-alert medication verification | Verbal or paper double-check by two pharmacists | Epic enforces two-pharmacist verification workflow for defined high-alert medications | High-alert medication list must be defined and built into Epic | Build two-pharmacist verification requirement for high-alert drug list | Pharmacy leadership defines and approves high-alert medication list |
| Pharmacist-to-prescriber communication | Phone call between pharmacist and prescriber | Electronic message sent from Willow verification screen directly to prescriber in Epic | Electronic messaging replaces most phone calls | Configure messaging routing from Willow to prescriber InBasket | Staff must understand when electronic messaging is appropriate vs. phone call |

---

## Section 3 — Dispensing and ADC

| Workflow | Current state | Epic future state | Gap | Analyst action | Org action |
|---|---|---|---|---|---|
| Medication delivery to nursing unit | Pharmacy delivers medications via pneumatic tube or runner on a schedule | Pharmacy-verified orders signal ADC immediately; nurse retrieves from cabinet | ADC cabinet profiles must be complete and accurate for every unit | Build ADC interface; configure cabinet profiles for all medications and locations | Nursing trained on retrieval workflow; pharmacy trained on replenishment process |
| ADC override for critical medications | Nurse calls pharmacy for override approval by phone | Override medication list configured in Epic — nurse can retrieve before verification with documentation | Override list must be clinically appropriate and compliance-approved | Build override medication list and documentation requirements | Pharmacy, nursing, and compliance leadership must approve override list |
| Controlled substance dispensing and reconciliation | Manual paper count and reconciliation at shift change | ADC records every controlled substance dispense; Epic generates reconciliation task at defined intervals | Reconciliation workflow must match state board of pharmacy requirements | Build controlled substance reconciliation intervals and escalation workflow | Staff trained on electronic reconciliation; policy updated to reflect Epic process |
| IV compounding and chemotherapy preparation | Paper or verbal order to IV room; manual label generation | Verified orders route to IV room workflow queue in Epic with label generation | Compounding workflow queue must be built and tested before go-live | Build IV room and chemo preparation workflow queues; configure label printing | IV room staff trained on Epic queue and label workflow |

---

## Section 4 — Nursing administration

| Workflow | Current state | Epic future state | Gap | Analyst action | Org action |
|---|---|---|---|---|---|
| Medication administration verification | Nurse manually verifies five rights using paper MAR | BCMA — nurse scans patient armband and medication barcode; Epic confirms match | Every dispensable medication must have correct NDC barcode mapping | Build and validate NDC mapping for entire formulary; configure BCMA mismatch alerts | Nursing trained on BCMA scanning process; handheld scanner hardware deployed |
| PRN medication documentation | Nurse documents on paper MAR with effectiveness noted in nurses notes | Epic eMAR requires PRN effectiveness documentation within configured time window | PRN effectiveness assessment must be built into eMAR workflow | Build PRN effectiveness documentation requirement and time window | Nursing trained on effectiveness documentation requirements |
| Late and missed dose management | Supervisor reviews paper MAR at end of shift for missed doses | Epic flags late and missed doses in real time; nurse must document reason | Missed dose reason codes must be meaningful and complete | Build missed dose reason code list; configure late administration time windows | Nursing leadership reviews and approves time windows and reason codes |

---

## Section 5 — Medication reconciliation

| Workflow | Current state | Epic future state | Gap | Analyst action | Org action |
|---|---|---|---|---|---|
| Admission medication reconciliation | Pharmacist or nurse calls patient or pharmacy to obtain home medication list; manual process | Epic medication reconciliation workflow compares home medication list to admission orders | Home medication data must be available in Epic before reconciliation can occur | Build admission reconciliation workflow; configure required documentation fields | Staff trained on reconciliation workflow; process for obtaining home med list defined |
| Transfer reconciliation | Verbal handoff between sending and receiving pharmacy or nursing staff | Epic transfer reconciliation workflow compares prior orders to new unit orders | Transfer workflow must fire automatically at every patient location change | Build transfer reconciliation trigger and workflow | Staff trained on transfer reconciliation requirement; completion tracked in Epic |
| Discharge reconciliation | Pharmacist manually compares inpatient orders to discharge prescriptions | Epic discharge reconciliation produces discharge medication list and routes to patient education | Discharge workflow must integrate with prescription routing and patient education build | Build discharge reconciliation workflow; configure patient education materials | Staff trained on discharge reconciliation; pharmacy involved in discharge workflow |

---

## Gap analysis summary

| Category | Total workflows analyzed | Requiring analyst build | Requiring org training | Requiring policy change |
|---|---|---|---|---|
| Order entry and routing | 4 | 4 | 4 | 2 |
| Pharmacy verification | 5 | 5 | 5 | 3 |
| Dispensing and ADC | 4 | 4 | 4 | 2 |
| Nursing administration | 3 | 3 | 3 | 1 |
| Medication reconciliation | 3 | 3 | 3 | 2 |
| **Total** | **19** | **19** | **19** | **10** |

---

*Document maintained by:* Kristina Ankrah, Healthcare IT Professional  
*Repository:* epic-willow-workflow-documentation  
*Last updated:* 2026
