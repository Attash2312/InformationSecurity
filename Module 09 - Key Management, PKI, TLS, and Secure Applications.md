# Module 09 — Key Management, PKI, TLS, and Secure Applications (Exam Prep Notes)

## 1) Why key management matters (often more important than algorithms)
Even strong algorithms (AES/RSA) fail if keys are:
- Weak (low entropy)
- Exposed (stored insecurely)
- Reused incorrectly (nonce/IV reuse)
- Not rotated

**Exam statement:** Security depends on correct key management.

---

## 2) Key lifecycle
Typical stages:
1) Generation (high entropy)
2) Distribution (secure transfer)
3) Storage (protect at rest)
4) Use (with correct modes/nonce rules)
5) Rotation (periodic change)
6) Revocation (if compromised)
7) Destruction (secure wipe)

---

## 3) Key generation and randomness
- Use cryptographically secure random number generators.
- Don’t generate keys from predictable data (timestamps, usernames).

### Salts vs IVs vs nonces (common confusion)
- **Salt** (password hashing): random value stored with hash to defeat rainbow tables.
- **IV** (CBC): random/unpredictable value to randomize first block.
- **Nonce** (CTR/GCM): must be unique per key (often not required to be secret).

### Quick table (exam-friendly)
| Term | Used in | Must be secret? | Must be unique? | Must be unpredictable? |
|---|---|---:|---:|---:|
| Salt | password hashing | No | Yes (per password) | Yes (random) |
| IV (CBC) | CBC mode | No | Yes (per encryption) | Yes |
| Nonce (CTR/GCM) | CTR/GCM | No | Yes (per key) | Not always, but uniqueness is critical |

---

## 4) Password hashing vs encryption
- Passwords should be stored with **slow KDF** (PBKDF2/bcrypt/scrypt/Argon2) + unique salt.
- Do not store passwords with fast hashes (e.g., plain SHA-256) alone.

---

## 5) Public Key Infrastructure (PKI)
### 5.1 Certificates
A certificate binds:
- Identity (subject)
- Public key
- Validity period
- Issuer signature (CA)

### Visual: certificate idea
```
Certificate = {
	Subject identity,
	Subject public key,
	Validity,
	Issuer (CA),
	CA signature over the above
}
```

### 5.2 Chain of trust
Trusted root CA → intermediate CA → end-entity certificate.

### Visual: chain of trust (what to draw)
```
Root CA (trusted in OS/browser)
	|
	| signs
	v
Intermediate CA
	|
	| signs
	v
Server certificate (example.com)
```

### 5.3 Revocation
- CRL
- OCSP

---

## 6) TLS (Transport Layer Security) — what you should know
TLS provides:
- Confidentiality (symmetric encryption)
- Integrity (MAC/AEAD)
- Authentication (certificates)

Typical modern flow (conceptually):
1) Client connects
2) Server presents certificate
3) Client validates certificate chain + hostname
4) Key exchange establishes a shared session key
5) Data encrypted with symmetric crypto (AES-GCM/ChaCha20-Poly1305)

### Visual: TLS “story” (high-yield)
```
Client ------------------------------ Server
	|   ClientHello (supported crypto)   |
	|----------------------------------->|
	|          Certificate               |
	|<-----------------------------------|
	|  Validate CA chain + hostname      |
	|   Key exchange -> shared secret    |
	|<========== handshake finished =====|
	|   Application data (AES-GCM)       |
	|<=========== encrypted ============>|
```

### Step-by-step: how to answer “what happens in TLS?”
1) Server proves identity with a certificate (signed by CA).
2) Client verifies chain + hostname.
3) They establish shared secrets (key exchange).
4) Then they switch to fast symmetric encryption for data.

**Exam tip:** TLS uses asymmetric crypto mainly for authentication/key exchange, then symmetric for data.

---

## 7) Secure application patterns (exam-friendly)
### 7.1 Data at rest vs data in transit
- At rest: disk/database encryption, key access controls
- In transit: TLS

### 7.2 Principle of least privilege
Apps should use minimal database permissions.

### 7.3 Logging and monitoring
- Log authentication failures
- Protect logs from tampering
- Use centralized monitoring/SIEM where possible

---

## 8) Solved examples

### Example 1: Choose correct storage method
Question: “Should we encrypt user passwords and store the key in the app?”
Correct approach:
- Don’t encrypt passwords.
- Store a salted slow-hash (KDF output).
Reason: encryption is reversible; hashes are verification-oriented.

### Example 2: Nonce reuse danger (CTR/GCM)
If the same key and nonce are reused, the same keystream is reused.
Given:
- $C_1 = P_1 \oplus S$
- $C_2 = P_2 \oplus S$
Then:
$$C_1 \oplus C_2 = (P_1 \oplus S) \oplus (P_2 \oplus S) = P_1 \oplus P_2$$
So an attacker learns relationship between plaintexts.

### Example 3: Certificate validation checks
When a browser validates a certificate, it checks:
- Signature chain to a trusted CA
- Valid dates
- Hostname matches
- Revocation status (as applicable)

### Example 4 (Numerical): RPO/RTO conversion
RPO = 45 minutes.
- If backups run every 15 minutes, RPO target is feasible.
RTO = 6 hours.
- You need staffing + automation + tested runbooks to meet it.

### Example 5 (Numerical): Password entropy (rough exam math)
If a password uses 8 characters and each character can be one of 26 lowercase letters:
$$N = 26^8$$
Entropy in bits:
$$H = \log_2(N) = 8\log_2(26) \approx 8\cdot 4.7 \approx 37.6\text{ bits}$$
This is why longer passwords (or passphrases) matter.

---

## 9) Practice questions (with solutions)

### Q1) Why is a salt used in password hashing?
**Answer:** To ensure identical passwords don’t have identical hashes and to defeat rainbow tables.

### Q2) Is an IV required to be secret?
**Answer:** Usually no, but it must meet required properties (CBC: unpredictable; CTR/GCM: unique).

### Q3) What does TLS primarily use asymmetric cryptography for?
**Answer:** Authentication and key exchange.

### Q4) What is key rotation?
**Answer:** Periodically replacing keys to reduce exposure window and limit damage if a key is compromised.

## 10) Numericals (solved drills)

### N1) Padding/blocks planning
You encrypt files with AES (16-byte blocks) using CBC + PKCS#7.
If file size is 10,000 bytes:
- Blocks = $\lceil 10000/16 \rceil = 625$ blocks
- If 10,000 is not divisible by 16, padding is included inside that ceiling.
Ciphertext size = $625\cdot 16 = 10,000$? Check remainder:
- $10000 \bmod 16 = 0$ so padding adds a full block.
- Blocks become 626, ciphertext = $626\cdot 16 = 10,016$ bytes.

### N2) Keyspace comparison
Compare keyspaces:
- AES-128: $2^{128}$
- DES: $2^{56}$
Ratio:
$$\frac{2^{128}}{2^{56}}=2^{72}$$
So AES-128 has $2^{72}$ times more keys than DES.

## 11) How to memorize + solve faster
1) Memorize the salt/IV/nonce table.
2) Drill RTO/RPO and “block size → block count → padding” calculations.
3) Remember: crypto fails more often from *bad key handling* than from AES/RSA being broken.

---

## 12) Exam checklist (Module 09)
- Key lifecycle stages.
- Salt vs IV vs nonce.
- Password hashing (KDF) vs encryption.
- PKI: certificates, CA chain, revocation.
- TLS: what it provides and high-level handshake purpose.
