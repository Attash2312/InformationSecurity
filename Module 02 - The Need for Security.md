# Module 02 — The Need for Security (Exam Prep Notes)

## 1) Why security is necessary
Organizations protect systems because failures cause:
- Financial loss (fraud, ransomware, downtime)
- Legal/regulatory penalties
- Reputation damage
- Safety risks (critical infrastructure, hospitals)

**Exam line:** Security exists to manage risk—not to eliminate it entirely.

### Quick table: common business impacts
| Impact type | What it looks like | CIA mapping |
|---|---|---|
| Financial | fraud, ransom payments, lost sales | A/C/I (depends on incident) |
| Legal/regulatory | fines, lawsuits, audits | Often C (privacy) + I (records) |
| Reputation | loss of trust, bad press | Often C/I incidents |
| Operational | downtime, missed deadlines | A |

---

## 2) Common threat categories
### 2.1 Malware
- **Virus**: attaches to files; needs user action to spread.
- **Worm**: self-replicates across networks.
- **Trojan**: looks legitimate, performs malicious actions.
- **Ransomware**: encrypts data and demands payment.
- **Spyware/keylogger**: steals information.

### 2.2 Social engineering
Attackers target humans instead of technology.
- Phishing, spear phishing
- Pretexting
- Baiting (infected USB)

### 2.3 Network and web attacks
- DoS/DDoS
- Man-in-the-middle (MITM)
- Password attacks (brute force, credential stuffing)
- Web: SQL injection, XSS (conceptually)

### 2.4 Physical and environmental threats
- Theft, vandalism
- Fire, flood, power loss

---

## 3) Risk management (core exam topic)
### 3.1 Risk response options
- **Avoid**: stop the risky activity.
- **Mitigate (reduce)**: implement controls.
- **Transfer**: shift risk (insurance, outsourcing with contract).
- **Accept**: acknowledge and monitor (when cost > benefit).

### Risk response decision guide (step-by-step)
1) If impact is unacceptable and you *can* stop the activity → **Avoid**.
2) If you can reduce likelihood/impact reasonably → **Mitigate**.
3) If you can shift financial impact via contracts/insurance → **Transfer**.
4) If cost of controls > expected loss and risk is tolerable → **Accept**.

### 3.2 Residual risk
Risk that remains after controls are applied.

### 3.3 Qualitative vs quantitative risk
- Qualitative: High/Medium/Low ratings.
- Quantitative: uses numbers and money values.

---

## 4) Business impact and continuity
### 4.1 BIA (Business Impact Analysis)
Finds critical processes and the impact of downtime.

Key terms:
- **RTO (Recovery Time Objective)**: max acceptable time to restore.
- **RPO (Recovery Point Objective)**: max acceptable data loss (time).

### Mini-figure: RTO vs RPO
```
Time  <------------------------------>

Last safe backup ----(RPO)---- Incident ----(RTO)---- Service restored
			 (data loss window)         (downtime window)
```

### 4.2 Backups (common exam list)
- Full, incremental, differential (conceptual differences)

| Backup type | What it contains | Restore speed | Storage use |
|---|---|---|---|
| Full | all data | Fastest | Highest |
| Incremental | changes since last backup (full or incremental) | Slowest (need many sets) | Lowest |
| Differential | changes since last full | Medium | Medium |

---

## 5) Security program benefits
- Reduces incidents
- Improves resilience and recovery
- Supports compliance and customer trust

---

## 6) Solved examples (exam-style)

### Example 1: Choose a risk response
Scenario: A small company runs a public website. Risk of DDoS is moderate; controls are expensive.
Possible responses:
- Transfer: Use a DDoS protection/CDN service.
- Mitigate: Rate limiting, WAF, monitoring.
- Accept: If business impact is low and cost is high.

**Best answer depends on impact + budget.** On exams: choose the option that best reduces high-impact risk.

### Example 2: RTO/RPO
A company says: “We must be back online within 4 hours and can tolerate losing up to 30 minutes of data.”
- RTO = 4 hours
- RPO = 30 minutes

### Example 3: Identify the best first controls (phishing)
Scenario: Employees keep clicking phishing links.
- Best first controls: awareness training + email filtering + MFA
- Reason: phishing targets humans; MFA reduces account takeover impact.

### Example 4: Malware category
Scenario: Malware spreads automatically across the network without user action.
- Answer: **Worm**

### Example 5: Availability planning
Scenario: A service must be available 24/7.
- Controls: redundancy + failover + monitoring + tested DR plan

---

## 7) Numericals (solved drills)

### N1) RPO → required backup frequency
If RPO is 30 minutes, your backup/replication schedule must be **≤ 30 minutes**.

Example:
- If backups run every 2 hours, you cannot guarantee RPO=30 minutes.
- If backups run every 15 minutes, RPO=30 minutes is feasible.

### N2) Downtime cost (simple BIA numeric)
If an online store loses $\$50{,}000$ per hour during an outage:
- For a 3-hour outage, expected revenue loss ≈ $50{,}000\times 3 = \$150{,}000$.

### N3) Quantitative risk (ALE)
A ransomware incident has:
- $AV=\$500{,}000$ potential impacted value
- $EF=0.20$ (20% loss per incident)
- $ARO=1$ per year

Compute:
- $SLE=500{,}000\times 0.20=\$100{,}000$
- $ALE=100{,}000\times 1=\$100{,}000$/year

---

## 8) Practice questions (with solutions)

### Q1) What is the most common reason organizations implement security controls?
**Answer:** To reduce/handle risk to acceptable levels.

### Q2) A user receives an email from the CEO asking for urgent gift cards. What attack is this?
**Answer:** Social engineering (phishing / business email compromise style).

### Q3) Which risk response involves purchasing insurance?
**Answer:** Transfer.

### Q4) If RPO is 15 minutes, what does it mean?
**Answer:** The organization can accept up to 15 minutes of data loss.

### Q5) Give one difference between qualitative and quantitative risk.
**Answer:** Qualitative uses labels (High/Med/Low); quantitative uses numeric estimates (often money).

### Q6) A USB drive labeled “Payroll” is left in the parking lot to tempt employees to plug it in. What is this?
**Answer:** Social engineering (baiting).

### Q7) A program looks like a legitimate installer but secretly steals data. What is it?
**Answer:** Trojan.

### Q8) What is “residual risk”?
**Answer:** The risk that remains after controls are applied.

---

## 9) Exam checklist (Module 02)
- Know why security matters (business + legal + reputation).
- Understand threats: malware, social engineering, network attacks.
- Risk responses: avoid/mitigate/transfer/accept.
- Define residual risk.
- Know RTO vs RPO.
- Be able to do basic numericals: downtime cost, RPO/backup frequency, ALE.
