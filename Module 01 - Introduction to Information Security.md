# Module 01 — Introduction to Information Security (Exam Prep Notes)

## 1) What “Information Security” means
**Information Security (InfoSec)** is protecting information and the systems that store/process/transmit it.

You’ll see two related terms:
- **Information Security**: protects information in any form (digital + paper + verbal).
- **Cybersecurity**: focuses mainly on digital systems and networks.

---

## 2) The CIA Triad (must-know)
### 2.1 Confidentiality
Prevent unauthorized disclosure of information.
- Examples: encryption, access control, data classification.

### 2.2 Integrity
Prevent or detect unauthorized modification.
- Examples: hashes, digital signatures, checksums, access control, change management.

### 2.3 Availability
Ensure systems/data are accessible when needed.
- Examples: redundancy, backups, DR plans, load balancing, DDoS protection.

**Exam trick:** A control can support multiple CIA goals.

### CIA quick table (memorize)
| Goal | What it prevents | Fast examples | Common exam keywords |
|---|---|---|---|
| Confidentiality | Data leaks | Encryption, access control, data masking | “unauthorized disclosure”, “privacy” |
| Integrity | Unauthorized change | Hash/MAC, digital signatures, change control | “tampering”, “modified”, “trustworthy” |
| Availability | Downtime | Backups, redundancy, DR, DDoS protection | “outage”, “uptime”, “resilience” |

### Mini-figure: CIA as a triangle (think “balance”)
```
				Confidentiality
						 /\
						/  \
					 /____\
	Integrity      Availability
```

---

## 2.4) How to answer CIA questions (step-by-step)
When an exam scenario describes a problem, do this:
1) Identify what happened: leak? change? downtime?
2) Map to CIA: leak→C, change→I, downtime→A.
3) Name 1–2 best controls that directly address it.
4) If multiple apply, pick the *most direct* one.

## 3) Core security concepts
### 3.1 Asset, threat, vulnerability, risk
- **Asset**: something valuable (data, server, reputation).
- **Threat**: something that can cause harm (attacker, fire, malware).
- **Vulnerability**: weakness that a threat can exploit (unpatched software, weak passwords).
- **Risk**: probability and impact of a threat exploiting a vulnerability.

A common way to express risk:
$$\text{Risk} \approx \text{Likelihood} \times \text{Impact}$$

### 3.2 Exposure
The extent to which an asset is vulnerable to loss/damage.

### 3.3 Control (countermeasure)
Anything that reduces risk (policy, firewall, MFA, training).

---

## 3.4) Quick risk identification template (step-by-step)
Use this template on scenario questions:
1) **Asset:** what’s valuable?
2) **Threat:** what could cause harm?
3) **Vulnerability:** what weakness exists?
4) **Impact:** what happens if exploited?
5) **Likelihood:** how likely is exploitation?
6) **Control:** what reduces likelihood/impact?

### Mini-figure: how risk forms
```
Threat + Vulnerability  --->  Incident  --->  Impact
		  (weakness)
```

## 4) Types of security controls (very exam-friendly)
### 4.1 By purpose
- **Preventive**: stops an incident (MFA, firewalls, least privilege).
- **Detective**: detects incidents (IDS, logs, monitoring).
- **Corrective**: fixes after incident (patching, restoration).
- **Deterrent**: discourages (warning banners, visible cameras).
- **Compensating**: alternative control if primary isn’t possible.

### 4.2 By implementation
- **Administrative**: policies, procedures, awareness training.
- **Technical (logical)**: access control, encryption, IDS.
- **Physical**: locks, guards, CCTV, mantraps.

---

## 4.3) Control cheat-sheet table
| Control type | Purpose | Quick example | Typical exam clue |
|---|---|---|---|
| Preventive | Stop it | MFA, firewall rules, least privilege | “prevent”, “block” |
| Detective | Find it | IDS, logs, SIEM alerts | “detect”, “monitor” |
| Corrective | Fix it | restore backups, patch after incident | “recover”, “remediate” |
| Deterrent | Discourage | warning signs, visible cameras | “discourage” |
| Compensating | Substitute | extra monitoring when MFA unavailable | “alternative control” |

## 5) Security principles you should be able to explain
- **Least privilege**: give only the access needed.
- **Need to know**: access to specific information only when required.
- **Separation of duties**: split critical tasks among multiple people.
- **Defense in depth**: layered controls so one failure doesn’t break everything.
- **Fail-safe defaults**: default deny.
- **Complete mediation**: check access every time.
- **Economy of mechanism**: keep security design simple.

---

## 5.1) Memorization tip: “LSD-DCFCE”
Use this as a checklist:
- **L**east privilege
- **S**eparation of duties
- **D**efense in depth
- **D**eny by default (fail-safe defaults)
- **C**omplete mediation
- **F**it-for-purpose simplicity (economy of mechanism)
- **C**ontrol access (need to know)
- **E**very layer counts

## 6) Authentication vs authorization vs accounting (AAA)
- **Authentication**: “Who are you?” (password, biometrics, MFA)
- **Authorization**: “What can you do?” (permissions, roles)
- **Accounting (auditing)**: “What did you do?” (logs, audit trails)

---

## 7) Threat actors (typical exam list)
- Script kiddies
- Cybercriminals
- Insiders (malicious or careless)
- Hacktivists
- Nation-state/APT

---

## 8) Security governance basics
### 8.1 Policies, standards, procedures, guidelines
- **Policy**: high-level rule/intent (mandatory).
- **Standard**: specific requirement to meet policy (mandatory).
- **Procedure**: step-by-step instructions (mandatory).
- **Guideline**: recommended best practice (optional).

### 8.2 Data classification (concept)
Typical levels: Public → Internal → Confidential → Restricted.
Higher sensitivity ⇒ stronger controls.

---

## 9) Solved examples (exam-style)

### Example 1: Identify asset/threat/vulnerability/risk/control
Scenario: A company stores customer data on a server. The server is missing security patches.
- Asset: customer data + server.
- Threat: attacker exploiting known vulnerability.
- Vulnerability: unpatched OS/app.
- Risk: data breach (likelihood high, impact high).
- Controls: patch management, vulnerability scanning, network segmentation, monitoring.

### Example 2: Control classification
“MFA on VPN login” is:
- Preventive (purpose)
- Technical/logical (implementation)

“CCTV in server room” is:
- Detective (purpose)
- Physical (implementation)

### Example 3: Map a scenario to CIA + control
Scenario: A database record was changed without approval.
- CIA impact: **Integrity**
- Best controls: least privilege + audit logs + change management + approvals

### Example 4: Administrative vs technical vs physical
Scenario: A company publishes an “Acceptable Use Policy”.
- Type: **Administrative** control
Scenario: Disk encryption on laptops.
- Type: **Technical** control
Scenario: Badge access to server room.
- Type: **Physical** control

---

## 10) Numericals (solved drills)

### Quick formulas (very common)
- **Risk (simple)**: $Risk \approx Likelihood \times Impact$
- **SLE (Single Loss Expectancy)**: $SLE = AV \times EF$
- **ALE (Annualized Loss Expectancy)**: $ALE = SLE \times ARO$

Where:
- $AV$ = Asset Value
- $EF$ = Exposure Factor (fraction lost, e.g., 0.25 means 25%)
- $ARO$ = Annual Rate of Occurrence (times per year)

### N1) Compute SLE and ALE
Asset value $AV=\$200{,}000$.
Exposure factor $EF=0.30$ (30% loss per incident).
ARO = 0.5 (once every 2 years).

1) $SLE=200{,}000\times 0.30=\$60{,}000$
2) $ALE=60{,}000\times 0.5=\$30{,}000$ per year

### N2) Decide if a control is worth it (simple exam style)
Using N1, current $ALE=\$30{,}000$/year.
A new control costs $\$8{,}000$/year and reduces ARO from 0.5 to 0.1.

New ALE:
- $SLE$ same = $\$60{,}000$
- $ALE_{new}=60{,}000\times 0.1=\$6{,}000$/year

Annual benefit (risk reduction) ≈ $30{,}000 - 6{,}000 = \$24{,}000$.
Net gain after control cost ≈ $24{,}000 - 8{,}000 = \$16{,}000$.

Conclusion: control is cost-justified (in simple quantitative terms).

### N3) Map a scenario to CIA quickly (scoring idea)
If an exam gives Likelihood (1–5) and Impact (1–5), compute:
$$Score = Likelihood\times Impact$$
Example: Likelihood=4, Impact=5 → Score=20 (very high priority).

---

## 11) Practice questions (with solutions)

### Q1) Define vulnerability in one line.
**Answer:** A weakness that can be exploited by a threat.

### Q2) Which CIA goal is most directly impacted by a DDoS attack?
**Answer:** Availability.

### Q3) Least privilege mainly supports which CIA goal?
**Answer:** Confidentiality and integrity (also reduces availability risks from misuse).

### Q4) What’s the difference between a policy and a procedure?
**Answer:** Policy states what must be done; procedure explains how to do it.

### Q5) A firewall rule blocks inbound traffic from the internet. What control type is it (purpose + implementation)?
**Answer:** Preventive + Technical.

### Q6) Security camera footage helps identify who entered the server room. What CIA goal does it most directly support?
**Answer:** Integrity (accountability) and also deterrence/detection.

### Q7) Give one example of separation of duties.
**Answer:** One person requests a payment; another approves it.

### Q8) What is the easiest “first step” when answering asset/threat/vulnerability questions?
**Answer:** Identify the asset first (what you’re protecting).

---

## 12) Exam checklist (Module 01)
- CIA mapping + best controls.
- Asset/threat/vulnerability/risk template.
- Control categories (preventive/detective/corrective + admin/technical/physical).
- Risk numericals: SLE/ALE and simple scoring.

## 11) How to memorize Module 01 fast (study method)
Use active recall instead of re-reading:
1) Turn the CIA table into flashcards (Goal → definition → 2 examples).
2) Practice 10 scenarios: write **Asset/Threat/Vuln/Control** in 30 seconds each.
3) Repeat after 1 day and 3 days (spaced repetition).

## 12) Exam checklist (Module 01)
- CIA triad definitions + examples.
- Asset/threat/vulnerability/risk/control.
- Control categories (preventive/detective/etc + administrative/technical/physical).
- AAA terms.
- Security principles (least privilege, defense in depth, separation of duties).
