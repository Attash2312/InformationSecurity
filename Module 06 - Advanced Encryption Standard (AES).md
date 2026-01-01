# Module 06 — Advanced Encryption Standard (AES) (Exam Prep Notes)

## 1) What AES is
**AES** is the modern standard symmetric-key block cipher used widely (TLS, VPNs, disk encryption, Wi‑Fi security, etc.).

Key facts to memorize:
- **Block size:** 128 bits
- **Key sizes:** 128 / 192 / 256 bits
- **Rounds:** 10 / 12 / 14 (for 128/192/256-bit keys)
- **Structure:** Substitution–Permutation Network (not Feistel)

### Quick reference table (AES)
| Key size | Rounds | Notes |
|---:|---:|---|
| 128 | 10 | most common baseline |
| 192 | 12 | stronger than 128 |
| 256 | 14 | strongest standard option |

---

## 2) AES data representation (State)
AES arranges a 128-bit block into a **4×4 matrix of bytes** called the **state**:

- 16 bytes total
- Often filled column-by-column

You don’t always need to memorize the exact fill order, but you should understand:
- Operations act on bytes, rows, and columns of this state.

### Visual: how the 16 bytes fill the 4×4 state (common exam expectation)
If the input bytes are $b_0..b_{15}$, AES typically fills **column-wise**:

|   | Col0 | Col1 | Col2 | Col3 |
|---|---|---|---|---|
| Row0 | $b_0$ | $b_4$ | $b_8$  | $b_{12}$ |
| Row1 | $b_1$ | $b_5$ | $b_9$  | $b_{13}$ |
| Row2 | $b_2$ | $b_6$ | $b_{10}$ | $b_{14}$ |
| Row3 | $b_3$ | $b_7$ | $b_{11}$ | $b_{15}$ |

This matters because **ShiftRows works on rows** and **MixColumns works on columns**.

---

## 3) AES round structure (AES-128)
AES-128 performs:
- **Initial round:** AddRoundKey
- **Rounds 1–9:** SubBytes → ShiftRows → MixColumns → AddRoundKey
- **Final round (round 10):** SubBytes → ShiftRows → AddRoundKey (no MixColumns)

### The four core transformations
1) **SubBytes**: byte-by-byte substitution using an S-box (nonlinear).
2) **ShiftRows**: rotates rows left by 0,1,2,3 bytes.
3) **MixColumns**: mixes each column using math in $GF(2^8)$ (diffusion).
4) **AddRoundKey**: XOR with round key (key mixing).

### Visual: one full round (what to sketch)
```
State (4x4 bytes)
  | SubBytes   (S-box lookup per byte)
  v
State
  | ShiftRows  (rotate rows)
  v
State
  | MixColumns (matrix multiply in GF(2^8))   [skip in final round]
  v
State
  | AddRoundKey (XOR round key)
  v
Next State
```

### SubBytes lookup (how to do S-box questions)
If a byte is `0xAB`:
- Row = high nibble `A`
- Column = low nibble `B`
- Output = AES_SBOX[A][B]

This “row/col from hex nibbles” is the exact style exams use.

Known quick-check example many teachers use:
- `S(0x53) = 0xED` (useful sanity check when practicing)

### Mini-figure: round flow (encryption)
```
AddRoundKey
  |
  v
(SubBytes -> ShiftRows -> MixColumns -> AddRoundKey) x 9
  |
  v
SubBytes -> ShiftRows -> AddRoundKey
```

---

## 4) Key schedule (high-level)
AES expands the original key into **round keys**.
Concepts you may see:
- **RotWord** (rotate bytes)
- **SubWord** (apply S-box)
- **Rcon** (round constants)

Exam idea: round keys are derived deterministically from the original key, but they are different per round.

### Visual: AES-128 key expansion (words)
AES-128 treats the key as 4 words ($w_0..w_3$), each 4 bytes.
It expands to 44 words ($w_0..w_{43}$) for 11 round keys.

Rule pattern (AES-128):
- If $i$ is a multiple of 4:
  $$w_i = w_{i-4} \oplus g(w_{i-1})$$
- Else:
  $$w_i = w_{i-4} \oplus w_{i-1}$$

Where:
$$g(w)=SubWord(RotWord(w)) \oplus Rcon$$

**g() diagram (exam-friendly):**
```
w (4 bytes)
  -> RotWord  (rotate left by 1 byte)
  -> SubWord  (S-box on each byte)
  -> XOR Rcon (only on first byte)
  = g(w)
```

**How to answer “find Round-1 key”**
1) Write $w_0..w_3$ from the 16-byte key.
2) Compute $g(w_3)$ using RotWord→SubWord→Rcon.
3) $w_4=w_0\oplus g(w_3)$, then chain XORs to get $w_5,w_6,w_7$.
4) Round-1 key is $w_4||w_5||w_6||w_7$.

---

## 5) $GF(2^8)$ (the math behind MixColumns)
MixColumns treats each column as a 4-byte vector and multiplies by a fixed matrix.

Common exam focus: multiplying by **02** and **03** in $GF(2^8)$.

Rules (byte operations):
- Multiply by 02: left shift by 1; if the original byte had MSB=1, XOR with 0x1B (reduction).
- Multiply by 03: $(02 \cdot b) \oplus b$.

### Step-by-step recipe (numericals): multiply by 02 and 03
To compute $02\cdot b$:
1) Write $b$ in hex.
2) Check MSB (is $b\ge 0x80$?).
3) Left shift one bit (drop overflow) → $b'$
4) If MSB was 1, do $b' \oplus 0x1B$.
To compute $03\cdot b$: $(02\cdot b) \oplus b$.

---

## 6) Worked examples (solved)

### Example 1: AddRoundKey (XOR) on one byte
If a state byte is $0x3C$ and the round key byte is $0xA9$:
- Output = $0x3C \oplus 0xA9 = 0x95$

Binary check:
- 0x3C = 0011 1100
- 0xA9 = 1010 1001
- XOR  = 1001 0101 = 0x95

### Example 2: ShiftRows (conceptual)
Suppose row 2 of the state is:
- Row2: [b0, b1, b2, b3]
ShiftRows shifts:
- Row0 by 0: [b0, b1, b2, b3]
- Row1 by 1: [b1, b2, b3, b0]
- Row2 by 2: [b2, b3, b0, b1]
- Row3 by 3: [b3, b0, b1, b2]

**Visual (before → after)**
| Row | Before | After |
|---:|---|---|
| 0 | [b0, b1, b2, b3] | [b0, b1, b2, b3] |
| 1 | [b0, b1, b2, b3] | [b1, b2, b3, b0] |
| 2 | [b0, b1, b2, b3] | [b2, b3, b0, b1] |
| 3 | [b0, b1, b2, b3] | [b3, b0, b1, b2] |

### Example 3: Multiply by 02 in $GF(2^8)$ (typical exam calc)
Compute $02 \cdot 0x57$.
- 0x57 = 0101 0111 (MSB=0)
- Left shift → 1010 1110 = 0xAE
So $02 \cdot 0x57 = 0xAE$.

Compute $02 \cdot 0x83$.
- 0x83 = 1000 0011 (MSB=1)
- Left shift → 0000 0110 = 0x06
- XOR with 0x1B → 0x06 \oplus 0x1B = 0x1D
So $02 \cdot 0x83 = 0x1D$.

### Example 4: Multiply by 03 in $GF(2^8)$
Compute $03 \cdot 0x57$.
- $03\cdot b = (02\cdot b) \oplus b$
- From above, $02\cdot 0x57 = 0xAE$
- So $03\cdot 0x57 = 0xAE \oplus 0x57 = 0xF9$

### Example 5: One MixColumns output byte (full calculation)
MixColumns uses the matrix:

|02 03 01 01|
|01 02 03 01|
|01 01 02 03|
|03 01 01 02|

Let a column be bytes: [a0, a1, a2, a3].
First output byte:
$$b0 = 02\cdot a0 \oplus 03\cdot a1 \oplus 01\cdot a2 \oplus 01\cdot a3$$

Take example column:
- a0=0x57, a1=0x83, a2=0x1A, a3=0xC6

Compute pieces:
- $02\cdot a0 = 02\cdot 0x57 = 0xAE$
- $03\cdot a1 = (02\cdot 0x83) \oplus 0x83 = 0x1D \oplus 0x83 = 0x9E$
- $01\cdot a2 = 0x1A$
- $01\cdot a3 = 0xC6$

Now XOR them:
- $b0 = 0xAE \oplus 0x9E \oplus 0x1A \oplus 0xC6$
- 0xAE ⊕ 0x9E = 0x30
- 0x30 ⊕ 0x1A = 0x2A
- 0x2A ⊕ 0xC6 = 0xEC

So **b0 = 0xEC**.

This is a common style of exam calculation.

### Example 6 (Numerical): MixColumns full column output (quick recap)
If your exam asks for the whole column, compute four equations:
$$\begin{aligned}
b0 &= 02a0\oplus 03a1\oplus a2\oplus a3\\
b1 &= a0\oplus 02a1\oplus 03a2\oplus a3\\
b2 &= a0\oplus a1\oplus 02a2\oplus 03a3\\
b3 &= 03a0\oplus a1\oplus a2\oplus 02a3
\end{aligned}$$

See the full worked column in the dedicated MixColumns drill sheet.

---

## 7) AES security notes (exam-friendly)
- AES is considered secure when used correctly.
- Most real-world failures come from:
  - Bad modes (e.g., ECB)
  - Reused IV/nonces
  - Weak key management
  - Side-channel leakage (timing/power)

---

## 8) Short theory questions (with answers)

### Q1) AES block size is ____.
**Answer:** 128 bits.

### Q2) AES-256 has how many rounds?
**Answer:** 14.

### Q3) Which AES step provides nonlinearity/confusion?
**Answer:** SubBytes (S-box).

### Q4) Why is MixColumns skipped in the final round?
**Answer:** It’s part of AES design; encryption/decryption symmetry is handled differently, and final-round structure still ensures security while simplifying inversion properties.

### Q5) How do you compute $03 \cdot b$ in $GF(2^8)$?
**Answer:** $(02\cdot b) \oplus b$.

## 9) Numericals (solved drills)

### N1) Multiply-by-02 drill
Compute $02\cdot 0x6D$.
- 0x6D MSB=0 → shift left: 0xDA
Answer: **0xDA**.

### N2) Multiply-by-02 with reduction
Compute $02\cdot 0xB7$.
- 0xB7 MSB=1
- shift: 0x6E
- reduce: 0x6E ⊕ 0x1B = 0x75
Answer: **0x75**.

### N3) Multiply-by-03 drill
Compute $03\cdot 0x6D$.
- $02\cdot 0x6D = 0xDA$
- $03\cdot 0x6D = 0xDA ⊕ 0x6D = 0xB7$
Answer: **0xB7**.

### N4) AddRoundKey drill
If state byte = 0x7F and key byte = 0x2A:
- output = 0x7F ⊕ 0x2A = **0x55**

---

## 10) How to memorize + solve faster
1) Memorize: AES block=128; rounds 10/12/14.
2) Drill xtime (×02) until it’s automatic.
3) For MixColumns, remember “03 = 02 ⊕ 01”.

## 11) Exam checklist (Module 06)
- Memorize AES: 128-bit block; 128/192/256-bit keys; 10/12/14 rounds.
- Know the round order and what changes in the final round.
- Know what each transformation does conceptually.
- Be able to do quick GF(2^8) multiply-by-02 and multiply-by-03.
- Explain why incorrect mode/nonce reuse can break security even if AES itself is strong.
