# Module 05 — Block Ciphers and DES (Exam Prep Notes)

## 1) Block ciphers in one sentence
A **block cipher** takes a fixed-size block of plaintext (e.g., 64 or 128 bits) and a key, and outputs a same-size block of ciphertext.

Most practical systems **do not** encrypt “one block once” for long messages; they use a **mode of operation** (CBC/CTR/GCM/etc.).

---

## 2) Feistel networks (the DES design idea)
DES is based on a **Feistel network**, which repeatedly applies a round function.

For each round $i$:
- Split block into left and right halves: $(L_i, R_i)$
- Compute:
  - $L_{i+1} = R_i$
  - $R_{i+1} = L_i \oplus F(R_i, K_i)$

Key point: **Feistel networks are invertible even if $F$ is not**, because decryption can run the same structure with subkeys in reverse order.

### Visual: one Feistel round (what to draw in exam)
```
      +-------------------+
Li ------>|                   |----+-----------------> Ri+1
      |        XOR        |    |
      +-------------------+    |
                   v
                 +--------+
Ri --------------------------->|  F()   |---->
                 |(Ri,Ki)|
                 +--------+
                   ^
                   |
                  Ki

Li+1 = Ri
Ri+1 = Li XOR F(Ri, Ki)
```

---

## 3) DES overview (what to memorize)
- **Block size:** 64 bits
- **Key size (effective):** 56 bits (often written as 64 bits with 8 parity bits)
- **Rounds:** 16
- **Structure:** Feistel network

### Quick reference table (DES)
| Item | Value |
|---|---:|
| Block size | 64 bits |
| Effective key size | 56 bits |
| Rounds | 16 |
| Network type | Feistel |
| S-box mapping | 6 bits → 4 bits |

### Why DES is considered insecure today
56-bit keys are too small → feasible brute-force attacks.

DES is still important to learn because:
- Many concepts (Feistel, S-boxes, key schedule) appear in exams
- 3DES exists historically

---

## 4) DES internals (high-level steps)
You may see these terms:
- **Initial Permutation (IP)** and **Final Permutation (FP)**: fixed bit shuffles.
- **Expansion (E)**: expands 32-bit $R$ to 48 bits.
- XOR with **round subkey** $K_i$ (48 bits).
- **S-boxes**: 8 substitution boxes, each maps 6 bits → 4 bits (total 48 → 32).
- **Permutation (P)**: permutes 32-bit output.

Round function:
$$F(R, K_i) = P(S(E(R) \oplus K_i))$$

### Visual: DES round function pipeline
```
R (32) -> E expansion (48) -> XOR Ki (48)
  -> split into 8 chunks (6 bits each)
  -> S1..S8 (each 6->4) => 32 bits
  -> P permutation (32) -> output of F
```

### S-box lookup (this is usually what students miss)
For each 6-bit chunk: b1 b2 b3 b4 b5 b6
- **Row** = (b1 b6) as a 2-bit number
- **Column** = (b2 b3 b4 b5) as a 4-bit number

Mini-example:
- Input: `101011`
- Row = `11` (3)
- Col = `0101` (5)
- Output = S[row][col] (a 4-bit value)

---

## 5) DES key schedule (what matters)
- Start with 56 effective key bits.
- Generate 16 subkeys $K_1..K_{16}$ (each 48 bits).
- Uses shifts/rotations and selection tables.

Exam-relevant idea: **each round uses a different subkey**.

### Visual: key schedule idea (what to write)
```
64-bit key (with parity)
  -> drop parity / permute (PC-1) -> 56 bits
  -> split: C0 (28) | D0 (28)
  -> left shifts per round -> Ci, Di
  -> select bits (PC-2) -> Ki (48)
```

Left-shift schedule (memorize pattern):
| Round | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 | 11 | 12 | 13 | 14 | 15 | 16 |
|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|
| Shifts | 1 | 1 | 2 | 2 | 2 | 2 | 2 | 2 | 1 | 2 | 2 | 2 | 2 | 2 | 2 | 1 |

---

## 6) 3DES (Triple DES)
Because DES is weak, 3DES applies DES multiple times.

Common form (EDE):
- Encrypt with $K_1$
- Decrypt with $K_2$
- Encrypt with $K_3$

Key sizes (typical):
- 2-key 3DES: effectively 112 bits
- 3-key 3DES: effectively 168 bits

3DES is **much slower** than AES and is largely deprecated for new designs.

---

## 7) Worked examples (solved)
These are simplified examples focusing on the logic you’re tested on.

### Example 1: One Feistel round (toy)
Let’s use small 8-bit halves (not real DES sizes).
- $L_0 = 1100\ 1010$
- $R_0 = 0110\ 0111$
- Define toy round function: $F(R, K) = R \oplus K$
- Let $K_0 = 1010\ 0001$

Compute:
1) $F(R_0, K_0) = 0110\ 0111 \oplus 1010\ 0001 = 1100\ 0110$
2) $L_1 = R_0 = 0110\ 0111$
3) $R_1 = L_0 \oplus F = 1100\ 1010 \oplus 1100\ 0110 = 0000\ 1100$

So after one round:
- $L_1 = 0110\ 0111$
- $R_1 = 0000\ 1100$

**Why this helps:** you can do these XOR steps quickly on exams.

### Example 2: Brute-force feasibility (DES)
DES key length = 56.
If an attacker can try $10^{12}$ keys/sec (fast hardware), worst-case tries $2^{56} \approx 7.2\times 10^{16}$ keys.
Time (worst-case):
$$\frac{7.2\times 10^{16}}{10^{12}} = 7.2\times 10^4 \text{ seconds} \approx 20\text{ hours}$$
Average would be about half.

This illustrates why 56-bit is too small.

### Example 3: Avalanche effect (concept)
If you flip **one bit** of plaintext and encrypt again, a strong cipher should flip about **half** of output bits on average.
DES was designed to have avalanche properties.

### Example 4 (Numerical): Keyspace and brute-force time
Keyspace for DES: $2^{56}$ keys.

If a machine tests $R$ keys/sec, worst-case time:
$$T_{worst} = \frac{2^{56}}{R}$$
Average-case time:
$$T_{avg} = \frac{2^{55}}{R}$$

Worked values:
- If $R = 10^9$ keys/sec:
  - $T_{worst} \approx \frac{7.2\times 10^{16}}{10^9} = 7.2\times 10^7$ sec ≈ 833 days ≈ 2.3 years
  - $T_{avg}$ ≈ 1.15 years

### Example 5 (Numerical): Why 3DES is “bigger” than DES
If a system used 2 independent 56-bit keys, the *naive* keyspace is $2^{112}$.
Real attacks can reduce that (meet-in-the-middle), which is why key-length comparisons can be subtle.

Exam-safe takeaway:
- DES (56) is too small.
- 3DES is stronger but slow/legacy.

---

## 8) Short theory questions (with answers)

### Q1) What is the block size of DES?
**Answer:** 64 bits.

### Q2) Why can Feistel ciphers be decrypted even if the round function is not invertible?
**Answer:** The structure uses XOR and swapping halves so you can reverse rounds with subkeys in reverse order.

### Q3) What is the effective key size of DES?
**Answer:** 56 bits.

### Q4) What do DES S-boxes do?
**Answer:** Substitute 6 bits to 4 bits (non-linear transformation), providing confusion.

### Q5) 3DES is slower than AES—why might it still appear historically?
**Answer:** It extended DES security without redesigning everything, providing backward compatibility.

### Q6) What is the purpose of S-boxes?
**Answer:** Provide nonlinearity (confusion), making attacks harder than simple linear algebra.

### Q7) Why are modes of operation necessary for block ciphers?
**Answer:** A block cipher encrypts one block; modes securely encrypt multi-block messages and prevent pattern leakage.

## 9) Numericals (solved drills)

### N1) Compute one Feistel round quickly
Given (toy 8-bit halves):
- $L_0=0x3C$, $R_0=0xA5$, $K_0=0xF0$, and $F(R,K)=R\oplus K$

Compute:
1) $F=0xA5 \oplus 0xF0 = 0x55$
2) $L_1=R_0=0xA5$
3) $R_1=L_0 \oplus F = 0x3C \oplus 0x55 = 0x69$

Answer: $(L_1,R_1)=(0xA5,0x69)$.

### N2) Brute-force time
DES keyspace $2^{56} \approx 7.2\times 10^{16}$.
If $R=5\times 10^{10}$ keys/sec:
$$T_{worst}=\frac{7.2\times 10^{16}}{5\times 10^{10}}=1.44\times 10^6\text{ sec}$$
Convert: $1.44\times 10^6$ sec ≈ 400 hours ≈ 16.7 days.

### N3) Block count (common exam numeric)
DES block size = 64 bits = 8 bytes.
How many blocks for a 1 KB message (1024 bytes) (ignoring padding)?
$$\frac{1024}{8}=128\text{ blocks}$$

---

## 10) How to memorize + solve faster
1) Memorize the DES table (64/56/16).
2) Practice the Feistel round equations until automatic.
3) Drill brute-force time conversions (sec → hours → days).

## 11) Exam checklist (Module 05)
- Define block cipher and why modes are needed.
- Explain Feistel round equations.
- Memorize DES: 64-bit block, 56-bit key, 16 rounds.
- Explain why DES is insecure today.
- Know what S-boxes contribute (nonlinearity/confusion).
- Know 3DES concept and why it’s deprecated.
