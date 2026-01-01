# Module 06b — DES and AES + Modes of Operation (Exam Prep Notes)

## 1) DES vs AES (fast comparison table)

| Feature | DES | 3DES | AES |
|---|---:|---:|---:|
| Type | Symmetric block cipher | Symmetric block cipher | Symmetric block cipher |
| Block size | 64 bits | 64 bits | 128 bits |
| Key size | 56 bits (effective) | 112/168 (effective) | 128/192/256 |
| Security today | Broken by brute force | Stronger but legacy | Strong modern standard |
| Speed | Fast in hardware (old) | Slow | Fast + widely optimized |

**Key exam takeaway:** AES replaced DES/3DES because DES key size is too small and 3DES is slow/legacy.

---

## 2) Why modes of operation exist
A block cipher alone encrypts **one block**.
For messages longer than one block you need a **mode of operation** to:
- Encrypt many blocks
- Add randomness (IV/nonce)
- Provide integrity (for AEAD modes)

**Important:** The same plaintext block encrypted under the same key **must not** always produce the same ciphertext block, otherwise patterns leak.

### Quick comparison table (numericals + exam focus)
| Mode | Needs IV/nonce? | Padding? | Parallel? | Typical failure |
|---|---|---|---|---|
| ECB | No | Yes | Yes | pattern leakage |
| CBC | IV (random/unpredictable) | Yes | Encrypt no / Decrypt yes | IV reuse/predictable IV, padding-oracle bugs |
| CTR | Nonce+counter (unique) | No | Yes | nonce reuse (keystream reuse) |
| GCM | Nonce (unique) | No | Yes | nonce reuse breaks security |

---

## 3) ECB mode (Electronic Codebook) — easiest to understand, usually discouraged
### How it works
Encrypt each block independently:
- $C_i = E_K(P_i)$

### Visual
```
P1 -> [ E_K ] -> C1
P2 -> [ E_K ] -> C2
P3 -> [ E_K ] -> C3

Same Pi => same Ci  (pattern leak)
```

### Problem
Equal plaintext blocks → equal ciphertext blocks (pattern leakage).

**Exam line:** ECB provides confidentiality poorly; it leaks structure.

---

## 4) CBC mode (Cipher Block Chaining)
### Encryption
- Choose random **IV** (same size as block)
- $C_0 = IV$
- For $i \ge 1$:
  $$C_i = E_K(P_i \oplus C_{i-1})$$

### Visual (encryption)
```
  +-------+
IV ---> |  XOR  | <--- P1 -----> [ E_K ] -----> C1
  +-------+
          ^
          |
          +---- previous ciphertext (C0 = IV)

C1 ---> XOR with P2 -> [ E_K ] -> C2 -> ...
```

### Decryption
$$P_i = D_K(C_i) \oplus C_{i-1}$$

### Key properties
- IV must be **unpredictable** (random) for CBC.
- Errors propagate: one bit error in $C_i$ affects plaintext block $P_i$ and partly $P_{i+1}$.


### Solved example (CBC with toy block cipher)
We’ll use a toy “cipher” where $E_K(x)=x\oplus K$ and block size is 1 byte.
(This is NOT real security—just to practice CBC math.)

Given:
- Key $K = 0xAA$
- IV = 0x10
- Plaintext blocks: $P_1=0x20$, $P_2=0x30$

Encrypt:
- $C_0 = 0x10$
- $C_1 = E_K(P_1 \oplus C_0) = (0x20 \oplus 0x10) \oplus 0xAA = 0x30 \oplus 0xAA = 0x9A$
- $C_2 = E_K(P_2 \oplus C_1) = (0x30 \oplus 0x9A) \oplus 0xAA = 0xAA \oplus 0xAA = 0x00$

So ciphertext blocks: $C_0=0x10, C_1=0x9A, C_2=0x00$.

Decrypt check:
- $P_1 = D_K(C_1) \oplus C_0 = (0x9A \oplus 0xAA) \oplus 0x10 = 0x30 \oplus 0x10 = 0x20$
- $P_2 = (0x00 \oplus 0xAA) \oplus 0x9A = 0xAA \oplus 0x9A = 0x30$

### Numerical drill: CBC error propagation (concept + quick check)
If one bit flips in ciphertext block $C_i$:
- Plaintext $P_i$ becomes completely wrong (after decryption then XOR)
- Plaintext $P_{i+1}$ has the same bit flipped (because XOR with corrupted $C_i$)

---

## 5) CTR mode (Counter mode) — stream-like
### How it works
- Choose a unique **nonce** (and initial counter)
- Generate keystream blocks:
  $$S_i = E_K(\text{nonce} \| \text{counter}_i)$$
- Encrypt/decrypt using XOR:
  $$C_i = P_i \oplus S_i$$
  $$P_i = C_i \oplus S_i$$

### Visual
```
(nonce||ctr1) -> [ E_K ] -> S1 -> XOR with P1 -> C1
(nonce||ctr2) -> [ E_K ] -> S2 -> XOR with P2 -> C2

Decrypt is identical: C XOR S = P
```

### Exam recipe (how to answer mode questions)
1) Write the core formula (ECB/CBC/CTR).
2) State what extra value is needed: IV (CBC) vs nonce+counter (CTR).
3) State the big failure case:
   - ECB: patterns
   - CBC: IV misuse + padding-oracle class bugs
   - CTR/GCM: nonce reuse (keystream reuse)

### Key properties
- Parallelizable (fast).
- If you reuse the same nonce+counter with the same key → catastrophic.

### Solved example (CTR XOR logic)
Assume keystream byte $S_1 = 0x5C$ and plaintext $P_1=0xF0$.
- $C_1 = 0xF0 \oplus 0x5C = 0xAC$
Decrypt:
- $P_1 = 0xAC \oplus 0x5C = 0xF0$

### Numerical drill: nonce reuse (CTR)
If the same keystream $S$ encrypts two plaintext bytes:
- $C_1 = P_1 \oplus S$
- $C_2 = P_2 \oplus S$
Then $C_1 \oplus C_2 = P_1 \oplus P_2$.

Worked mini example:
- Let $C_1=0xAA$, $C_2=0x0F$, and attacker guesses $P_1=0x20$.
- First compute $P_1 \oplus P_2 = C_1 \oplus C_2 = 0xAA \oplus 0x0F = 0xA5$
- Then $P_2 = P_1 \oplus 0xA5 = 0x20 \oplus 0xA5 = 0x85$

---

## 6) GCM (Galois/Counter Mode) — AEAD concept
GCM combines:
- CTR for encryption (confidentiality)
- A polynomial hash (GHASH) for authentication/integrity

**Exam takeaway:** GCM provides confidentiality + integrity (authenticated encryption).

Nonce rules:
- Nonce must be unique for a given key.
- Reusing a nonce with GCM is very dangerous.

---

## 7) Padding (common exam point)
Block ciphers require plaintext to be a multiple of block size.
CBC typically needs padding (e.g., PKCS#7).
CTR does not require padding (it can encrypt partial blocks by XORing keystream).

### PKCS#7 padding numerical (very exam-friendly)
Block size $B$ bytes, message length $L$ bytes.
Padding length:
$$pad = B - (L \bmod B)$$
If $L$ is already a multiple of $B$, then $pad=B$.

Example: AES block size $B=16$.
- If $L=30$ bytes: $pad = 16 - (30\bmod 16) = 16 - 14 = 2$.
- If $L=32$ bytes: $pad = 16$.

---

## 8) Short theory questions (with answers)

### Q1) Which mode is generally considered insecure because it reveals patterns?
**Answer:** ECB.

### Q2) In CBC, should the IV be secret?
**Answer:** Not necessarily secret, but it must be unpredictable/random and must not repeat with the same key.

### Q3) In CTR, what happens if the same nonce/counter is reused with the same key?
**Answer:** The same keystream is reused; attacker can XOR ciphertexts to cancel keystream and learn relationships between plaintexts.

### Q4) Which mode provides both confidentiality and integrity (in common practice)?
**Answer:** An AEAD mode such as AES-GCM (also ChaCha20-Poly1305).

### Q5) Which is newer and standard today: DES or AES?
**Answer:** AES.

## 9) Numericals (solved drills)

### N1) CBC with toy cipher (one-block)
Using $E_K(x)=x\oplus K$:
- $K=0x3F$, $IV=0x10$, $P_1=0x22$
Compute $C_1$:
- $P_1\oplus IV = 0x22\oplus 0x10 = 0x32$
- $C_1 = 0x32\oplus 0x3F = 0x0D$

### N2) CTR encrypt/decrypt
If keystream byte $S_1=0x9C$ and plaintext $P_1=0x55$:
- $C_1 = 0x55 \oplus 0x9C = 0xC9$
- Decrypt: $0xC9 \oplus 0x9C = 0x55$

### N3) How many AES blocks?
AES block size = 16 bytes.
Message length $L=1000$ bytes.
- Blocks (ceil): $\lceil 1000/16 \rceil = \lceil 62.5 \rceil = 63$ blocks
If using PKCS#7, ciphertext will be 63 blocks (1008 bytes).

---

## 10) How to memorize + solve faster
1) Memorize: ECB pattern leak; CBC uses IV; CTR/GCM require unique nonce.
2) Drill: CTR XOR math and PKCS#7 padding length.

## 11) Exam checklist (Module 06b)
- Explain why ECB is bad.
- Write CBC encryption/decryption formulas.
- Explain CTR keystream idea and nonce reuse danger.
- Know that AES is standard; DES is obsolete; 3DES is legacy.
- Understand why AEAD (like GCM) is preferred for real systems.
