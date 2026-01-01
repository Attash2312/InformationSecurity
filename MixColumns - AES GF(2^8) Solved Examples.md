# MixColumns — AES $GF(2^8)$ Solved Examples (Exam Drill Sheet)

This file focuses only on **MixColumns** and the **finite-field math** that exams often test.

---

## 1) What MixColumns does (concept)
MixColumns takes each **column** of the AES state (4 bytes) and mixes it to create diffusion.

For a column vector $[a0,a1,a2,a3]^T$, encryption MixColumns computes $[b0,b1,b2,b3]^T$:

|02 03 01 01|   |a0|
|01 02 03 01| × |a1|
|01 01 02 03|   |a2|
|03 01 01 02|   |a3|

All multiplication/addition are in $GF(2^8)$.

---

## 2) The field rules you need
### 2.1 Addition in $GF(2^8)$
Addition is **XOR**.

### 2.2 Multiply by 02 (xtime)
To compute $02 \cdot b$:
- Left shift $b$ by 1 bit
- If the original MSB was 1, XOR with 0x1B

### 2.3 Multiply by 03
$$03\cdot b = (02\cdot b) \oplus b$$

### Fast multiplication cheat-sheet (for inverse MixColumns too)
Compute in layers using xtime:
- $02\cdot b$ = xtime(b)
- $04\cdot b$ = xtime(xtime(b))
- $08\cdot b$ = xtime($04\cdot b$)

Then:
- $09\cdot b = 08\cdot b \oplus b$
- $0B\cdot b = 08\cdot b \oplus 02\cdot b \oplus b$
- $0D\cdot b = 08\cdot b \oplus 04\cdot b \oplus b$
- $0E\cdot b = 08\cdot b \oplus 04\cdot b \oplus 02\cdot b$

---

## 3) Solved mini-examples (multiply by 02 and 03)

### Example 1: $02\cdot 0x57$
- 0x57 = 0101 0111 (MSB=0)
- Shift left → 1010 1110 = 0xAE
So $02\cdot 0x57 = 0xAE$.

### Example 2: $02\cdot 0x83$
- 0x83 = 1000 0011 (MSB=1)
- Shift left → 0000 0110 = 0x06
- XOR 0x1B → 0x06 ⊕ 0x1B = 0x1D
So $02\cdot 0x83 = 0x1D$.

### Example 3: $03\cdot 0x57$
- $02\cdot 0x57 = 0xAE$
- $03\cdot 0x57 = 0xAE ⊕ 0x57 = 0xF9$

### Example 4: $03\cdot 0x83$
- $02\cdot 0x83 = 0x1D$
- $03\cdot 0x83 = 0x1D ⊕ 0x83 = 0x9E$

---

## 4) Full MixColumns worked example (one column)
Let input column bytes be:
- a0=0x57, a1=0x83, a2=0x1A, a3=0xC6

Compute outputs:

### b0
$$b0 = 02a0 ⊕ 03a1 ⊕ 01a2 ⊕ 01a3$$
- 02a0 = 0xAE
- 03a1 = 0x9E
- 01a2 = 0x1A
- 01a3 = 0xC6

XOR:
- 0xAE ⊕ 0x9E = 0x30
- 0x30 ⊕ 0x1A = 0x2A
- 0x2A ⊕ 0xC6 = **0xEC**
So b0 = **0xEC**.

### b1
$$b1 = 01a0 ⊕ 02a1 ⊕ 03a2 ⊕ 01a3$$
We need 02a1 and 03a2.
- 02a1 = 02·0x83 = 0x1D
- 02a2 = 02·0x1A: 0x1A=0001 1010 (MSB=0) → shift = 0x34
- 03a2 = 0x34 ⊕ 0x1A = 0x2E

Now XOR:
- 01a0 = 0x57
- 02a1 = 0x1D
- 03a2 = 0x2E
- 01a3 = 0xC6

Compute:
- 0x57 ⊕ 0x1D = 0x4A
- 0x4A ⊕ 0x2E = 0x64
- 0x64 ⊕ 0xC6 = **0xA2**
So b1 = **0xA2**.

### b2
$$b2 = 01a0 ⊕ 01a1 ⊕ 02a2 ⊕ 03a3$$
We need 02a2 and 03a3.
- 02a2 = 0x34 (from above)
- 02a3 = 02·0xC6:
  - 0xC6=1100 0110 (MSB=1)
  - shift → 1000 1100 = 0x8C
  - XOR 0x1B → 0x8C ⊕ 0x1B = 0x97
- 03a3 = 0x97 ⊕ 0xC6 = 0x51

Now XOR:
- 0x57 ⊕ 0x83 = 0xD4
- 0xD4 ⊕ 0x34 = 0xE0
- 0xE0 ⊕ 0x51 = **0xB1**
So b2 = **0xB1**.

### b3
$$b3 = 03a0 ⊕ 01a1 ⊕ 01a2 ⊕ 02a3$$
We need 03a0 and 02a3.
- 03a0 = (02·0x57) ⊕ 0x57 = 0xAE ⊕ 0x57 = 0xF9
- 02a3 = 0x97 (from above)

Now XOR:
- 0xF9 ⊕ 0x83 = 0x7A
- 0x7A ⊕ 0x1A = 0x60
- 0x60 ⊕ 0x97 = **0xF7**
So b3 = **0xF7**.

**Final output column:** [EC, A2, B1, F7]

---

## 5) Inverse MixColumns (what to know)
Decryption uses a different fixed matrix:

|0E 0B 0D 09|
|09 0E 0B 0D|
|0D 09 0E 0B|
|0B 0D 09 0E|

Many exams only require you to recognize the constants and that decryption uses the inverse matrix.
If your exam requires calculations, you’ll need multiply-by-09/0B/0D/0E in $GF(2^8)$.

Helpful identities:
- 09·b = (08·b) ⊕ b
- 0B·b = (08·b) ⊕ (02·b) ⊕ b
- 0D·b = (08·b) ⊕ (04·b) ⊕ b
- 0E·b = (08·b) ⊕ (04·b) ⊕ (02·b)

And:
- 04·b = 02·(02·b)
- 08·b = 02·(04·b)

---

## 6) Inverse MixColumns numericals (solved)

### Example 1: Compute $09\cdot 0x57$
Steps:
- $02\cdot 0x57 = 0xAE$ (from earlier)
- $04\cdot 0x57 = 02\cdot 0xAE$:
  - 0xAE MSB=1 → shift 0x5C → XOR 0x1B = 0x47
- $08\cdot 0x57 = 02\cdot 0x47$:
  - 0x47 MSB=0 → shift = 0x8E
- $09\cdot 0x57 = 0x8E \oplus 0x57 = 0xD9$
Answer: **0xD9**.

### Example 2: Compute $0E\cdot 0x57$
Use $0E\cdot b = 08\cdot b \oplus 04\cdot b \oplus 02\cdot b$.
- From above: $08=0x8E$, $04=0x47$, $02=0xAE$.
- XOR: 0x8E ⊕ 0x47 = 0xC9; 0xC9 ⊕ 0xAE = 0x67
Answer: **0x67**.

---

## 7) Practice numericals (with answers)

### Q1) In $GF(2^8)$, addition is implemented as what operation?
**Answer:** XOR.

### Q2) How do you compute $03\cdot b$ quickly?
**Answer:** $(02\cdot b) ⊕ b$.

### Q3) What is the purpose of MixColumns?
**Answer:** Diffusion (mix bytes within each column).

### Q4) Which AES round omits MixColumns?
**Answer:** The final encryption round.

### Q5) Compute $02\cdot 0xB7$.
**Answer:** 0x75.

### Q6) Compute $03\cdot 0xB7$.
**Answer:** $(02\cdot 0xB7) \oplus 0xB7 = 0x75 \oplus 0xB7 = 0xC2$.

### Q7) Compute $09\cdot 0x57$.
**Answer:** 0xD9.
