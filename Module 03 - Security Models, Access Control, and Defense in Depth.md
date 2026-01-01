# Module 03 — Security Models, Access Control, and Defense in Depth (Exam Prep Notes)

## 1) Access control fundamentals
Access control answers: **who** can access **what** and **how**.

Core terms:
- **Subject**: active entity (user/process).
- **Object**: resource (file, database row, server).
- **Access**: read/write/execute/delete.

---

## 2) Identification, Authentication, Authorization
- **Identification**: claim an identity (username, ID number).
- **Authentication**: prove the claim.
- **Authorization**: permissions after authentication.

---

## 3) Authentication factors (common exam list)
- Something you **know**: password, PIN
- Something you **have**: token, smart card
- Something you **are**: biometrics
- Somewhere you **are**: location
- Something you **do**: behavior/keystrokes

**MFA** uses 2+ different factor types (not just two passwords).

---

## 4) Authorization models
### 4.1 DAC (Discretionary Access Control)
Owner controls access.
- Example: file owner sharing permissions.

### 4.2 MAC (Mandatory Access Control)
Central authority enforces labels/classification.
- Example: military classification (Top Secret, Secret).

### 4.3 RBAC (Role-Based Access Control)
Permissions assigned to roles; users get roles.
- Example: “HR role”, “Finance role”.

### 4.4 ABAC (Attribute-Based Access Control)
Policy decisions based on attributes (user, resource, environment).
- Example: allow if Department=Finance AND Device=Compliant AND Time=BusinessHours.

### Quick comparison table (memorize)
| Model | Who decides? | Best for | Typical exam clue |
|---|---|---|---|
| DAC | Owner | small/medium, file sharing | “owner grants permission” |
| MAC | Central authority | high security/classification | “labels/clearance” |
| RBAC | Role definitions | enterprises | “job role” |
| ABAC | Policy engine | complex rules | “attributes/time/device/location” |

---

## 5) Access control mechanisms (implementation)
- **ACL (Access Control List)**: list of permissions attached to an object.
- **Capability list**: permissions attached to a subject.
- **Permissions**: allow/deny rules.

---

## 6) Security models (conceptual)
### 6.1 Bell–LaPadula (confidentiality-focused)
Rules:
- **No read up** (simple security property)
- **No write down** (*-property)

Meaning: protect secrets from leaking to lower classifications.

Mini-figure (think “read up is blocked”):
```
Top Secret
	^   (no read up)
Secret
	v   (no write down)
Confidential
```

### 6.2 Biba (integrity-focused)
Rules:
- **No read down**
- **No write up**

Meaning: protect high-integrity data from being contaminated by low-integrity sources.

Mini-figure (opposite of Bell–LaPadula):
```
High Integrity
	^   (no write up)
Medium
	v   (no read down)
Low Integrity
```

### 6.3 Clark–Wilson (integrity via well-formed transactions)
Focus on:
- Separation of duties
- Controlled processes (only specific programs can modify data)

**Exam tip:** If question mentions “confidentiality classification” → Bell–LaPadula. If it mentions “integrity levels” → Biba/Clark–Wilson.

---

## 7) Defense in depth
Use multiple layers so one failure doesn’t compromise everything.

Examples of layers:
- Physical security (locks)
- Network security (firewalls, segmentation)
- Host security (patching, EDR)
- Application security (input validation)
- Data security (encryption)
- Monitoring (logs/SIEM)

### Step-by-step: how to answer “which model?” questions
1) If it mentions **classification/clearance** → MAC + Bell–LaPadula.
2) If it mentions **data trustworthiness / contamination** → Biba/Clark–Wilson.
3) If it mentions **job functions** → RBAC.
4) If it mentions **many conditions (time/device/location)** → ABAC.

### Step-by-step: how to answer “defense in depth” questions
List at least 3 layers:
1) Network (segmentation, firewall)
2) Host (patching, EDR)
3) Data (encryption, backups)

---

## 8) Least privilege and privilege management
- Give minimum permissions required.
- Use admin accounts only when needed.
- Prefer “just-in-time” privileges where possible.

---

## 9) Solved examples

### Example 1: Identify control model
Scenario: Employees are assigned “Cashier”, “Manager”, “Auditor” roles. Access depends on role.
**Answer:** RBAC.

### Example 2: Bell–LaPadula decision
User clearance = Secret. File classification = Top Secret.
Can user read the file?
- Bell–LaPadula: “No read up” ⇒ Secret cannot read Top Secret.
**Answer:** No.

Can user write to a Confidential file?
- “No write down” ⇒ Secret cannot write down to Confidential.
**Answer:** No.

### Example 3: Separation of duties
Requirement: One employee requests vendor payment; a second employee approves it.
**Answer:** Separation of duties (helps prevent fraud).

---

## 10) Logic drills (solved, exam-style)

### L1) Bell–LaPadula quick decisions
Clearance levels: Confidential < Secret < Top Secret.

User is **Secret**.
1) Read Confidential? Yes (not reading up).
2) Read Top Secret? No (no read up).
3) Write Confidential? No (no write down).
4) Write Top Secret? Yes (writing up is allowed).

### L2) Biba quick decisions
Integrity levels: Low < Medium < High.

Process is **High integrity**.
1) Read Low input? No (no read down).
2) Write to Low object? Yes (writing down is allowed).
3) Write to High object from Low process? No (no write up for low).

### L3) RBAC mapping (mini “numerical”)
If there are 4 roles and each user gets exactly 1 role:
- 20 users → 20 role assignments
If each user can have up to 2 roles:
- maximum assignments = $20\times 2 = 40$

---

## 11) Practice questions (with solutions)

### Q1) Which access control model is best for large organizations where job functions define permissions?
**Answer:** RBAC.

### Q2) In Bell–LaPadula, what rule prevents data leakage to lower classifications?
**Answer:** No write down.

### Q3) In Biba, why is “no read down” useful?
**Answer:** Prevents high-integrity subjects from reading low-integrity data (reduces contamination).

### Q4) What is the difference between ACL and RBAC?
**Answer:** ACLs attach permissions to objects; RBAC assigns permissions to roles.

### Q5) A user can access a file only if they are in Finance, using a corporate laptop, during business hours. Which model fits?
**Answer:** ABAC.

### Q6) In Bell–LaPadula, can a Top Secret user write to a Secret file?
**Answer:** No (no write down).

### Q7) In Biba, can a high-integrity process read low-integrity input?
**Answer:** No (no read down).

### Q8) Give one example of a detective control in access control.
**Answer:** Audit logs of login attempts.

---

## 12) Exam checklist (Module 03)
- DAC vs MAC vs RBAC vs ABAC.
- Bell–LaPadula vs Biba vs Clark–Wilson.
- Separation of duties and least privilege.
- Defense in depth examples.
- Be able to answer “can read/write?” model questions fast.
