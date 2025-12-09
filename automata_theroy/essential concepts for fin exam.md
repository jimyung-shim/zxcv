Here is **the complete list of “must-know essential concepts” for your automata theory final exam**, extracted *directly* from all the project PDF files you uploaded.
I organized them **exactly the way professors design finals**: definitions, theorems, closure properties, hierarchy, machine power, and undecidability.

I also marked **🔥 SUPER ESSENTIAL (high chance of exam)** items based on typical final-exam patterns.

---

# ✅ **1. Pushdown Automata (Chapter 7)**  

### **Key Definitions**

* Definition of NPDA tuple:
  ( M = (Q, Σ, Γ, δ, q_0, Z, F) )
  (Know domain & range of δ exactly.)
* Instantaneous description (ID): (state, unread-input, stack).
* Acceptance by **final state**.

### **Core Theorems**

* PDA ↔ CFG equivalence

  * **Theorem 7.1**: For any CFL, there exists an NPDA that accepts it.
  * **Theorem 7.2**: If a PDA accepts a language, it is context-free.

🔥 **HIGH PRIORITY**: Steps converting

* CFG → PDA (especially Greibach Normal Form version)
* PDA → CFG (requiring a single final state and stack-empty condition)

### **Deterministic PDA**

* **Definition 7.3** DPDA restrictions:

  1. δ(q, x, A) contains at most one element
  2. If ε-transition exists, no consuming transition allowed.
* Deterministic context-free language = language accepted by DPDA.
* **DPDA < NPDA** (strict).

🔥 **IMPORTANT EXAMPLE**

* Language ( L = { a^n b^n } ∪ { a^n b^{2n} } ) is **CFL but NOT deterministic**.

### **Deterministic Grammars**

* LL(k) grammar definition (lookahead k).
* Concept of s-grammar, LL grammar examples.

---

# ✅ **2. Properties of Context-Free Languages (Chapter 8)**  

### **Pumping Lemma for CFL**

* Statement of Theorem 8.1 (classic 5-part decomposition ( uvxyz )).
* Positions constraints:

  * (|vxy| ≤ p)
  * (|vy| ≥ 1)
* Used to prove non-CFL.

🔥 **Important exam examples**

* Show ( { a^n b^n c^n \mid n ≥ 1 } ) is NOT context-free.
* Show ( { ww \mid w ∈ {0,1}^* } ) is NOT context-free.

### **Linear CFL Pumping Lemma**

* Definition of linear grammar.
* Theorem 8.2 pumping lemma specialized for linear languages.

### **Closure Properties**

* **CFL are closed under:**

  * union
  * concatenation
  * star
* **CFL NOT closed under:**

  * intersection
  * complement
* **CFL ∩ Regular = CFL** (VERY IMPORTANT)

🔥 Must know example:

* Prove language is CFL by intersecting with regular language (Theorem 8.5).

### **Decidable properties**

* Emptiness of CFL: decidable (Theorem 8.6).
* Infiniteness of CFL: decidable (Theorem 8.7 using dependency graph).

---

# ✅ **3. Turing Machines (Chapter 9)**  

### **Definition of a TM**

* Tuple: ( M = (Q, Σ, Γ, δ, q_0, □, F) ).
* Tape infinite in both directions.
* δ(q, a) = (q’, b, L/R).

### **Key Concepts**

* Configuration / Instantaneous description.
* Halting vs infinite loop.
* Acceptance: halts in final state with input on tape.

### **Turing Transducers (TM computing functions)**

* Definition 9.4: TM computes f(x).
* Know how unary addition/multiplication TMs work (example structures).

### **Combining Turing machines**

* Using comparers, adders, erasers.
* Macro-instructions: IF–THEN–ELSE structure.

### **Turing Thesis**

* TM captures all effective computation.

---

# ✅ **4. Other Models of TM (Chapter 10)**  

### **Equivalence of machine models**

All the following are **equivalent to standard TM**:

* TM with Stay-Option
* Multi-track TM
* Semi-infinite tape TM
* Off-line TM
* Multi-tape TM
* Multi-dimensional TM
* Nondeterministic TM

🔥 **VERY IMPORTANT**

* Deterministic TM ≡ Nondeterministic TM (Theorem 10.2).
* Multi-tape TM can be simulated by single-tape TM with only polynomial slowdown.

### **Universal Turing Machine**

* Concept: TM that simulates any TM given ⟨M,w⟩.
* Encoding of TM descriptions.
* Enumeration procedures.

🔥 **Countability results**

* Set of all TMs: countable.
* Set of all languages: uncountable.
* Therefore **some languages are NOT Turing recognizable**.

### **Linear Bounded Automata**

* Definition of LBA.
* LBA ↔ context-sensitive languages.
* CSL ⊂ Recursive.

---

# ✅ **5. Hierarchy & Recursion Theory (Chapter 11)**  

### **Language Classes**

* Recursive
* Recursively enumerable (RE)
* Non-RE languages exist.

🔥 Core relationships:

* Recursive ⊂ RE
* RE − Recursive ≠ ∅
* If L and ¬L are RE ⇒ both are recursive
  (Theorem 11.4)

### **Unrestricted Grammars**

* Generate exactly all RE languages (Theorems 11.6, 11.7).

### **Context-Sensitive Languages**

* CSL ↔ LBA equivalence.
* CSL ⊂ Recursive.
* Recursive is *strictly larger* than CSL.

🔥 **Chomsky Hierarchy**
(know levels, machines, grammars)

---

# ✅ **6. Limits of Computation (Chapter 12)**  

### **Halting Problem**

* Definition 12.1
* Theorem 12.1: halting problem undecidable.

### **Reductions**

* If halting problem were decidable → all RE languages would be recursive.

### **Major Undecidable Problems**

* Emptiness of RE grammar is undecidable.
* Finiteness of TM language is undecidable.
* Ambiguity of CFG undecidable.
* Intersection emptiness of CFLs undecidable.

### **Post Correspondence Problem**

* PCP definition.
* MPCP.
* PCP is undecidable (Theorem 12.7).
* Reduction from halting → PCP.

🔥 MUST KNOW

* PCP tile matching definition
* How reductions work at high level

---

# ✅ **7. Other Models of Computation (Chapter 13)**  

### **Recursive Functions**

* Primitive recursive functions
* Composition
* Primitive recursion
* Ackermann function is total but NOT primitive recursive.

🔥 **lambda/minimization operator**

* μ-recursive functions = computable functions = Turing computable.

### **Post systems**

* Post production structure
* Recursively enumerable ↔ Post system (Theorem 13.6)

### **Markov algorithms**

* Deterministic rewriting system
* RE ↔ Markov algorithms (Theorem 13.7)

### **L-systems**

* Parallel rewriting
* Generates growth-like languages
* Understand example derivation

---

# 🎯 **THE ABSOLUTE BARE MINIMUM YOU MUST MASTER BEFORE THE FINAL**

### **Short 15-item checklist**

1. PDA definition and CFG ↔ PDA (both directions).
2. DPDA restrictions & deterministic CFL concept.
3. CFL Pumping Lemma usage.
4. Closure properties of CFL (union OK, intersection ×).
5. CFL ∩ Regular = CFL.
6. TM formal definition and configurations.
7. TM acceptance and halting/infinite loop distinction.
8. Universal TM + encoding ideas.
9. Countability: TMs countable, languages uncountable.
10. Existence of non-RE languages.
11. Halting problem undecidable.
12. PCP definition & undecidability.
13. Chomsky hierarchy (levels, machines, grammars).
14. LBA ↔ Context-sensitive languages.
15. Recursive vs RE vs non-RE distinctions.

---

If you want, I can make:

* **🔥 A 2-page cheat sheet for instant memorization**, or
* **🔥 A full set of final-exam practice problems with answers**, or
* **🔥 A predicted list of exam questions based on your professor's style**.

Just tell me!
