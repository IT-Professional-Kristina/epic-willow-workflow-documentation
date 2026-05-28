# Inpatient medication order lifecycle — Epic Willow analyst documentation

This document describes the complete inpatient medication lifecycle from prescriber order 
entry through nursing administration and reconciliation. Each stage includes workflow 
narrative, Epic Willow system behavior, and analyst build considerations.

---

## Overview

The inpatient medication lifecycle spans six sequential stages. Every stage involves at 
least one clinical role, one Epic module, and a set of system behaviors that the analyst 
is responsible for configuring, testing, and maintaining.

```
Prescriber → CPOE Order Entry
     ↓
Epic → Order Routing
     ↓
Pharmacist → Clinical Verification (Willow)
     ↓
Pharmacy → Dispensing and ADC Load
     ↓
Nurse → Retrieval, BCMA Scan, Administration
     ↓
Epic → eMAR Documentation and Reconciliation
```

---

## Stage 1 — Prescriber order entry (CPOE)

### What happens
The prescriber enters a medication order in Epic using the Order Composer. They may select 
from an order set, search the formulary directly, or use a preference list. As the order 
is built, Epic's Clinical Decision Support engine evaluates the order against the patient's 
allergy list, current medication profile, renal function, weight, and diagnosis.

### Epic system behavior
- Formulary search returns only medications on the approved drug catalog
- Order sets present pre-configured medication groupings with default doses and frequencies
- CDS rules fire alerts — hard stops or soft stops — based on analyst-configured logic
- Ordering provider must acknowledge or resolve all hard stop alerts before signing

### Analyst build considerations
- Formulary catalog must reflect current P&T committee approvals
- Order sets require clinical validation before activation
- CDS rule severity (hard vs. soft stop) must be calibrated to avoid alert fatigue
- Default doses, routes, and frequencies must be appropriate for the patient population
- Restricted medications require build of prescriber authorization logic

---

## Stage 2 — Order routing

### What happens
After the prescriber signs the order, Epic evaluates the order against routing rules and 
delivers it to the appropriate pharmacy queue. The correct pharmacist worklist receives 
the order within seconds of signature.

### Epic system behavior
- Routing rules evaluate patient location, medication class, order priority, and care area
- STAT orders surface at the top of the pharmacy queue with visual priority indicators
- Orders for satellite pharmacies (ICU, ED, oncology) route independently of central pharmacy
- Unrouted or misrouted orders generate system alerts for analyst follow-up

### Analyst build considerations
- Every patient care area must have a defined routing rule — no location can be unassigned
- Satellite pharmacy coverage hours must be reflected in routing logic
- STAT, urgent, and routine priority levels must route and display differently
- Routing rules must be tested for every care area, shift, and medication class combination
- Order routing failures are among the highest-impact go-live issues — test exhaustively

---

## Stage 3 — Pharmacy clinical verification (Willow)

### What happens
The pharmacist opens the order in the Willow pharmacy queue and performs clinical review. 
They verify that the medication, dose, route, frequency, and duration are appropriate for 
this specific patient given their current clinical status. The pharmacist may approve, 
modify, place on hold, or reject the order back to the prescriber.

### Epic system behavior
- Willow displays patient allergies, current medications, labs, and vitals alongside the order
- CDS alerts fire at verification if not already resolved at order entry
- Pharmacist can send an electronic message to the prescriber directly from the verification screen
- Approved orders generate a medication label and signal the ADC for dispensing
- Rejected orders route back to the prescriber with pharmacist comments

### Analyst build considerations
- Pharmacist-facing CDS rules may differ from prescriber-facing rules in severity and content
- Verification screens must display the right patient data without requiring navigation away
- Label print groups must be configured for each dispensing location
- High-alert medication workflows (chemotherapy, anticoagulants, concentrated electrolytes) 
  require additional verification steps built by the analyst
- Pharmacokinetics consultation workflows must integrate with Willow verification

---

## Stage 4 — Dispensing and ADC integration

### What happens
After verification, pharmacy prepares the medication for delivery to the patient care area. 
For unit-dosed and pre-packaged medications, Epic signals the ADC (Pyxis, Omnicell, or 
equivalent) that the medication is available for retrieval. For compounded medications — 
IV admixtures, chemotherapy, total parenteral nutrition — the dispensing workflow routes 
to the appropriate compounding area.

### Epic system behavior
- ADC interface receives approved medication data including drug, dose, patient, and location
- Cabinet profile determines which pocket the medication is assigned to in the ADC
- Override logic allows nurse retrieval of critical medications before pharmacy verification 
  in defined emergency scenarios, with documentation requirements
- Controlled substance dispenses generate a reconciliation task at a configurable interval
- Compounding orders route to the IV room or chemotherapy hood workflow queue

### Analyst build considerations
- ADC cabinet profiles must be built and maintained for every cabinet in every unit
- Override medication lists require clinical and compliance review before activation
- Controlled substance reconciliation intervals must align with state board of pharmacy requirements
- Pyxis and Omnicell integration requires interface configuration beyond Epic build alone
- Compounding workflow must reflect USP 795, 797, and 800 compliance requirements

---

## Stage 5 — Nursing administration and BCMA

### What happens
The nurse retrieves the medication from the ADC, performs the five rights verification 
(right patient, drug, dose, route, time), scans the patient's armband barcode and the 
medication barcode using a handheld scanner, and administers the medication. Administration 
is documented in the eMAR in real time.

### Epic system behavior
- BCMA scanner reads the patient identification barcode and matches it to the active order
- Medication barcode is scanned and matched to the verified, dispensed medication
- Mismatches trigger an alert — the nurse cannot document administration without resolution
- eMAR records time of administration, dose given, route, site, and administering nurse
- Late administration flags fire when documentation occurs outside the configured time window
- Missed dose documentation requires a reason code selected from an analyst-configured list

### Analyst build considerations
- BCMA requires accurate NDC (National Drug Code) mapping for every dispensable medication
- Time window configuration for administration (acceptable early/late range) requires 
  clinical input and must balance safety with nursing workflow reality
- Missed dose reason codes must be meaningful and reflect actual clinical scenarios
- PRN medication documentation must require effectiveness assessment documentation
- High-alert medication administration must require two-nurse verification build

---

## Stage 6 — Reconciliation and monitoring

### What happens
Throughout the patient's stay and at every transition of care, medications are reconciled 
to identify discrepancies, omissions, and therapy changes. Therapeutic drug monitoring 
(TDM) workflows flag when levels are due or results are critical. At discharge, 
inpatient medications are reconciled against discharge prescriptions.

### Epic system behavior
- Medication reconciliation workflows fire at admission, transfer, and discharge
- TDM workflows generate pharmacy tasks when monitoring labs are resulted
- Controlled substance reconciliation compares ADC dispense records against eMAR 
  administration documentation on a scheduled basis
- Discharge medication reconciliation produces the discharge medication list and 
  patient education materials
- Unreconciled discrepancies generate outstanding tasks for the responsible clinician

### Analyst build considerations
- Reconciliation workflows must be built for every transition type the health system uses
- TDM thresholds and monitoring intervals must reflect current pharmacokinetic guidelines
- Controlled substance reconciliation discrepancy workflows must include escalation paths 
  to pharmacy management and compliance
- Discharge reconciliation must integrate with patient education and prescription routing
- Medication reconciliation completion rates are a Joint Commission measure — build must 
  support documentation that is both complete and clinically meaningful

---

## Summary — analyst accountability by stage

| Stage | Clinical Role | Epic Module | Analyst Build Scope |
|---|---|---|---|
| Order entry | Prescriber | CPOE / Order Composer | Formulary, order sets, CDS rules |
| Order routing | System | Willow routing engine | Routing rules, queue setup |
| Verification | Pharmacist | Willow Inpatient | Verification screens, labels, CDS |
| Dispensing | Pharmacist / Tech | Willow + ADC interface | Cabinet profiles, override logic, compounding |
| Administration | Nurse | eMAR / BCMA | Time windows, reason codes, two-nurse verify |
| Reconciliation | Pharmacist / Team | Willow + Care Everywhere | Reconciliation workflows, TDM, discharge |

---

*Document maintained by:* Kristina Ankrah, Healthcare IT Professional  
*Repository:* epic-willow-workflow-documentation  
*Last updated:* 2026
