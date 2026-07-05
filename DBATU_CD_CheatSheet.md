# DBATU Compiler Design (BTCOC601) — Final Day Cheat Sheet

*Quick recall only — read the full plan for exam-answer format. Ordered by probability.*

---

### 1. Compiler Phases + Tools ★★★★★
- Compiler = translator, high-level → machine code
- 6 phases: Lexical → Syntax → Semantic → Intermediate → Optimization → Code Gen
- Symbol table + error handler support ALL phases
- Lexical = tokens, Syntax = parse tree, Semantic = type check
- Tools: Lex, Yacc, LLVM, ANTLR
- TAC = Three Address Code (intermediate form)
- **Trick:** "Lazy Students Study Intermediate Optimization Code"

---

### 2. Left Recursion Elimination ★★★★★
- Left recursion: A → Aα | β (A calls itself first)
- Problem: infinite loop in top-down parsers
- Formula: A → βA' , A' → αA' | ε
- Apply to E and T (both left recursive); F is already fine
- Always add ε as one of the options for the new non-terminal
- Direct recursion = same rule; Indirect = through another non-terminal
- **Trick:** "Aage jo bacha (β) pehle likho, peeche jo tha (α) naye non-terminal ke andar daal do, aur ε mat bhoolo."

---

### 3. FIRST/FOLLOW + LL(1) Table ★★★★★
- FIRST = terminals that can start a derivation
- FOLLOW = terminals that can come right after a non-terminal
- Start symbol always has `$` in FOLLOW
- If ε ∈ FIRST(A), production also goes in FOLLOW-based table entries
- LL(1) table: rows = non-terminals, columns = terminals + $
- Two entries in one cell = grammar is NOT LL(1)
- **Trick:** "FIRST dekhta hai shuruaat, FOLLOW dekhta hai baad ki baat."

---

### 4. Type Checking & Conversion ★★★★☆
- Type checking = verifying operand type compatibility
- Happens in Semantic Analysis phase
- Static = compile-time (C, Java); Dynamic = run-time (Python)
- Implicit conversion = automatic (coercion)
- Explicit conversion = manual (type casting)
- No valid conversion → type error
- **Trick:** "Compiler khud kare = Implicit, Programmer khud kare = Explicit."

---

### 5. Code Generation + Registers ★★★★☆
- Code generation = last phase, TAC → machine code
- Uses Register Descriptor (what's in each register) + Address Descriptor (where variable is)
- 4 register uses: loop variables, temporary values, base register, index register
- Register access >> memory access in speed
- Register spilling = problem when registers run out
- **Trick:** "LTBI" — Loop variable, Temporary value, Base register, Index register

---

### 6. Lexical Analysis (Token/Lexeme/Pattern) ★★★★★
- Lexeme = actual text; Token = category; Pattern = rule (regex)
- Lexical analyzer removes whitespace/comments
- Output: token stream `<token-name, attribute-value>`
- Identifiers go into symbol table here
- Tool: Lex/Flex generates lexical analyzers from regex
- **Trick:** "Lexeme dikhta hai, Token bolta hai kaun hai, Pattern batata hai kaise bana."

---

### 7. Symbol Table ★★★★☆
- Stores: name, type, scope, address, size
- Two main operations: insert() and lookup()
- Best implementation: hash table (O(1) average)
- Created in lexical analysis, used by all later phases
- Helps in type checking, scoping, and code generation
- **Trick:** "Symbol Table = School Register of Compiler"

---

### 8. Code Optimization + DAG ★★★★☆
- Optimization = faster/smaller code, same output
- Types: local, global, common sub-expr elimination, dead code elimination, loop optimization, constant folding, strength reduction
- DAG built for one basic block at a time
- Shared nodes in DAG = common sub-expressions (redundant code)
- **Trick:** "DAG = Duplicate Andar Gayab"

---

### 9. LR Parsing (SLR Table) ★★★★★
- LR = Left-to-right scan, Rightmost derivation in reverse
- Always augment grammar first: S' → S
- Dot (.) in item shows parsing progress
- Shift = push input symbol; Reduce = replace RHS with LHS using a production
- Reduce action added for all terminals in FOLLOW(A) — that's what makes it "SLR"
- Accept happens only when S'→S. is reached with $ as lookahead
- **Trick:** "A-I-T-P" — Augment → Items (closure+goto) → Table (Action+Goto) → Parse

---

### 10. Left Factoring ★★★★☆
- Left factoring: A → αβ1 | αβ2 (common prefix α)
- Formula: A → αA' , A' → β1 | β2
- Classic example: if-then-else grammar (S → iEtS | iEtSeS | a)
- Goal: remove ambiguity for top-down parser decision-making
- Different from left recursion (self-reference vs shared prefix)
- **Trick:** "Common shuruaat nikalo bahar, baaki sab naye A' ke andar."

---

### 11. Ambiguous Grammar ★★★☆☆
- Ambiguous = more than one parse tree for same string
- Classic example: E → E+E | E*E | id
- Proof requires showing 2 different parse trees
- Resolved by: rewriting grammar with precedence levels, OR precedence/associativity declarations
- Dangling-else is a famous real-world ambiguity example
- **Trick:** "Ek string, do trees = Ambiguous. Ek string, ek tree = Safe."

---

### 12. Peephole Optimization ★★★☆☆
- Peephole = small window, machine-dependent, local optimization
- Techniques: redundant instruction elimination, unreachable code removal, algebraic simplification, strength reduction, machine idioms
- Applied as a final pass on target code
- Example: x = x+0 gets removed entirely
- **Trick:** "RASU-M" — Redundant elimination, Algebraic simplification, Strength reduction, Unreachable code, Machine idioms

---

### 13. Symbol Table — Functions/Implementation/Applications ★★★★☆
- Functions: store, verify, type-check, scope, address, duplicate detection
- Implementation: array (O(n)), sorted array (O(log n)), hash table (O(1) avg) — hash table is best
- Used across: lexical, semantic, code generation phases
- Applications: type checking, scope resolution, memory allocation, error detection
- **Trick:** "SVTSMD" — Store, Verify, Type-check, Scope, Memory address, Duplicate detection

---

### 14. Compiler Errors — Lexical/Syntax/Semantic/Logical ★★★★☆
- Lexical error = bad token/character (caught by lexical analyzer)
- Syntax error = grammar violation (caught by parser)
- Semantic error = type/meaning issue (caught by semantic analyzer)
- Logical error = compiles fine, wrong output (NOT caught by compiler)
- Order of detection: Lexical → Syntax → Semantic → (Logical found only at runtime)
- **Trick:** "LSSL" — Lexical, Syntax, Semantic, Logical (in detection order)

---

### 15. Predictive Parsing (LL(1) Parser Working) ★★★★☆
- LL(1) = Left-to-right scan, Leftmost derivation, 1 lookahead
- Uses stack + input buffer + LL(1) table
- Match terminal = pop & advance; non-terminal = expand using table
- Push production symbols in REVERSE order onto stack
- Accept when both stack and input reach `$`
- **Trick:** "Stack Top se Match karo, ya Table se Expand karo — jab tak dono $ pe na aa jaye."

---

### 16. Differentiate FIRST/FOLLOW + Table Construction ★★★★☆
- FIRST = what can start a derivation from A
- FOLLOW = what can come right after A
- FIRST computed for any symbol; FOLLOW only for non-terminals
- ε can be in FIRST, never in FOLLOW
- Table rule: FIRST(α) → normal entries; ε in FIRST(α) → also use FOLLOW(A)
- **Trick:** "FIRST = Andar dekho, FOLLOW = Bahar dekho."

---

### 17. Operator Precedence Parsing ★★★★☆
- Works only on operator grammars (no adjacent non-terminals, no ε-productions)
- 3 relations: ⋖ (shift), ⋗ (reduce), ≐ (equal, shift — usually brackets)
- Simpler than full LR table but less powerful
- Table built based on operator precedence + associativity
- **Trick:** "⋖ = Shift (chhota, aage badho), ⋗ = Reduce (bada, wapas simplify karo)."

---

### 18. LR(0) vs SLR(1) vs CLR(1) vs LALR(1) ★★★★★
- 4 variants: LR(0) < SLR(1) < LALR(1) ≤ CLR(1) in power
- LR(0): no lookahead
- SLR(1): uses FOLLOW set
- CLR(1): per-item specific lookahead, most powerful, largest table
- LALR(1): merges CLR states with same core → practical, most widely used (YACC)
- **Trick:** Power order — LR(0) → SLR → LALR → CLR (increasing sophistication)

---

### 19. Syntax Tree vs DAG ★★★★☆
- Syntax tree: duplicates common sub-expressions
- DAG: shares/merges identical sub-expressions into one node
- Both built from expressions within a basic block
- DAG size ≤ Syntax tree size always
- DAG directly enables optimization; syntax tree does not
- **Trick:** "Tree = Twice likhta hai, DAG = ek baar likh ke Adjust kar leta hai (share karta hai)."

---

### 20. Machine Independent vs Dependent Optimization ★★★★★
- Machine Independent = works on intermediate code, hardware-agnostic
  → constant folding, dead code elimination, common sub-expr elimination, loop optimization
- Machine Dependent = works on target code, hardware-specific
  → register allocation, peephole optimization, instruction scheduling
- Independent happens BEFORE code generation; Dependent happens DURING/AFTER
- **Trick:** "Independent = Idea level (intermediate code), Dependent = Device level (target machine)."

---

## Last-Glance Formula Box

| Concept | Formula |
|---|---|
| Left Recursion Removal | A → βA' , A' → αA' \| ε |
| Left Factoring | A → αA' , A' → β1 \| β2 |
| LL(1) Table Rule | FIRST(α) → Table[A,a]; if ε∈FIRST(α), use FOLLOW(A) |
| SLR Reduce Rule | reduce A→α for all a ∈ FOLLOW(A) |
| LR Power Order | LR(0) < SLR(1) < LALR(1) ≤ CLR(1) |

## Topics by Unit (Quick Locator)

| Unit | Topics |
|---|---|
| Unit 1 | Compiler Phases (1), Lexical Analysis (6), Symbol Table (13), Compiler Errors (14) |
| Unit 2 | Left Recursion (2), FIRST/FOLLOW+Table (3), Left Factoring (10), Ambiguous Grammar (11), Predictive Parsing (15), FIRST/FOLLOW Differentiate (16) |
| Unit 3 | LR/SLR Parsing (9), Operator Precedence Parsing (17), LR(0)/SLR/CLR/LALR Comparison (18) |
| Unit 4 | Type Checking (4), Symbol Table (7), Code Optimization+DAG (8), Peephole Optimization (12), Syntax Tree vs DAG (19), Machine Indep. vs Dep. Optimization (20) |
| Unit 5/6 | Code Generation + Registers (5) |

## 5-Minute Priority Order (if very short on time)
1. Compiler Phases (1)
2. Left Recursion + Left Factoring (2, 10)
3. FIRST/FOLLOW + LL(1) Table (3)
4. LR Parsing — SLR + Comparison (9, 18)
5. Lexical Analysis (6)
6. Machine Indep. vs Dep. Optimization (20)

All the best for your exam.
