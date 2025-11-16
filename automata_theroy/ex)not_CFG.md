Great — here are **clear, textbook-style examples** of productions that **are NOT context-free grammar (CFG)**.

Remember:

### ✅ A context-free grammar allows ONLY rules of the shape:

[
A \to \alpha
]
where **A is a single nonterminal**, and **α is any string of terminals/nonterminals**.

---

# ❌ **1. Left-hand side has more than one symbol**

These are **NOT** context-free:

### Example 1

[
AB \to aB
]
(Left side contains two nonterminals → **context-sensitive**)

### Example 2

[
aA \to Bb
]
(Left side contains terminal + nonterminal → **not allowed in CFG**)

### Example 3

[
XYC \to a
]
(Three symbols on the left → **not CFG**)

---

# ❌ **2. Context-dependent rules (LHS has surrounding symbols)**

These appear in **context-sensitive** grammars:

### Example 4

[
A B C \to A D C
]
You can replace **B only when surrounded by A and C** → not context-free.

### Example 5

[
aBb \to aaBb
]
Again, the LHS is longer than one symbol → **not context-free**.

---

# ❌ **3. Contracting or unrestricted grammar rules**

These belong to **unrestricted (Type-0)** grammars:

### Example 6

[
ab \to \epsilon
]
CFG **never** allows terminals on LHS.

### Example 7

[
a \to AA
]
LHS must be a **nonterminal**.
A terminal cannot appear on the left → **not context-free**.

---

# ❌ **4. Rules that try to “rewrite context”**

These are patterns from context-sensitive languages:

### Example 8

[
A B \to B A
]
Reordering 2 symbols at once → **not context-free**.

### Example 9

[
B C D \to E F
]
Left side has multiple symbols → not allowed.

---

# ❌ **5. Productions trying to “check equality among three parts”**

Example from a grammar attempting to generate (a^n b^n c^n):

### Example 10

[
S \to a S b c
]
This *looks* context-free syntactically — but such a grammar **cannot generate** (a^n b^n c^n).
(Important point: **syntactically allowed** but **not sufficient** to describe the language.)

But this rule **alone** is still CFG.
I include it to show that *even if allowed*, it may still fail to represent the language.

---

# ⭐ **Summary Table**

| Production (example) | Context-Free? | Reason                                |
| -------------------- | ------------- | ------------------------------------- |
| (A \to aBC)          | ✔ Yes         | Single nonterminal on LHS             |
| (AB \to a)           | ❌ No          | LHS has 2 symbols                     |
| (aA \to B)           | ❌ No          | Terminal on LHS                       |
| (ABC \to ADC)        | ❌ No          | Context-sensitive                     |
| (A \to \epsilon)     | ✔ Yes         | CFG allows ε (except CNF restriction) |
| (AB \to CD)          | ❌ No          | LHS has >1 symbol                     |
| (a \to A)            | ❌ No          | Terminal on LHS                       |

---

If you want, I can:

✅ Generate a quiz testing whether a rule is CFG or not
✅ Show examples of regular grammar vs CFG vs CSG rules
✅ Give you a diagram showing the Chomsky hierarchy (Type 0–3)

Just tell me!
