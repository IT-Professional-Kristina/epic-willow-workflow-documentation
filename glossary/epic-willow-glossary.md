# Epic Willow glossary — key terms for inpatient pharmacy analysts

This glossary defines core Epic Willow concepts from both the clinical and analyst perspective. 
Written to support implementation, build, and go-live activities for Epic Willow Inpatient.

---

### CPOE — Computerized Physician Order Entry

**Definition:** The system through which prescribers enter medication orders directly into Epic, 
replacing verbal, telephone, and handwritten orders.

**In Epic Willow:** Orders entered via CPOE route automatically to the pharmacy Willow queue 
based on order routing rules configured by the analyst. Department setup, order priority flags, 
and routing logic determine which pharmacist queue receives the order and at what priority level.

**Clinical context:** Every inpatient medication order begins here. The analyst builds what the 
prescriber sees at order entry — order sets, preference lists, default doses, and the CDS rules 
that fire before the order is signed.

---

### CDS — Clinical Decision Support

**Definition:** Automated alerts and logic built into Epic that fire when a clinical condition 
is met, prompting the user to review, acknowledge, or act before proceeding.

**In Epic Willow:** CDS rules are configured by the analyst and fire at two points — at order 
entry (prescriber-facing) and at pharmacy verification (pharmacist-facing). Common rule types 
include drug-drug interaction alerts, allergy cross-reactivity checks, dose range warnings, 
renal dosing flags, and weight-based dosing calculations.

**Hard stop vs. soft stop:**
- **Hard stop:** The user cannot proceed without taking a required action — documenting a 
  rationale, modifying the order, or contacting the prescriber. Used for high-severity alerts 
  such as contraindicated drug combinations or critical allergy conflicts.
- **Soft stop:** An advisory alert the user can acknowledge and bypass with a single click. 
  Used for lower-severity warnings where clinical judgment may override the alert. Overuse 
  of soft stops leads to alert fatigue — a key analyst calibration challenge.

**Clinical context:** As a pharmacy technician and pharmacist-support staff, these alerts 
appeared during verification. The analyst decides which alerts are hard stops, which are soft 
stops, and which are suppressed entirely to balance patient safety with workflow efficiency.

---

### eMAR — Electronic Medication Administration Record

**Definition:** The digital record within Epic where nurses document every medication 
administration — time given, dose, route, site, and any clinical observations at the 
time of administration.

**In Epic Willow:** The eMAR is the downstream endpoint of the pharmacy workflow. After a 
pharmacist verifies an order and the medication is dispensed to the ADC, the nurse retrieves 
it and documents administration in the eMAR. The analyst's Willow build determines what 
information is required at documentation, what triggers a late administration flag, and how 
missed doses are tracked and escalated.

**Clinical context:** From the pharmacy side, the eMAR is where medication administration 
evidence lives. Discrepancies between what pharmacy dispensed and what nursing documented 
are surfaced here — a key data source for controlled substance reconciliation.

---

### BCMA — Barcode Medication Administration

**Definition:** A safety verification process in which the nurse scans the patient's 
identification barcode and the medication barcode at the point of administration to confirm 
the five rights: right patient, right drug, right dose, right route, right time.

**In Epic Willow:** BCMA is integrated with the eMAR. A mismatch between the scanned 
medication and the ordered medication triggers an alert before administration can be 
documented. The analyst configures what mismatches generate hard stops versus warnings, 
and which medications are exempt from BCMA scanning requirements.

**Clinical context:** BCMA is a front-line safety net that catches dispensing and administration 
errors. The pharmacy analyst's build directly affects what the nurse sees when they scan — 
incorrect NDC mapping or formulary setup causes BCMA failures at the bedside.

---

### ADC — Automated Dispensing Cabinet

**Definition:** A secured, automated medication storage and dispensing unit located in or 
near patient care areas — most commonly Pyxis (BD) or Omnicell — that controls access to 
medications and tracks every dispense, return, and waste event.

**In Epic Willow:** ADC integration is configured by the analyst. After pharmacy verifies an 
order, Epic signals the ADC that the medication is available for retrieval. Cabinet profiling 
(which medications are stocked in which cabinet pockets), override logic, and controlled 
substance reconciliation workflows are all part of the Willow analyst's build scope.

**Clinical context:** Pyxis, Omnicell, Swisslog, and ScriptPro are the most common systems. 
Every medication retrieval, override, and waste creates an event log that flows back into 
Epic — the analyst ensures that data is captured correctly and that reconciliation workflows 
fire on schedule.

---

### Pharmacy queue

**Definition:** The worklist within Epic Willow where medication orders appear for pharmacist 
review after CPOE entry. Each order displays patient information, the ordered medication, 
prescriber, priority, and any active CDS alerts.

**In Epic Willow:** The analyst configures routing rules that determine which queue an order 
lands in — ICU pharmacy queue, oncology pharmacy queue, central pharmacy, or ED pharmacy — 
based on patient location, order type, medication class, or priority flag. Queue management 
is one of the most operationally critical areas of Willow build.

**Clinical context:** A misrouted order — an ICU stat medication landing in the central 
pharmacy queue — directly delays patient care. The analyst's routing logic must account for 
every care area, every satellite pharmacy, and every exception scenario the health system operates.

---

### Formulary

**Definition:** The approved list of medications a health system has authorized for 
prescribing, dispensing, and administration within its facilities.

**In Epic Willow:** The formulary is built and maintained by the analyst in coordination 
with pharmacy leadership. It controls which medications can be ordered via CPOE, how they 
appear in the prescriber's order search results, and which alternatives are suggested when 
a non-formulary drug is requested. The formulary is the foundation of the entire Willow 
medication catalog.

**Clinical context:** Formulary management decisions — which drugs are preferred agents, 
which require prior authorization, which are restricted to specific prescribers — directly 
affect patient care and institutional cost. The analyst translates these decisions into 
system configuration.

---

### Order set

**Definition:** A pre-built collection of orders — medications, labs, nursing tasks, diet 
orders — grouped together for a specific clinical scenario, allowing a prescriber to place 
multiple related orders simultaneously with a single selection.

**In Epic Willow:** Order sets are built and maintained by the analyst in collaboration 
with clinical informatics, pharmacy, and physician leadership. A vancomycin order set, for 
example, would include the vancomycin order with weight-based dosing guidance, a baseline 
serum creatinine lab order, a trough level order, and a pharmacokinetics consult task — 
all placed together at initiation.

**Clinical context:** Well-built order sets reduce prescriber cognitive load and standardize 
care. Poorly built order sets cause alert fatigue, workarounds, and clinical variation. 
The analyst is responsible for both the technical build and the clinical accuracy of every 
order set in scope.

---

### Medication reconciliation

**Definition:** The process of comparing a patient's current medication list against newly 
ordered medications to identify and resolve discrepancies — omissions, duplications, dosing 
conflicts, or contraindications — at every transition of care.

**In Epic Willow:** Medication reconciliation workflows are configured by the analyst for 
three transition points: admission (comparing home medications to inpatient orders), 
transfer (comparing prior unit orders to new unit orders), and discharge (comparing inpatient 
orders to discharge prescriptions). The analyst builds the workflow, the required 
documentation fields, and the escalation logic when reconciliation is incomplete.

**Clinical context:** Medication reconciliation errors are among the leading causes of 
preventable adverse drug events. The analyst's build determines how visible discrepancies 
are to clinicians and how hard the system makes it to proceed without resolving them.

---

### Epic build

**Definition:** The process of configuring Epic software to match the workflows, policies, 
and operational requirements of a specific health system. Build is the core technical 
responsibility of an Epic analyst.

**In Epic Willow:** Build encompasses formulary setup, order routing, CDS rule creation, 
ADC integration, department and location configuration, pharmacy queue design, print group 
setup, dispense preparation workflow, controlled substance tracking, and all associated 
reporting. Every configuration decision is documented, tested, and validated before go-live.

**Clinical context:** The difference between a well-configured and a poorly configured Epic 
environment is felt by every pharmacist, nurse, and prescriber on day one of go-live — and 
every day after. The analyst's build decisions are the difference between a system that 
supports clinical work and one that creates barriers to it.

---

*Glossary maintained by:* Kristina Ankrah, Healthcare IT Professional  
*Repository:* epic-willow-workflow-documentation  
*Last updated:* 2026
