# Requirements gathering guide — Epic Willow Inpatient pharmacy

This guide provides the interview framework, question sets, and documentation structure 
an Epic Willow analyst uses to gather requirements from pharmacy, nursing, and prescriber 
stakeholders before beginning system build.

---

## Purpose of requirements gathering

Before an analyst configures a single setting in Epic, they must understand how the 
organization actually operates — not how leadership thinks it operates, and not how a 
policy document says it should operate. Requirements gathering closes that gap.

The analyst's role in this process is to:
- Ask questions that reveal actual workflow, not idealized workflow
- Listen for workarounds — they reveal where the current system fails
- Probe for exceptions — edge cases become the hardest build problems
- Translate clinical answers into system requirements the build team can act on

---

## Who to interview

| Role | Why they matter | What they know that others don't |
|---|---|---|
| Staff pharmacist (inpatient) | Primary Willow end user | Daily verification pain points, alert fatigue, what information is missing at verification |
| Pharmacy technician | ADC and dispensing workflow expert | Dispensing workarounds, cabinet stocking problems, compounding workflow gaps |
| Pharmacy manager / director | Policy and compliance requirements | Approval thresholds, controlled substance protocols, regulatory requirements |
| Clinical pharmacist specialist | High-complexity medication expertise | TDM workflows, renal dosing protocols, high-alert medication requirements |
| Charge nurse / nurse manager | Nursing administration workflow | BCMA issues, ADC access problems, late dose workflow reality |
| Staff nurse (inpatient) | eMAR and BCMA end user | What actually happens at the bedside vs. what policy says happens |
| Prescriber / attending physician | CPOE and order set user | What order sets they actually use, what makes them bypass the formulary |
| Pharmacy informatics / IT | Current system configuration | What the current system does that Epic must replicate or improve |

---

## Interview framework

### Before the interview
- Review the current system configuration and any available workflow documentation
- Identify which workflows this stakeholder touches most directly
- Prepare role-specific questions from the sections below
- Schedule 60 minutes minimum — clinical staff rarely have more than 90

### During the interview
- Start with open-ended questions before specific ones
- When a workaround appears, stop and probe: *"Walk me through exactly what you do in that situation"*
- Ask about the worst day, not the average day: *"What's the scenario that causes the most problems?"*
- Confirm your understanding by summarizing back: *"So what I'm hearing is..."*

### After the interview
- Document requirements in the format: *"The system must [do X] when [condition Y] occurs"*
- Flag anything that requires clinical policy decision before build can proceed
- Identify conflicting requirements between stakeholder groups — these need resolution before build

---

## Question sets by role

---

### Pharmacy staff pharmacist

**Order entry and routing**
- When a STAT order comes in today, how do you know it's urgent? How is it different from 
  a routine order in your current system?
- Are there medications that should always go to a specific pharmacist or team? How is that 
  handled today?
- What happens when an order is sent to the wrong location or the wrong pharmacist?
- How do you handle orders that come in after satellite pharmacy hours?

**Clinical verification**
- What clinical information do you need to see when verifying a medication order? What 
  information are you currently missing or have to look up in a separate system?
- Which drug-drug interaction alerts do you find useful? Which ones do you click through 
  without reading?
- How do you handle a weight-based dose that needs to be calculated — what's your process today?
- What are the high-alert medications at this institution? What extra steps do you take for those?
- When you need to contact the prescriber about an order, how do you do it today? How long 
  does it typically take to get a response?

**Controlled substances**
- Walk me through your current controlled substance reconciliation process. How often does 
  it happen? Who is responsible?
- What happens when there is a discrepancy? What is the escalation path?
- How are controlled substance overrides handled today? What documentation is required?

**Pain points**
- What is the single biggest problem with your current medication order workflow?
- What workarounds do you use regularly that you wish you didn't have to?
- What would make the biggest positive difference to your daily work?

---

### Pharmacy technician

**ADC and dispensing**
- Which medications do nurses most frequently call about not being able to find in the cabinet?
- How often do nurses use the override function? For which medications?
- What is your current process for restocking cabinets? How do you know what needs to be 
  restocked and when?
- What happens when a medication isn't in the cabinet and a nurse needs it urgently?

**IV room and compounding**
- Walk me through how a compounded IV order reaches the IV room today. From pharmacist 
  approval to finished product — what are the steps?
- How are chemotherapy orders handled differently from standard IV admixtures?
- How do you track what has been compounded and what is waiting to be compounded?
- What labeling information is required on every compounded product?

**Controlled substances**
- Walk me through your shift-change controlled substance count. What system do you use today?
- What happens when the count doesn't match? What documentation is required?

---

### Pharmacy manager / director

**Policy and compliance**
- What medications require a prescriber to have special authorization before ordering? 
  How is that authorization tracked today?
- What are your state board of pharmacy requirements for controlled substance reconciliation 
  frequency and documentation?
- Which medications require pharmacist-to-pharmacist verification before dispensing? 
  What is your current process for that?
- Are there any medications that require a clinical pharmacology or specialist consult 
  before the order can be processed? How is that triggered today?

**Formulary and non-formulary**
- How does a prescriber request a non-formulary medication today? What is the approval process?
- Who has authority to approve non-formulary requests? Is it role-based or individual?
- How are formulary exceptions for specific patient populations handled — for example, 
  a patient on a home medication that is not on your formulary?

**Reporting and compliance**
- What medication-related reports do you currently run regularly? What decisions do they inform?
- What regulatory measures related to medications does your organization report on?
- Are there any Joint Commission or state survey findings related to medication management 
  that the Epic build needs to address?

---

### Staff nurse

**eMAR and administration**
- When you go to administer a medication, what information do you need to see? Is everything 
  you need visible in your current system, or do you have to look elsewhere?
- Have you ever had a situation where you couldn't administer a medication because of a 
  system problem? What happened?
- How do you handle a PRN medication? What documentation do you do today?
- What happens when a medication is late or missed? What is your current process for 
  documenting that?

**ADC and retrieval**
- Are there medications that you frequently can't find in the cabinet when you need them?
- How do you handle an override situation today? When is it appropriate to override?
- What happens when a medication is not available in the cabinet and you need it for a 
  time-sensitive administration?

**BCMA**
- Do you currently use barcode scanning for medication administration? If so, what problems 
  do you encounter most frequently?
- Are there medications or situations where scanning is difficult or not possible? How do 
  you document those?

---

### Prescriber / attending physician

**Order entry**
- How do you currently enter medication orders? What system or process do you use?
- Are there specific medication orders you place frequently where you have a preferred dose, 
  route, and frequency? Would a pre-built order set be helpful?
- When you need information about a medication while ordering — interactions, dosing, 
  alternatives — where do you look today?

**Alerts and CDS**
- When your ordering system generates a warning or alert, do you find them useful? 
  Which ones do you pay attention to? Which ones do you typically bypass?
- Have you ever ordered a medication and been stopped by an alert that you felt was 
  clinically incorrect or unnecessary? Can you give an example?

**Communication with pharmacy**
- When pharmacy contacts you about an order — dose change, interaction concern, 
  non-formulary alternative — how do they reach you today? How quickly do you typically respond?
- What would make it easier for you to respond to pharmacy concerns about your orders?

---

## Requirements documentation template

Use this format to capture each requirement identified during interviews:

```
REQUIREMENT ID: WIL-[number]
Source: [stakeholder role and interview date]
Workflow area: [order entry / routing / verification / dispensing / administration / reconciliation]
Requirement: The system must [action] when [condition].
Priority: [High / Medium / Low]
Decision needed: [Yes / No — if Yes, describe what decision must be made before build]
Build owner: [Analyst name or TBD]
Status: [Open / In build / Complete / Deferred]
```

**Example:**
```
REQUIREMENT ID: WIL-014
Source: Staff pharmacist interview, 2026-04-15
Workflow area: Verification
Requirement: The system must fire a HIGH severity hard stop alert when vancomycin is ordered 
for any patient with serum creatinine greater than 1.5 mg/dL, requiring pharmacist 
documentation of dose adjustment rationale or clinical override justification before the 
order can be verified and released.
Priority: High
Decision needed: Yes — pharmacy leadership must confirm the 1.5 mg/dL threshold and 
approve the list of acceptable override justification options
Build owner: TBD
Status: Open
```

---

*Document maintained by:* Kristina Ankrah, Healthcare IT Professional  
*Repository:* epic-willow-workflow-documentation  
*Last updated:* 2026
