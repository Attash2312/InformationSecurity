# Module 04 — Cryptography and Encryption (Exam Prep Notes)

## 1) Big Picture: What cryptography is (and is not)
**Cryptography** is the science of protecting information by transforming it so only authorized parties can use it.

Cryptography supports four core security goals:
- **Confidentiality**: keep data secret from unauthorized parties (encryption).
- **Integrity**: detect unauthorized modification (hash/MAC/signature).
- **Authentication**: prove identity or prove message origin.
- **Non-repudiation**: prevent a sender from denying they sent a message (digital signatures).

What cryptography does **not** magically solve:
- Weak passwords
- Malware on endpoints
- Poor key management
- Social engineering

---

## 2) Key terms you must know
- **Plaintext**: original readable message.
- **Ciphertext**: encrypted (scrambled) output.
- **Cipher**: an algorithm for encryption/decryption.
- **Key**: secret value controlling the cipher.
- **Encryption**: plaintext → ciphertext.
- **Decryption**: ciphertext → plaintext.
- **Kerckhoffs’s Principle**: assume the attacker knows the algorithm; security must rely on the key.
- **Cryptanalysis**: attacks on cryptographic systems.

### Symmetric vs Asymmetric (high-level)
- **Symmetric-key**: same key for encryption and decryption. Fast. Great for bulk data.
- **Asymmetric-key**: public/private key pair. Slower. Great for key exchange, signatures, identity.

### Quick table: when to use what (exam-friendly)
| Goal | Best primitive | Why |
|---|---|---|
| Confidentiality | Symmetric encryption (AES) | Fast for large data |
| Integrity | Hash / MAC / signature | Detect tampering |
| Authentication | MAC or digital signature | Proves origin (shared key vs public key) |
| Non-repudiation | Digital signature | Sender cannot deny (private key) |

---

## 3) Common cryptographic primitives
### 3.1 Encryption (confidentiality)
- **Block ciphers** (AES, DES): encrypt fixed-size blocks (e.g., AES uses 128-bit blocks).
- **Stream ciphers** (concept): generate a keystream and XOR with plaintext.

### 3.2 Hash functions (integrity checks, fingerprints)
A **hash** maps any input to a fixed-length output.
Properties (idealized):
- **Preimage resistance**: given hash $h$, hard to find $m$ such that $H(m)=h$.
- **Second preimage resistance**: given $m$, hard to find $m'\neq m$ with same hash.
- **Collision resistance**: hard to find any pair $(m,m')$ with $H(m)=H(m')$.

Common uses:
- File integrity verification
- Password storage (with salt + slow KDF)
- Digital signatures often sign a hash of the message

### 3.3 MAC (Message Authentication Code)
A **MAC** provides **integrity + authentication** using a shared secret key.
- Example: HMAC (hash-based MAC)
- If two parties share key $K$, then MAC proves “someone with $K$ produced this”.

### 3.4 Digital signatures
Provide integrity + authentication + non-repudiation using private/public keys.
(Details in Module 08.)

### Mini-figure: how the primitives relate
```
Confidentiality -> Encryption (AES)
Integrity       -> Hash / MAC / Signature
Authentication  -> MAC (shared key) or Signature (public key)
```

---

## 4) XOR is the most important operation in crypto basics
XOR rules (treat as bitwise):
- $A \oplus A = 0$
- $A \oplus 0 = A$
- $A \oplus B = B \oplus A$ (commutative)
- If $C = A \oplus B$, then $A = C \oplus B$ and $B = C \oplus A$

These rules explain why stream ciphers and modes like CBC/CTR rely heavily on XOR.

---

## 5) Classical ciphers (often tested conceptually)
### 5.1 Caesar cipher
Shift each letter by $k$.
- Easy to break (only 25 possible shifts in English).

**Visual (how shifting works)**
If we number letters as A=0..Z=25, Caesar is:
$$E(x)=(x+k)\bmod 26$$

Quick “alphabet strip” view (shift by 3):
| Plain | A | B | C | D | E | F | G | H | I | J | K | L | M | N | O | P | Q | R | S | T | U | V | W | X | Y | Z |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| Cipher | D | E | F | G | H | I | J | K | L | M | N | O | P | Q | R | S | T | U | V | W | X | Y | Z | A | B | C |

**Solved example**
Encrypt “ATTACK” with shift $k=3$:
- A→D, T→W, T→W, A→D, C→F, K→N
- Ciphertext: **DWWDFN**

Decrypt “DWWDFN” with shift $k=3$:
- D→A, W→T, W→T, D→A, F→C, N→K
- Plaintext: **ATTACK**

### 5.2 Vigenère cipher (polyalphabetic)
Uses a repeating key to shift each letter by varying amounts.
- Stronger than Caesar but still breakable with frequency methods.

**How it works (exam recipe)**
1) Map letters to numbers A=0..Z=25.
2) Repeat the key to match plaintext length.
3) Encrypt each position:
$$C_i = (P_i + K_i)\bmod 26$$
4) Decrypt:
$$P_i = (C_i - K_i)\bmod 26$$

**Visual: aligned key**
Example (spaces ignored):
```
PLAINTEXT:  A T T A C K
KEY:        L E M O N L
```

**Solved mini-example (classic style)**
Encrypt “ATTACK” with key “LEMON”:
- Convert: A=0, T=19, C=2, K=10
- Key: L=11, E=4, M=12, O=14, N=13
- Compute:
	- A(0)+L(11)=11 → L
	- T(19)+E(4)=23 → X
	- T(19)+M(12)=31 mod26=5 → F
	- A(0)+O(14)=14 → O
	- C(2)+N(13)=15 → P
	- K(10)+L(11)=21 → V
- Ciphertext: **LXFOPV**

---

### 5.3 Affine cipher (very common in numericals)
Affine is a “multiply then add” cipher on letter indices.

**Formulas (write these in exam)**
- Encryption:
$$E(x)=(ax+b)\bmod 26$$
- Decryption (requires modular inverse $a^{-1}$):
$$D(y)=a^{-1}(y-b)\bmod 26$$

**Critical condition**
You can decrypt only if $\gcd(a,26)=1$ (so $a^{-1}$ exists).

**Visual: what changes vs Caesar**
- Caesar: add a fixed shift.
- Affine: “scale” the alphabet by $a$ (scramble spacing), then shift by $b$.

**Exam recipe (how to solve fast)**
1) Confirm $\gcd(a,26)=1$.
2) If encrypting: compute $E(x)$ letter-by-letter.
3) If decrypting:
	 - Find $a^{-1}\bmod 26$ (Extended Euclid is fastest).
	 - Apply $x=a^{-1}(y-b)\bmod 26$.

**Solved example (encryption)**
Encrypt “HELLO” with $a=5$, $b=8$.
- Mapping: H=7, E=4, L=11, O=14
- Compute $E(x)=(5x+8)\bmod 26$:
	- H: (5·7+8)=43 mod26=17 → R
	- E: (5·4+8)=28 mod26=2 → C
	- L: (5·11+8)=63 mod26=11 → L
	- L: → L
	- O: (5·14+8)=78 mod26=0 → A
Ciphertext: **RCLLA**

**Solved example (decryption)**
Decrypt “RCLLA” with $a=5$, $b=8$.
- Find inverse: $5^{-1}\bmod 26 = 21$ (because 5·21=105 ≡ 1 mod26)
- Apply $x=21(y-8)\bmod 26$:
	- R(17): 21(17-8)=21·9=189 mod26=7 → H
	- C(2):  21(2-8)=21·(-6)=-126 mod26=4 → E
	- L(11): 21(11-8)=21·3=63 mod26=11 → L
	- L → L
	- A(0):  21(0-8)=21·(-8)=-168 mod26=14 → O
Plaintext: **HELLO**

**Exam shortcut (special case you saw in past papers)**
If $a=25$, then $a\equiv -1\pmod{26}$ so:
$$E(x)=(-x+b)\bmod 26$$
This becomes “flip index then add $b$”.

---

### 5.4 Transposition cipher (reordering positions)
Transposition does **not** change letters; it changes their positions.

**Example: simple columnar transposition (visual)**
Write plaintext under a fixed number of columns, then read column-by-column.

Plaintext: “MEETME” with 3 columns:
| 1 | 2 | 3 |
|---|---|---|
| M | E | E |
| T | M | E |

Read down columns: (col1) MT, (col2) EM, (col3) EE → Ciphertext: **MTEMEE**

**Exam note**
Transposition is about permutation (reordering). Substitution/Affine/Vigenère are about changing letters.

---

## 6) Modern crypto concepts you’re likely to be tested on
### 6.1 Confusion and diffusion
- **Confusion**: make relationship between key and ciphertext complex.
- **Diffusion**: spread plaintext influence across many ciphertext bits.

Block ciphers achieve these with substitution + permutation across rounds.

### 6.2 Security depends on key size and brute force
If a key is $n$ bits, a brute-force attacker may need up to $2^n$ tries (average $2^{n-1}$).
- 56-bit (DES) is too small today.
- 128-bit (AES-128) is considered strong for most uses.

### 6.3 Entropy (password and key strength)
- Keys should be random with high entropy.
- Human-chosen passwords are low-entropy → use salt + slow KDF (e.g., PBKDF2/bcrypt/scrypt/Argon2).

---

## 7) Common attacks (know the names + the idea)
- **Brute force**: try all keys.
- **Dictionary attack**: try likely passwords/keys.
- **Rainbow tables**: precomputed hashes (mitigated by salting).
- **Birthday attack**: collisions become likely around $\approx 2^{n/2}$ for an $n$-bit hash.
- **Meet-in-the-middle**: reduces complexity for some multi-encryption designs.
- **Man-in-the-middle (MITM)**: intercept/modify key exchange if authentication is missing.

---

## 8) “Encryption vs encoding vs hashing” (common exam trick)
- **Encryption**: reversible with a key (confidentiality).
- **Encoding**: reversible without a secret (for format/transport, e.g., Base64).
- **Hashing**: one-way (integrity/fingerprint), not meant to be reversible.

### Quick table: encryption vs encoding vs hashing vs signing
| Mechanism | Secret needed? | Reversible? | Primary purpose | Example |
|---|---:|---:|---|---|
| Encryption | Yes (key) | Yes (with key) | Confidentiality | AES |
| Encoding | No | Yes | Transport/format | Base64 |
| Hashing | No | No | Fingerprint/integrity | SHA-256 |
| Digital signature | Private key | Verify (not “reverse”) | Integrity + authenticity | RSA-PSS |

---

## 9) Worked examples (core skills)

### Example 1: XOR encryption (toy stream cipher idea)
Suppose plaintext byte $P=0x3A$ and keystream byte $K=0xC5$.
Ciphertext: $C = P \oplus K = 0x3A \oplus 0xC5$

Compute:
- $0x3A = 0011\ 1010$
- $0xC5 = 1100\ 0101$
- XOR  = 1111\ 1111 = $0xFF$

So $C=0xFF$.

Decrypt uses the same operation:
- $P = C \oplus K = 0xFF \oplus 0xC5 = 0x3A$

### Example 2: Hash “integrity check” concept
You download a file and the website provides SHA-256 hash.
- If your computed hash matches the published hash, it strongly suggests file integrity.
- It does **not** automatically prove authenticity unless the hash itself is delivered securely (e.g., signed).

### Example 3: Birthday bound quick math
If a hash is 128 bits, collision resistance is roughly $2^{128/2} = 2^{64}$ operations.
This is why 64-bit hashes are too small for collision resistance.

---

## 10) Numericals (solved drills)

### N1) XOR drill (fast)
Compute $0x5A \oplus 0xC3$.
- $0x5A \oplus 0xC3 = 0x99$

### N2) Brute-force time
If key length is $n$ bits and a system can try $R$ keys/sec:
- Worst-case: $T=2^n/R$
- Average-case: $T=2^{n-1}/R$

Example: DES $n=56$, $R=10^9$ keys/sec:
- Worst-case $\approx 2^{56}/10^9 \approx 7.2\times 10^7$ sec ≈ 2.3 years

### N3) Birthday bound estimate
For an $n$-bit hash, collision work is about $2^{n/2}$.
Example: SHA-256 → about $2^{128}$ operations.

### N4) “Is Base64 encryption?” quick proof
If you can decode without a secret key, it’s not encryption.
Base64 decoding is public → encoding, not encryption.

---

## 11) Practice questions (with solutions)

### Q1) Which property of a hash function prevents finding any two messages with the same hash?
**Answer:** Collision resistance.

### Q2) You see Base64 in a system. Is that encryption?
**Answer:** No. Base64 is encoding; anyone can decode it.

### Q3) Why is Kerckhoffs’s principle important?
**Answer:** Because algorithms become public; security must rely on secret keys, not secrecy of the algorithm.

### Q4) A system uses a shared secret key to verify that messages were not altered and came from someone who knows the key. What primitive is this?
**Answer:** A MAC (e.g., HMAC).

### Q5) If a password database stores unsalted hashes, what’s the risk?
**Answer:** Rainbow table attacks become practical; identical passwords produce identical hashes.

### Q6) You need integrity + sender authentication between two servers that share a secret. What should you use?
**Answer:** A MAC (e.g., HMAC).

### Q7) You need integrity + non-repudiation for a contract PDF. What should you use?
**Answer:** A digital signature.

### Q8) Why is “security by obscurity” a bad strategy?
**Answer:** Attackers can learn algorithms; good designs remain secure even when the algorithm is known.

### Q9) A 256-bit hash has collision work factor about what size?
**Answer:** About $2^{128}$ (birthday bound).

### Q10) What two things must be protected for encryption to remain secure?
**Answer:** The key (and nonce/IV rules, depending on mode).

---

## 12) How to memorize Module 04 fast
Use the mnemonic **“E-H-M-S”**:
- **E**ncryption = confidentiality
- **H**ash = fingerprint (integrity check)
- **M**AC = integrity + authentication (shared key)
- **S**ignature = integrity + authentication + non-repudiation (public key)

Practice drill: for each scenario, write the required goal(s) → pick E/H/M/S.

---

## 13) Exam checklist (Module 04)
- Define encryption, hashing, MAC, signature.
- Explain symmetric vs asymmetric (speed + use cases).
- Know XOR properties and why they matter.
- Know confusion/diffusion.
- Recognize common attacks by name.
- Distinguish encryption vs encoding vs hashing.
- Be able to do quick numericals: XOR, brute-force time, birthday bound.
