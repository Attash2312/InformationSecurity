# Module 08 — Asymmetric Key Cryptography and RSA (Exam Prep Notes)

## 1) Why asymmetric crypto exists
Symmetric crypto is fast but has a big problem: **how do two parties securely share a secret key** over an insecure network?

Asymmetric crypto solves this using a **key pair**:
- **Public key**: shared with everyone
- **Private key**: kept secret

Main uses:
- **Key exchange** / key transport (establish a symmetric session key)
- **Digital signatures** (integrity + authenticity + non-repudiation)

In practice:
- Use asymmetric crypto to set up trust/keys
- Use symmetric crypto (AES) to encrypt the bulk data

---

## 2) Core asymmetric concepts
### 2.1 One-way trapdoor function
Easy to compute one direction, hard to reverse unless you have a “trapdoor” (private key).

### 2.2 Public key encryption vs digital signatures
- **Public key encryption**: anyone can encrypt to you using your public key; only you decrypt using your private key.
- **Digital signature**: you sign with your private key; anyone verifies with your public key.

This “direction” is a common exam trick.

### Visual: which key is used for which goal (exam table)
| Goal | Sender uses | Receiver uses | What you write in exam |
|---|---|---|---|
| Confidentiality | Receiver **public** key (encrypt) | Receiver **private** key (decrypt) | “Encrypt with receiver+, decrypt with receiver−.” |
| Integrity | Sender **private** key (sign hash) | Sender **public** key (verify) | “Sign with sender−, verify with sender+.” |
| Authentication | Sender **private** key (signature proves origin) | Sender **public** key (verify) | “Verification proves it came from sender.” |
| Non-repudiation | Sender **private** key (only owner can sign) | Sender **public** key (verify) | “Sender cannot deny signing.” |

### Visual: PGP / hybrid encryption (encrypt + sign)
```
Sender:
  M -> hash -> sign with sender private  -> signature
  (M || signature) --sym-encrypt with session key Ks--> ciphertext
  Ks --encrypt with receiver public--> encrypted Ks

Receiver:
  encrypted Ks --decrypt with receiver private--> Ks
  ciphertext --sym-decrypt with Ks--> (M || signature)
  verify signature using sender public
```

---

## 3) RSA overview (what to memorize)
RSA is based on the difficulty of factoring large integers.

Notation:
- Choose primes $p$ and $q$
- Compute $n = pq$ (the modulus)
- Compute Euler’s totient: $\varphi(n) = (p-1)(q-1)$
- Choose public exponent $e$ such that $\gcd(e,\varphi(n))=1$
- Compute private exponent $d$ such that:
  $$ed \equiv 1 \pmod{\varphi(n)}$$

Keys:
- Public key: $(n, e)$
- Private key: $d$ (and often $p,q$ kept too)

Encryption:
$$c \equiv m^e \pmod{n}$$
Decryption:
$$m \equiv c^d \pmod{n}$$

### RSA formula sheet (numericals)
| Quantity | Formula |
|---|---|
| Modulus | $n=pq$ |
| Totient | $\varphi(n)=(p-1)(q-1)$ |
| Public exponent condition | $\gcd(e,\varphi(n))=1$ |
| Private exponent | $d=e^{-1}\pmod{\varphi(n)}$ |
| Encrypt | $c=m^e \bmod n$ |
| Decrypt | $m=c^d \bmod n$ |

### Exam recipe: how to solve RSA key questions (fast)
1) Compute $n=pq$.
2) Compute $\varphi(n)=(p-1)(q-1)$.
3) Check $\gcd(e,\varphi(n))=1$ (otherwise **invalid e**, no inverse).
4) Find $d=e^{-1}\bmod \varphi(n)$ using Extended Euclid.
5) If asked to encrypt/decrypt: use square-and-multiply.

---

## 4) RSA worked example (small numbers)
Real RSA uses huge primes; exams may use small primes for hand calculation.

### Step 1: Choose primes
Let:
- $p=11$, $q=17$
- $n = pq = 187$
- $\varphi(n)=(11-1)(17-1)=10\cdot 16=160$

### Step 2: Choose public exponent $e$
Pick $e=7$.
Check $\gcd(7,160)=1$ ✅

### Step 3: Find private exponent $d$
We need $d$ such that:
$$7d \equiv 1 \pmod{160}$$
Solve: $7d = 1 + 160k$.
Try $k=3$: $1+480=481$. $481/7=68.714$ not integer.
Try $k=4$: $1+640=641$. $641/7=91.571$ not integer.
Try $k=5$: $1+800=801$. $801/7=114.428$ not integer.
Try $k=6$: $1+960=961$. $961/7=137.285$ not integer.
Try $k=7$: $1+1120=1121$. $1121/7=160.142$ not integer.
Try $k=8$: $1+1280=1281$. $1281/7=183$ ✅
So $d=183$.

#### Faster method (recommended for exams): Extended Euclidean Algorithm
To find $d=e^{-1} \bmod \varphi(n)$, use extended Euclid on $(e,\varphi(n))$.
It’s faster than trial-and-error.

Public key: $(n=187, e=7)$
Private key: $d=183$

### Step 4: Encrypt a message
Let message $m=8$ (must be < n).
Compute:
$$c = 8^7 \bmod 187$$
Compute using modular reduction:
- $8^2 = 64$
- $8^4 = 64^2 = 4096 \bmod 187$
  - $187\cdot 21=3927$, remainder $4096-3927=169$
  - so $8^4 \equiv 169$
- $8^7 = 8^4 \cdot 8^2 \cdot 8$
  - $\equiv 169 \cdot 64 \cdot 8 \bmod 187$
  - First: $169\cdot 64 = 10816 \bmod 187$
    - $187\cdot 57=10659$, remainder $157$
  - Then: $157\cdot 8 = 1256 \bmod 187$
    - $187\cdot 6=1122$, remainder $134$
So ciphertext $c=134$.

### Step 5: Decrypt
Compute:
$$m = 134^{183} \bmod 187$$
This is big; in real systems computers do fast modular exponentiation.
In exam settings you might not be asked to fully compute this, but conceptually:
- Decryption recovers $m=8$.

### Example 2 (Numerical): Find modular inverse using extended Euclid
Let $\varphi(n)=160$ and $e=7$. Find $d$ such that $7d\equiv 1\pmod{160}$.

Euclid:
- $160 = 7\cdot 22 + 6$
- $7 = 6\cdot 1 + 1$
- $6 = 1\cdot 6 + 0$

Back-substitute:
- $1 = 7 - 6\cdot 1$
- $6 = 160 - 7\cdot 22$
So:
$$1 = 7 - (160 - 7\cdot 22) = 7\cdot 23 - 160$$
Thus $7\cdot 23 \equiv 1\pmod{160}$, so $d=23$ is an inverse.

Note: This differs from the earlier $d=183$ because inverses are modulo 160:
- $183\equiv 23 \pmod{160}$
Both are valid.

### Visual: Extended Euclid as a table (easy to write in exam)
For inverse of $e$ mod $\varphi$:
1) Do Euclid remainders.
2) Back-substitute to express 1 as a combination of $e$ and $\varphi$.

Template table:
| Step | r (remainder) | q (quotient) | equation |
|---:|---:|---:|---|
| 1 | $r_0=\varphi$ |  | $r_0 = q_1 r_1 + r_2$ |
| 2 | $r_1=e$ | $q_1$ | $r_1 = q_2 r_2 + r_3$ |
| … | … | … | … |

Back-substitute until you get $1 = s\cdot \varphi + t\cdot e$.
Then $t$ (mod $\varphi$) is the inverse $d$.

---

## 5) Digital signatures (concept + solved miniature example)
### Concept
To sign message $m$:
$$s \equiv m^d \pmod{n}$$
To verify signature $s$:
$$m \stackrel{?}{\equiv} s^e \pmod{n}$$

In real life you sign a **hash** of the message, not the whole message.

### Tiny demonstration using our RSA numbers
Using $(n=187, e=7, d=183)$ and message $m=8$:
- Signature: $s = 8^{183} \bmod 187$ (large)
- Verification: compute $s^7 \bmod 187$ → should return 8

Again: actual systems use padding schemes (below).

### Example 3 (Numerical): RSA encrypt/decrypt with very small numbers
Let $p=5, q=11$.
- $n=55$, $\varphi(n)=40$
Choose $e=3$ (since $\gcd(3,40)=1$).
Find $d$ such that $3d\equiv 1\pmod{40}$.
- $3\cdot 27=81\equiv 1\pmod{40}$ so $d=27$.

Encrypt $m=7$:
- $c=7^3\bmod 55=343\bmod 55=13$
Decrypt:
- Need $m=13^{27}\bmod 55$.
Use fast powers:
  - $13^2=169\bmod 55=4$
  - $13^4=4^2=16$
  - $13^8=16^2=256\bmod 55=36$
  - $13^{16}=36^2=1296\bmod 55=31$
  - $13^{27}=13^{16}\cdot 13^8\cdot 13^2\cdot 13^1$
    - $31\cdot 36=1116\bmod 55=16$
    - $16\cdot 4=64\bmod 55=9$
    - $9\cdot 13=117\bmod 55=7$
So decrypted $m=7$ ✅

This style (square-and-multiply) is very exam-friendly.

### Visual: square-and-multiply (fast exponent) layout
To compute $a^k\bmod n$:
1) Write $k$ in binary.
2) Square (mod n) each step; multiply only when the bit is 1.

Mini-template:
| Bit (MSB→LSB) | Action | Current value (mod n) |
|---|---|---|
| 1 | start with a | … |
| next bit | square | … |
| if bit=1 | multiply by a | … |

---

## 6) RSA padding (very important for exams)
Raw RSA is not safe by itself.
- For encryption: use **OAEP** (RSAES-OAEP)
- For signatures: use **PSS** (RSASSA-PSS)

Why padding matters:
- Prevents deterministic encryption (same message always encrypts to same ciphertext)
- Protects against chosen-ciphertext/signature forgeries

Exam statement you can use:
- “RSA should be used with standardized padding (OAEP/PSS), not raw.”

---

## 7) Key sizes (general guidance)
Key sizes evolve over time, but typical modern guidance:
- RSA 2048-bit is common baseline
- RSA 3072-bit for longer-term security goals

(Exact requirements depend on policy/industry.)

---

## 8) Public Key Infrastructure (PKI) basics
### Certificates
A **certificate** binds a public key to an identity.
- Signed by a **Certificate Authority (CA)**

### Chain of trust
Browser/OS trusts root CAs → intermediate CAs → end-entity certificates.

### Revocation
- CRL (Certificate Revocation List)
- OCSP (Online Certificate Status Protocol)

---

## 9) Common asymmetric algorithms (besides RSA)
- **Diffie–Hellman (DH)** / **ECDH**: key exchange
- **DSA/ECDSA/EdDSA**: digital signatures
- ECC (elliptic curve cryptography) generally offers smaller keys for similar security.

---

## 10) Practice questions (with solutions)

### Q1) In RSA, what is $n$?
**Answer:** $n=pq$ is the modulus used in both public and private keys.

### Q2) In RSA, what equation defines the private exponent $d$?
**Answer:** $ed \equiv 1 \pmod{\varphi(n)}$.

### Q3) If Alice wants confidentiality when sending to Bob, which key should she use to encrypt?
**Answer:** Bob’s **public key**.

### Q4) If Bob wants to prove he authored a message, which key does he use to sign?
**Answer:** Bob’s **private key**.

### Q5) Name safe padding for RSA encryption and RSA signatures.
**Answer:** OAEP for encryption, PSS for signatures.

### Q6) Why don’t we use RSA to encrypt large files directly?
**Answer:** It’s slow and size-limited; instead RSA establishes a symmetric key and AES encrypts the data.

## 11) Numericals (solved drills)

### N1) Compute $\varphi(n)$
If $p=13$ and $q=19$:
- $n=247$
- $\varphi(n)=(13-1)(19-1)=12\cdot 18=216$

### N2) Check if an $e$ is valid
If $\varphi(n)=216$, is $e=6$ valid?
- $\gcd(6,216)=6\ne 1$ → **not valid**.

### N3) Quick modular exponent
Compute $4^{5}\bmod 13$:
- $4^2=16\bmod 13=3$
- $4^4=3^2=9$
- $4^5=9\cdot 4=36\bmod 13=10$
Answer: **10**.

---

## 12) How to memorize + solve faster
1) Memorize RSA pipeline: $p,q\to n,\varphi(n)\to e\to d\to$ encrypt/decrypt.
2) Drill extended Euclid for modular inverse.
3) Drill square-and-multiply for modular exponent.

## 13) Exam checklist (Module 08)
- Explain why asymmetric crypto is needed (key distribution + signatures).
- Memorize RSA steps: choose primes, compute $n$ and $\varphi(n)$, choose $e$, compute $d$.
- Know the difference between encryption and signatures (which key is used).
- Mention OAEP and PSS for real RSA safety.
- Understand certificates/CA chain at a high level.
