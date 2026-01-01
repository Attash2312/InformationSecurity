# Solved Past Papers (Paraphrased) — Solved Answers + Explanations

> Notes
> - Questions are **paraphrased** (not copied) from scanned papers.
> - Each item follows: **Solution → Final Answer → Explanation**.
> - Scope filter applied: **only topics within Modules 1, 2, 3, 4, 5, 6, 6b, 8, 9 + MixColumns**.

---

## Key Usage Table (Required Exam Question)

**Question (exam-style):** Explain how the **public/private keys** of the **sender** and **receiver** are used to achieve: confidentiality, integrity, authentication, non-repudiation, and PGP.

### Solution

- **Confidentiality (public-key encryption):**
  - Sender encrypts using **Receiver Public Key**.
  - Receiver decrypts using **Receiver Private Key**.

- **Integrity / Authentication / Non-repudiation (digital signature):**
  - Sender signs using **Sender Private Key**.
  - Receiver verifies using **Sender Public Key**.

- **PGP (hybrid: encrypt + sign):**
  - Sender creates a **digital signature** (Sender Private) over the message (or its hash).
  - Sender encrypts message+signature with a **random session key** (symmetric).
  - Sender encrypts the session key using **Receiver Public Key**.
  - Receiver uses **Receiver Private Key** to recover the session key, decrypts the message, then verifies signature using **Sender Public Key**.

### Final Answer (table to write in exam)

| Key owner (row) | Confidentiality | Integrity | Authentication | Non-repudiation | PGP |
|---|---|---|---|---|---|
| **Sender+** (Sender Public) | Not used | **Used by receiver** to verify | **Used by receiver** to verify | **Used by receiver** to verify | Used by receiver to verify signature (Sender Public) |
| **Sender−** (Sender Private) | Not used | **Used to sign** | **Used to sign** | **Used to sign** | Used to sign (Sender Private) |
| **Receiver+** (Receiver Public) | **Used by sender** to encrypt | Not used | Not used | Not used | Used by sender to encrypt session key (Receiver Public) |
| **Receiver−** (Receiver Private) | **Used to decrypt** | Not used | Not used | Not used | Used to decrypt session key (Receiver Private) |

### Explanation
- Confidentiality is achieved when only the receiver can decrypt (private key is secret).
- Integrity/authentication/non-repudiation come from the fact that only the sender holds the sender’s private key.
- PGP combines both: **sign (private) + encrypt (receiver public for key transport)**.

---

## IS Terminal — Spring 2025 (Paraphrased)

### Q2.1 (Theory): Countermeasures and security controls
**Paraphrased question:** List countermeasures to reduce risk/exposure.

**Solution (high-yield list)**
- Preventive: MFA, least privilege, patching, segmentation, secure configuration.
- Detective: audit logs, monitoring/alerting.
- Corrective: backups, incident response, recovery procedures.
- Administrative: security policies, user training, audits.

**Final Answer**
- Give 2–3 controls per category (prevent/detect/correct + admin/technical/physical).

**Explanation**
- Marks come from correct classification + realistic examples.

---

### Q2.2 (Numerical): Affine cipher (a=25, b=6)
**Paraphrased question:** Apply Affine cipher with $a=25$ and $b=6$ to the given sentence.

**Given**
- Alphabet index: A=0..Z=25
- $E(x)=(ax+b)\bmod 26$
- Here $a=25\equiv -1\pmod{26}$ so $E(x)=(-x+6)\bmod 26$

**Final Answer (ciphertext)**
`ISM UMON FC NZC EZGTAC ISM KYOZ NS OCC YT NZC KSPVD`

**Explanation**
- Because $a=25\equiv -1$, you “flip” the index then shift by 6.

---

### Q2.3 (Numerical): AES-128 first-round key for ASCII key
**Paraphrased question:** AES key = `IamTakingNextSem` (16 ASCII bytes). Generate the **first-round key** (Rcon = 01 hex).

**Solution (computed results)**
Key words (hex):
- $w_0=49616d54$
- $w_1=616b696e$
- $w_2=674e6578$
- $w_3=7453656d$

Round-1 words:
- $w_4=a52c51c6$
- $w_5=c44738a8$
- $w_6=a3095dd0$
- $w_7=d75a38bd$

**Final Answer (round-1 key = $w_4||w_5||w_6||w_7$)**
- `a52c51c6 c44738a8 a3095dd0 d75a38bd`

**Explanation**
- AES-128 expansion is: $w_4=w_0\oplus g(w_3)$ then XOR-chain forward.

---

### Q3.1 (Numerical): Diffie–Hellman with MITM
**Paraphrased question:** $p=17$, $g=7$. Alice $a=2$, Bob $b=3$. Trudy MITM with $t=6$. Find the two secrets.

**Solution**
- $A=7^2\bmod 17=15$
- $B=7^3\bmod 17=3$
- $T=7^6\bmod 17=9$

Secrets:
- $K_{AT}=T^a\bmod 17=9^2\bmod 17=13$
- $K_{BT}=T^b\bmod 17=9^3\bmod 17=15$

**Final Answer**
- $K_{AT}=13$, $K_{BT}=15$

**Explanation**
- MITM splits the key exchange into two separate shared secrets.

---

### Q3.2 (Numerical): RSA decoding key with p=q=7
**Paraphrased question:** RSA with $p=7$, $q=7$, $e=5$. Find $d$.

**Solution**
- $n=49$, $\varphi(n)=(6)(6)=36$
- $d=e^{-1}\bmod 36=5^{-1}\bmod 36=29$

**Final Answer**
- $d=29$

**Explanation**
- RSA requires modular inverse of $e$ modulo $\varphi(n)$.

---

## IS Terminal — Fall 2022 (Paraphrased)

### Q2 (Numerical): Affine cipher decryption (a=7, b=5)
**Paraphrased question:** Decrypt the Affine ciphertext with $a=7$, $b=5$.

**Solution**
- Inverse: $7^{-1}\bmod 26 = 15$ because $7\cdot 15\equiv 1\pmod{26}$
- Decrypt with: $x=15(y-5)\bmod 26$

**Final Answer (plaintext)**
- `THE FUTURE IS YET IN YOUR POWER`

**Explanation**
- The key step is finding $a^{-1}$; then apply the formula letter-by-letter.

---

### Q4 (Numerical): Diffie–Hellman shared secret
**Paraphrased question:** $g=7$, $p=11$, Alice $a=7$, Bob $b=8$. Find shared secret.

**Final Answer**
- Public values: $A=6$, $B=9$
- Shared secret: $K=4$

**Explanation**
- Both sides compute $g^{ab}\bmod p$ in different ways.

---

### Q5 (Numerical): RSA with p=7, q=13
**Paraphrased question:** Compute $n$, $\varphi(n)$ and list the three largest valid public exponents $e$ (<72).

**Final Answer**
- $n=91$, $\varphi(n)=72$
- Three largest valid $e$: **65, 67, 71**
- Matching $d=e^{-1}\bmod 72$: **41, 43, 71**

**Explanation**
- Valid $e$ must satisfy $\gcd(e,72)=1$ so it is invertible mod $\varphi(n)$.

---

### Q6(a) (Numerical): Digest collision (sum of first letters)
**Paraphrased question:** Digest = sum of indices of first letter of each word. For “I insist staying in COMSATS”, compute digest and give a collision.

**Solution**
First letters: I, I, S, I, C → indices 8, 8, 18, 8, 2.

**Final Answer**
- Digest = $8+8+18+8+2=44$
- Collision example: “I imagine sleeping in class” (same first letters → same digest 44)

**Explanation**
- The digest ignores almost all the message; any message with same first-letter pattern collides.

---

### Q6(b) (Theory): ADD → MULTIPLY and collisions
**Paraphrased question:** If you replace addition with multiplication, why can collisions explode?

**Final Answer**
- If any letter index is 0 (A), product becomes 0 → massive collisions.
- Products also have many factorizations → many different inputs can map to same product.

**Explanation**
- Multiplication creates “special values” and a lot of structural ambiguity.

---

### Q6(c) (Theory): Use first two letters instead of first
**Paraphrased question:** If digest sums indices of first two letters of each word, does collision count increase or decrease?

**Final Answer**
- **Decrease**, because more information from the message is included.

**Explanation**
- More features generally reduce collisions (still not cryptographically secure, but better than only first letters).

---

## IS Terminal — Spring 2024 (Paraphrased)

### Q1.1 (Theory): CIA in an online portal
**Paraphrased question:** Using a university portal, explain confidentiality, integrity, availability.

**Final Answer (exam points)**
- Confidentiality: only authorized users can view data (use MFA/ACLs/TLS).
- Integrity: prevent unauthorized changes (use RBAC/audit logs/change control).
- Availability: service stays reachable (use redundancy/backups/monitoring).

**Explanation**
- Marking usually expects definition + mapping to the portal + controls.

---

### Q1.2 (Numerical): Password brute-force search space (7 chars)
**Paraphrased question:** Password length 7 using lowercase + uppercase + digits. Worst-case brute-force tries?

**Solution**
- Alphabet size = $26+26+10=62$
- Search space: $62^7=3,521,614,606,208$

**Final Answer**
- $62^7 = 3,521,614,606,208$

**Explanation**
- Product rule: 62 choices per position × 7 positions.

---

### Q3.1 (Numerical): Diffie–Hellman MITM (g=6, p=13)
**Paraphrased question:** $p=13$, $g=6$, Alice $a=5$, Bob $b=4$, Trudy $t=6$. Find $K_{AT}$ and $K_{BT}$.

**Final Answer**
- $K_{AT}=12$
- $K_{BT}=1$

**Explanation**
- $T=6^6\bmod 13=12\equiv -1$ makes powers easy: odd → 12, even → 1.

---

### Q3.2 (Numerical): RSA invalid public exponent
**Paraphrased question:** RSA with $p=5$, $q=13$, and $e=12$. Find $d$.

**Final Answer**
- No valid $d$ exists because $\gcd(12,48)\neq 1$ so $12$ has no inverse mod $48$.

**Explanation**
- RSA requires $d=e^{-1}\bmod \varphi(n)$ and inverse exists only when gcd is 1.

---

### Q4(a) (Numerical): Digest collision (sum of letters)
**Paraphrased question:** Sum-of-letter-indices digest. Compute digest of “COMSIAN” and give a collision.

**Final Answer**
- Digest(COMSIAN) = **67**
- Collision example: **ZZKFCAA** (also sums to 67)

**Explanation**
- Sum digests ignore order and are trivially collision-prone.

---

## Message Integrity — Exam Practice (within syllabus)

### Q1 (Theory): Define message integrity
**Final Answer**
- Integrity means the message received is exactly the same as the message sent (detect unauthorized modification).

**Explanation**
- Integrity failures allow silent tampering (amounts/commands/grades).

---

### Q2 (Theory): Checksum vs hash vs MAC vs digital signature
**Final Answer**
- Checksum: error detection (not attacker-resistant).
- Hash: integrity detection (no sender authenticity).
- MAC (HMAC): integrity + authentication (shared secret key).
- Digital signature: integrity + authentication + non-repudiation (public/private keys).

**Explanation**
- Authenticity requires either a shared secret (MAC) or a private key (signature).

---

### Q3 (Theory): Why (message + hash) is not authenticity
**Final Answer**
- An attacker can replace both the message and the hash; use MAC or signatures.

**Explanation**
- Without a key, anyone can compute a new hash for a modified message.

---

### Q4 (Numerical): Simple checksum collision
**Final Answer**
- Digest(COMSIAN) = 67
- Collision: ZZKFCAA also sums to 67

**Explanation**
- Sum-based checksums collide easily.

---

### Q5 (Theory): HMAC purpose
**Final Answer**
- HMAC provides integrity + sender authentication because only parties with the shared key can produce a valid MAC.

**Explanation**
- It prevents forging “message + hash” without the secret.

---

### Q6 (Theory): Digital signature workflow
**Final Answer**
1) Sender computes $h=H(M)$
2) Sender signs $h$ with sender private key
3) Receiver hashes $M$ and verifies signature with sender public key

**Explanation**
- Signature binds the sender to the message hash.
