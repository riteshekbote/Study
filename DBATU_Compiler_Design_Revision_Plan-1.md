# DBATU Compiler Design (BTCOC601) — High-Priority Revision Plan

**Based on:** Repeated patterns across DBATU CD papers (Summer 2022, Aug 2022, Jul 2023, and similar cycles) + standard compiler design marks distribution.

This plan covers **5 highest-probability questions**. Each covers a different syllabus unit, so together they give maximum syllabus coverage with minimum wasted effort.

---

# Q1

**Question:**
What is a Compiler? Explain the different phases of a compiler with a neat diagram. State commonly used compiler-construction tools.

**Probability:** ★★★★★ (Very High)

**Why Important:**
- This is the single most repeated question type in DBATU CD papers — appears almost every cycle in some form (Define Compiler + Tools was directly asked).
- Covers Unit 1 entirely (Introduction to Compilers).
- It's often clubbed as "define + explain" so it's an easy guaranteed-marks question if memorized well.

---

## Part 1: Hinglish Concept

Dekho, tum jo bhi C, Java, Python me code likhte ho, wo computer seedha samajh nahi sakta. Computer sirf **0 aur 1 (machine code)** samajhta hai.

**Ye hota kya hai?**
Compiler ek **translator** hai jo tumhari high-level language (jaise C) ko machine language me convert karta hai — bilkul waise jaise ek Hindi-English translator ek Hindi speech ko English me convert karta hai taaki foreign audience samajh sake.

Ye translation ek hi step me nahi hota — **6 phases** me hota hai, ek assembly line ki tarah:
1. Lexical Analysis — code ko chhote-chhote tokens (words) me todna
2. Syntax Analysis — grammar check (parse tree banana)
3. Semantic Analysis — meaning check (type mismatch, undeclared variable)
4. Intermediate Code Generation — ek generic code banate hain (three address code)
5. Code Optimization — code ko fast/chota banana
6. Code Generation — final machine code banana

**Ye kyu use hota hai?**
Kyuki agar direct machine code likhna pade to har programmer ko binary me code likhna padta — bahut mushkil. Compiler is problem ko solve karta hai — tum easy language me likho, wo machine ke liye convert kar dega.

**Exam me isse kya puch sakte hai?**
- Diagram bana ke saare phases explain karo
- Har phase ka kaam ek line me batao
- Ek example lekar dikhao ki `a = b + c * 2` in phases se kaise guzarta hai
- Compiler construction tools ke naam (Lex, Yacc, LLVM, etc.)

---

## Part 2: English Exam Answer

### 1. Definition
A **compiler** is a translator/software program that converts source code written in a high-level programming language into equivalent target code (machine code or assembly code), while also checking the code for errors.

### 2. Introduction
Since computers understand only machine language (binary), a compiler bridges the gap between human-readable code and machine-executable code. The translation process is broken into several logically distinct phases, each performing a specific transformation and passing its output to the next phase.

### 3. Working / Steps (Phases of Compiler)

1. **Lexical Analysis (Scanner):** Reads source code character by character and groups them into meaningful sequences called **lexemes**, producing **tokens** (e.g., identifier, keyword, operator). Also builds entries in the Symbol Table.

2. **Syntax Analysis (Parser):** Takes tokens and checks whether they follow the grammar rules of the language. Produces a **parse tree / syntax tree**.

3. **Semantic Analysis:** Checks for meaning-level errors — type mismatches, undeclared variables, scope rules. Produces an **annotated syntax tree**.

4. **Intermediate Code Generation:** Converts the syntax tree into an intermediate, machine-independent representation, commonly **Three Address Code (TAC)**.

5. **Code Optimization:** Improves the intermediate code to make it run faster or use less memory, without changing its meaning.

6. **Code Generation:** Converts optimized intermediate code into **target machine code / assembly code**, allocating registers and memory.

Throughout all phases, the **Symbol Table Manager** and **Error Handler** work alongside, storing variable information and catching errors respectively.

### 4. Diagram

```
                Source Program
                      |
              +----------------+
              | Lexical Analyzer|
              +----------------+
                      | tokens
              +----------------+
              | Syntax Analyzer |
              +----------------+
                      | parse tree
              +------------------+
              | Semantic Analyzer|
              +------------------+
                      | annotated tree
        +----------------------------+
        | Intermediate Code Generator|
        +----------------------------+
                      | three address code
              +------------------+
              | Code Optimizer   |
              +------------------+
                      | optimized code
              +------------------+
              | Code Generator   |
              +------------------+
                      |
              Target Machine Code

   <---> Symbol Table Manager  (connected to all phases)
   <---> Error Handler         (connected to all phases)
```

### 5. Example
For statement: `a = b + c * 2`

- Lexical Analysis → tokens: `id(a) = id(b) + id(c) * 2`
- Syntax Analysis → parse tree with `+` and `*` following precedence
- Semantic Analysis → checks `a, b, c` are declared and type-compatible
- Intermediate Code → `t1 = c * 2` , `t2 = b + t1` , `a = t2`
- Code Optimization → may reduce temporary variables
- Code Generation → `MOV R1, c` `MUL R1, #2` `ADD R1, b` `MOV a, R1`

### 6. Compiler Construction Tools
- **Lex / Flex** — Lexical analyzer generator
- **Yacc / Bison** — Parser generator
- **LLVM** — Code generation and optimization framework
- **JavaCC** — Parser generator for Java
- **ANTLR** — Parser generator for multiple languages

### 7. Advantages
- Produces fast target code (compiled once, run many times).
- Detects errors before program execution.
- Optimized code improves performance.

### 8. Limitations
- Compilation itself takes time.
- Debugging can be harder since errors are shown after full compilation.
- Machine-dependent final code (needs recompilation for different platforms).

### 9. Applications
- Used to build compilers for C, C++, Java (JIT), Python (bytecode compiler), etc.
- Concepts used in building interpreters, assemblers, and even tools like grammar checkers.

### 10. Conclusion
A compiler is essential software that systematically transforms high-level code into machine code through six well-defined phases, ensuring correctness and efficiency, supported by tools like Lex and Yacc for construction.

---

## Part 3: Diagram
(See diagram above — draw the 6 boxes in a vertical chain with Symbol Table + Error Handler as side boxes connected to all phases.)

---

## Part 4: Examiner Keywords
Compiler, **Lexical Analyzer**, **Token**, **Lexeme**, **Symbol Table**, **Parse Tree**, **Syntax Analyzer**, **Semantic Analyzer**, **Intermediate Code**, **Three Address Code**, **Code Optimization**, **Code Generation**, **Error Handler**

---

## Part 5: PYQ Notes
- **Expected Marks:** 6–8 marks (sometimes split as 3+3 with tools)
- **Previous Frequency:** Asked almost every semester in some form — extremely repeated
- **Common Mistakes:** Students forget Symbol Table/Error Handler as cross-cutting components; forget to number phases in correct order
- **Related Questions:** "Differentiate compiler and interpreter", "What is cross-compiler / bootstrapping?"

---

## Part 6: Revision Box
- Compiler = translator, high-level → machine code
- 6 phases: Lexical → Syntax → Semantic → Intermediate → Optimization → Code Gen
- Symbol table + error handler support ALL phases
- Lexical = tokens, Syntax = parse tree, Semantic = type check
- Tools: Lex, Yacc, LLVM, ANTLR
- TAC = Three Address Code (intermediate form)

---

## Part 7: Expected Viva Questions
1. What is the difference between a compiler and an interpreter?
2. Which phase of the compiler detects type mismatch errors?
3. What is a token vs a lexeme?
4. Why is code optimization done after intermediate code generation?
5. Name any two compiler construction tools.

---

## Part 8: Memory Trick
**"Lazy Students Study Intermediate Optimization Code"**
(Lexical, Syntax, Semantic, Intermediate, Optimization, Code generation)

---
---

# Q2

**Question:**
What is Left Recursion? Explain the algorithm to eliminate left recursion with a suitable example. Also eliminate left recursion from: E → E+T | T, T → T*F | F, F → (E) | id

**Probability:** ★★★★★ (Very High)

**Why Important:**
- Directly repeated as an exact PYQ (asked with this exact grammar in DBATU CD papers).
- Core topic of Unit 2 (Syntax Analysis / Top-Down Parsing).
- Numerical + theory combo — high scoring if practiced.

---

## Part 1: Hinglish Concept

**Ye hota kya hai?**
Left recursion tab hoti hai jab ek grammar rule khud apne aap ko **left side (shuru) me** call karta hai. Jaise: `E → E + T`. Yaha E ke definition ke andar hi E phir se aa raha hai, shuru me.

Isse problem kya hai? Agar tum ek **top-down parser** (jaise recursive descent) banate ho, to ye parser E ko expand karega, phir wapas E milega, phir wapas E... **infinite loop** ban jayega! Parser kabhi khatam nahi hoga.

**Real life example:** Socho tumse koi bole "Pehle apna naam batao, phir tumhara naam batao, phir tumhara naam batao..." — ye kabhi ruk hi nahi raha. Yehi left recursion ka problem hai.

**Ye kyu use hota hai (fix kyu karte hai)?**
Top-down parsers (LL parsers) left recursion handle nahi kar sakte. Isliye grammar ko rewrite karna padta hai taaki wahi language generate ho, but bina left recursion ke — right recursion use karke.

**Formula yaad rakho:**
Agar: `A → Aα | β`
To convert karo:
```
A  → βA'
A' → αA' | ε
```

**Exam me isse kya puch sakte hai?**
- Definition + algorithm/formula
- Direct numerical: given grammar, eliminate left recursion
- Sometimes combined with "what is ambiguous grammar"

---

## Part 2: English Exam Answer

### 1. Definition
**Left Recursion** occurs in a grammar when a non-terminal calls itself as the leftmost symbol in its own production, either directly (`A → Aα | β`) or indirectly (through a chain of other non-terminals).

### 2. Introduction
Top-down parsers (like recursive descent and LL parsers) parse input by expanding the leftmost non-terminal first. If a grammar is left-recursive, the parser keeps expanding the same non-terminal infinitely without consuming any input, causing an **infinite loop**. Hence, left recursion must be eliminated before top-down parsing.

### 3. Working / Steps (Algorithm)

**General Rule for immediate left recursion:**

For a production of the form:
```
A → Aα1 | Aα2 | ... | β1 | β2 | ...
```
(where β does not start with A)

Rewrite as:
```
A  → β1 A' | β2 A' | ...
A' → α1 A' | α2 A' | ... | ε
```

**Steps to solve a numerical:**
1. Identify the left-recursive non-terminal (A → Aα | β form).
2. Separate the recursive part (α) and non-recursive part (β).
3. Introduce a new non-terminal A'.
4. Rewrite using the rule above.
5. Repeat for all non-terminals in the grammar.

### 4. Diagram (Transformation)

```
BEFORE (Left Recursive):        AFTER (Right Recursive):
   A                                A
  / \                              / \
 A   α                            β   A'
 |                                    / \
 β                                   α   A'
                                          |
                                          ε
```

### 5. Example — Solving the Given Grammar

**Given:**
```
E → E + T | T
T → T * F | F
F → (E) | id
```

**Step 1: Eliminate left recursion in E**
Here A = E, α = "+T", β = "T"
```
E  → T E'
E' → + T E' | ε
```

**Step 2: Eliminate left recursion in T**
Here A = T, α = "*F", β = "F"
```
T  → F T'
T' → * F T' | ε
```

**Step 3: F has no left recursion, so it stays the same**
```
F → (E) | id
```

**Final Grammar (Left-recursion free):**
```
E  → T E'
E' → + T E' | ε
T  → F T'
T' → * F T' | ε
F  → (E) | id
```

### 6. Advantages
- Makes grammar suitable for top-down (LL) parsing.
- Prevents infinite recursion/looping in recursive descent parsers.
- Preserves the same language generated by original grammar.

### 7. Limitations
- Resulting grammar becomes less intuitive to read.
- Increases number of non-terminals and productions.
- Does not remove ambiguity or left factoring issues — separate techniques needed for those.

### 8. Applications
- Essential pre-processing step before building LL(1) parsers.
- Used in compiler front-end design for languages like arithmetic expression parsers.

### 9. Conclusion
Left recursion elimination is a mandatory transformation for grammars used in top-down parsing. By systematically converting `A → Aα | β` into `A → βA'` and `A' → αA' | ε`, we retain the language while making it parseable without infinite loops.

---

## Part 3: Diagram
(See transformation diagram above — draw before/after tree structures for A → Aα | β.)

---

## Part 4: Examiner Keywords
**Left Recursion**, Non-terminal, **Direct Recursion**, Indirect Recursion, **Top-Down Parser**, LL Parser, Recursive Descent, **A → βA' , A' → αA' | ε**, Epsilon (ε)

---

## Part 5: PYQ Notes
- **Expected Marks:** 6–8 marks (this exact grammar has appeared as a direct PYQ)
- **Previous Frequency:** Very high — repeated almost verbatim across cycles
- **Common Mistakes:** Forgetting the ε in A'; mixing up α and β; not applying to ALL left-recursive non-terminals (students often forget T)
- **Related Questions:** "What is Left Factoring? Eliminate left factoring from grammar...", "What is ambiguous grammar?"

---

## Part 6: Revision Box
- Left recursion: A → Aα | β (A calls itself first)
- Problem: infinite loop in top-down parsers
- Formula: A → βA' , A' → αA' | ε
- Apply to E and T (both left recursive); F is already fine
- Always add ε as one of the options for the new non-terminal
- Direct recursion = same rule; Indirect = through another non-terminal

---

## Part 7: Expected Viva Questions
1. Why can't top-down parsers handle left recursion?
2. What is the difference between direct and indirect left recursion?
3. Does eliminating left recursion change the language generated?
4. What is left factoring, and how is it different from left recursion?
5. Give the general formula for removing left recursion.

---

## Part 8: Memory Trick
**"Aage jo bacha (β) pehle likho, peeche jo tha (α) naye non-terminal ke andar daal do, aur ε mat bhoolo."**
(β first, α goes inside A' with ε as an option)

---
---

# Q3

**Question:**
What is FIRST and FOLLOW? Compute FIRST and FOLLOW for the given grammar and construct the LL(1) parsing table:
E → TE' , E' → +TE' | ε , T → FT' , T' → *FT' | ε , F → (E) | id

**Probability:** ★★★★★ (Very High)

**Why Important:**
- Direct continuation of Q2's grammar — DBATU frequently asks FIRST/FOLLOW and LL(1) table right after left recursion elimination.
- Covers core Unit 2 topic (Predictive/LL(1) Parsing).
- High-mark numerical question (often 8–10 marks).

---

## Part 1: Hinglish Concept

**Ye hota kya hai?**
- **FIRST(X)** = wo saare terminals jo X se derive hote hote **sabse pehle** aa sakte hain.
- **FOLLOW(X)** = wo saare terminals jo grammar me X ke **turant baad** aa sakte hain.

**Real life example:** Socho ek sentence "Main _____ khaata hoon". FIRST puchta hai "blank me shuru me kya-kya aa sakta hai" (jaise "khana", "roti"). FOLLOW puchta hai "is word ke baad kya-kya aata hai" (jaise "hoon", "tha").

**Ye kyu use hota hai?**
Parser ko decide karna hota hai ki kaunsi production use kare jab usko ek particular input symbol dikhe — bina backtrack kiye (LL(1) parsing me sirf 1 token dekh ke decide karna hota hai). FIRST/FOLLOW ye decision lene me madad karte hain. Fir inko use karke **LL(1) Parsing Table** banate hain, jisse parser ko pata chalta hai "is non-terminal aur is input par konsa rule apply karna hai".

**Exam me isse kya puch sakte hai?**
- FIRST aur FOLLOW compute karna diye gaye grammar ke liye
- Us par based LL(1) table banana
- Check karna ki grammar LL(1) hai ya nahi (koi cell me do entries to nahi)

---

## Part 2: English Exam Answer

### 1. Definition
- **FIRST(α):** Set of terminals that begin the strings derivable from α.
- **FOLLOW(A):** Set of terminals that can appear immediately to the right of non-terminal A in some derivation.

### 2. Introduction
FIRST and FOLLOW sets are computed for every non-terminal in a grammar and are the foundation for constructing an **LL(1) Parsing Table**, which predictive (top-down) parsers use to decide which production to apply without backtracking.

### 3. Working / Steps

**Rules for FIRST(X):**
1. If X is a terminal, FIRST(X) = {X}.
2. If X → ε, add ε to FIRST(X).
3. If X → Y1Y2...Yn, add FIRST(Y1) (minus ε) to FIRST(X); if Y1 can derive ε, also include FIRST(Y2), and so on.

**Rules for FOLLOW(A):**
1. Place `$` in FOLLOW(Start Symbol).
2. If A → αBβ, add FIRST(β) (minus ε) to FOLLOW(B).
3. If A → αBβ and β derives ε (or β is absent), add FOLLOW(A) to FOLLOW(B).

**LL(1) Table Construction Rule:**
For each production A → α:
- For each terminal `a` in FIRST(α), add A → α to Table[A, a].
- If ε is in FIRST(α), then for each terminal `b` in FOLLOW(A), add A → α to Table[A, b].

### Computing for the Given Grammar:
```
E  → T E'
E' → + T E' | ε
T  → F T'
T' → * F T' | ε
F  → (E) | id
```

**FIRST sets:**
| Non-terminal | FIRST |
|---|---|
| E | { (, id } |
| E' | { +, ε } |
| T | { (, id } |
| T' | { *, ε } |
| F | { (, id } |

**FOLLOW sets:**
| Non-terminal | FOLLOW |
|---|---|
| E | { ), $ } |
| E' | { ), $ } |
| T | { +, ), $ } |
| T' | { +, ), $ } |
| F | { *, +, ), $ } |

### 4. Diagram (LL(1) Parsing Table)

| | id | + | * | ( | ) | $ |
|---|---|---|---|---|---|---|
| **E** | E→TE' | | | E→TE' | | |
| **E'** | | E'→+TE' | | | E'→ε | E'→ε |
| **T** | T→FT' | | | T→FT' | | |
| **T'** | | T'→ε | T'→*FT' | | T'→ε | T'→ε |
| **F** | F→id | | | F→(E) | | |

### 5. Example
Parsing the string `id + id * id` using this table follows the entries: start at E, look at `id`, apply E→TE', then T→FT', then F→id, and continue — each step decided instantly by looking at just one input symbol.

### 6. Advantages
- No backtracking needed — fast, deterministic parsing.
- Simple table lookup makes implementation easy.
- Detects syntax errors early (blank table cell = error).

### 7. Limitations
- Only works for LL(1) grammars (no left recursion, no ambiguity, no common prefixes).
- Cannot handle grammars needing more than 1 lookahead token.
- Left-recursive or ambiguous grammars must be transformed first.

### 8. Applications
- Basis for building predictive/recursive-descent parsers.
- Used in compilers for languages with unambiguous, LL(1)-compatible grammars.

### 9. Conclusion
FIRST and FOLLOW sets systematically determine which production a parser should choose for a given input symbol, forming the backbone of LL(1) parsing table construction and enabling efficient, backtrack-free syntax analysis.

---

## Part 3: Diagram
(The LL(1) table above is the diagram to reproduce in exam — draw it as a grid exactly as shown.)

---

## Part 4: Examiner Keywords
**FIRST**, **FOLLOW**, LL(1) Parsing Table, Predictive Parser, **Epsilon Production**, Lookahead, Non-terminal, Terminal, **$ (end marker)**

---

## Part 5: PYQ Notes
- **Expected Marks:** 8–10 marks (often the highest-weight numerical in the paper)
- **Previous Frequency:** Very high — almost always paired with the E→E+T grammar
- **Common Mistakes:** Forgetting `$` in FOLLOW(Start symbol); forgetting to propagate FOLLOW when a production ends in a nullable non-terminal; leaving ε entries out of the table
- **Related Questions:** "Check if a grammar is LL(1)", "What is a predictive parser?"

---

## Part 6: Revision Box
- FIRST = terminals that can start a derivation
- FOLLOW = terminals that can come right after a non-terminal
- Start symbol always has `$` in FOLLOW
- If ε ∈ FIRST(A), production also goes in FOLLOW(A) columns of table
- LL(1) table: rows = non-terminals, columns = terminals + $
- Blank cell in table = syntax error / not LL(1) if two entries in one cell

---

## Part 7: Expected Viva Questions
1. What does LL(1) mean (L, L, and 1)?
2. When do we add a production to the FOLLOW-based table entries?
3. Can a grammar with left recursion have an LL(1) table? Why not?
4. What indicates a grammar is NOT LL(1)?
5. Why is `$` added to FOLLOW of the start symbol?

---

## Part 8: Memory Trick
**"FIRST dekhta hai shuruaat, FOLLOW dekhta hai baad ki baat."**
(FIRST = what starts it, FOLLOW = what comes after it)

---
---

# Q4

**Question:**
Explain Type Checking and Type Conversion in Compiler Design.

**Probability:** ★★★★☆ (High)

**Why Important:**
- Directly repeated PYQ wording ("Explain in brief about Type checking and Type Conversion").
- Covers Unit 4 (Semantic Analysis / Type Systems) — often under-prepared by students, so it's a good scoring opportunity.
- Usually a 6-mark theory question, easy to reproduce if points are memorized.

---

## Part 1: Hinglish Concept

**Ye hota kya hai?**
Type checking wo process hai jisme compiler check karta hai ki tumne jo operations likhe hai (jaise `int + string`) wo **type ke hisaab se valid hai ya nahi**.

**Real life example:** Agar tum kaho "5 kilo + 3 litre", ye add nahi ho sakta kyuki units alag hai. Compiler bhi aise hi check karta hai ki `int + float` allowed hai ya nahi, aur `int + string` jaisi galat cheez allowed nahi hai.

**Type Conversion** kya hai? Jab do alag types ko combine karna ho (jaise `int` aur `float`), to compiler automatically ek type ko dusre me convert kar deta hai taaki operation ho sake. Jaise 5 (int) ko 5.0 (float) me convert karna taaki `5 + 3.2` ho sake. Isse **implicit conversion / coercion** kehte hai. Agar programmer khud likhta hai jaise `(float)5`, to wo **explicit conversion / type casting** hai.

**Ye kyu use hota hai?**
Bina type checking ke, program crash ho sakta hai ya galat result de sakta hai (jaise string ko number samajh lena). Type conversion isliye zaroori hai taaki different types ke beech operations safely ho sake.

**Exam me isse kya puch sakte hai?**
- Definition of type checking + type conversion
- Types of type checking (static vs dynamic)
- Implicit vs Explicit conversion with example
- Where in compiler phases this happens (Semantic Analysis)

---

## Part 2: English Exam Answer

### 1. Definition
**Type Checking** is the process performed by the compiler (during semantic analysis) to verify that the operations in a program are performed on operands of compatible data types.
**Type Conversion** is the process of converting a value from one data type to another so that an operation can be legally performed.

### 2. Introduction
Every variable and expression in a program has a type (int, float, char, etc.). The compiler must ensure that operators are applied to compatible operand types; if not, it either reports a **type error** or automatically converts one type to match the other (type conversion), depending on the language rules.

### 3. Working / Steps

**Type Checking process:**
1. Compiler assigns a type to every identifier and literal (using declarations and symbol table).
2. For every expression (e.g., `a + b`), compiler checks operand types against the operator's type rules.
3. If types match → expression is valid; if not → check if conversion is possible.
4. If no valid conversion exists → **type error** reported.

**Types of Type Checking:**
- **Static Type Checking:** Done at compile time (e.g., in C, Java).
- **Dynamic Type Checking:** Done at run time (e.g., in Python).

**Type Conversion process:**
- **Implicit Conversion (Coercion):** Automatically done by the compiler.
  Example: `int a = 5; float b = 3.5; float c = a + b;` → `a` is auto-converted to float.
- **Explicit Conversion (Type Casting):** Done manually by programmer.
  Example: `float x = 9.7; int y = (int) x;` → `y = 9`.

### 4. Diagram

```
        Expression: a + b
              |
   +----------------------+
   |  Check type of 'a'   |
   |  Check type of 'b'   |
   +----------------------+
              |
        Types same? -----No-----> Try Implicit Conversion
              | Yes                        |
              v                    Conversion possible?
        Perform Operation           /            \
                                  Yes              No
                                   |                |
                          Convert & Proceed     TYPE ERROR
```

### 5. Example
```
int a = 10;
float b = 3.5;
float result = a + b;   // 'a' implicitly converted to 10.0
```
```
double d = 7.9;
int i = (int) d;   // explicit type casting, i = 7
```

### 6. Advantages
- Prevents illegal/meaningless operations (e.g., adding a string to an integer).
- Implicit conversion improves programmer convenience.
- Detects type-related bugs early (in static type checking).

### 7. Limitations
- Implicit conversion can sometimes cause unexpected precision loss (e.g., float to int truncation).
- Dynamic type checking can cause runtime errors that are missed at compile time.
- Overuse of explicit casting can lead to data loss or bugs if misused.

### 8. Applications
- Used in every compiler's semantic analysis phase.
- Critical in strongly-typed languages (Java, C++) to maintain type safety.
- Helps generate correct intermediate code with proper type-cast instructions.

### 9. Conclusion
Type checking ensures that operations in a program are semantically valid with respect to data types, while type conversion allows compatible types to interact smoothly — together they prevent type errors and maintain program correctness.

---

## Part 3: Diagram
(Use the decision-flow diagram above showing type check → conversion → error/proceed.)

---

## Part 4: Examiner Keywords
**Type Checking**, **Type Conversion**, Semantic Analysis, **Implicit Conversion (Coercion)**, **Explicit Conversion (Type Casting)**, Static Type Checking, Dynamic Type Checking, Type Error

---

## Part 5: PYQ Notes
- **Expected Marks:** 6 marks
- **Previous Frequency:** High — asked in "Explain in brief" style directly
- **Common Mistakes:** Confusing implicit vs explicit conversion; not mentioning that type checking happens in semantic analysis phase
- **Related Questions:** "What is a type checker?", "Explain static vs dynamic type checking"

---

## Part 6: Revision Box
- Type checking = verifying operand type compatibility
- Happens in Semantic Analysis phase
- Static = compile-time (C, Java); Dynamic = run-time (Python)
- Implicit conversion = automatic (coercion)
- Explicit conversion = manual (type casting)
- No valid conversion → type error

---

## Part 7: Expected Viva Questions
1. In which compiler phase does type checking occur?
2. What is the difference between implicit and explicit type conversion?
3. Give one example of a type error.
4. Is Python statically or dynamically typed?
5. What happens if type conversion is not possible?

---

## Part 8: Memory Trick
**"Compiler khud kare = Implicit, Programmer khud kare = Explicit."**

---
---

# Q5

**Question:**
Explain the Code Generation algorithm with Three Address Instructions. State the four principal uses of registers used by the Code Generator.

**Probability:** ★★★★☆ (High)

**Why Important:**
- Directly repeated PYQ wording from DBATU CD paper.
- Covers Unit 5/6 (Code Generation) — one of the last-unit topics students often skip, making it a high-value scoring opportunity.
- Combines theory + algorithm, typically worth 8 marks.

---

## Part 1: Hinglish Concept

**Ye hota kya hai?**
Code generation compiler ka **last phase** hai jaha optimized intermediate code (three-address code) ko **actual machine/assembly instructions** me convert kiya jata hai — jise CPU directly run kar sake.

**Real life example:** Socho tumne ek recipe hindi me likhi (intermediate code), ab usse ek chef ke liye specific kitchen-language instructions me likhna hai jisme exact tools (registers) allocate karne hai — "Register R1 me ye value rakho, R2 me wo value rakho."

**Registers kyu important hai?**
CPU ke paas limited fast-memory locations hote hai jinhe **registers** kehte hai. Code generator ko decide karna padta hai kaunsi value kaunse register me rakhein taaki program fast chale.

**4 Principal Uses of Registers:**
1. Loop control variables ko store karna
2. Frequently used values (jaise repeated calculations) rakhna
3. Base register — memory address calculate karne ke liye
4. Index register — array/pointer offset calculate karne ke liye

**Ye kyu use hota hai?**
Registers memory se bahut fast hote hai, isliye jitna zyada data register me rakha jaye, utna fast program chalega.

**Exam me isse kya puch sakte hai?**
- Code generation algorithm steps
- Register descriptor / address descriptor concept
- 4 uses of registers (bilkul direct question)

---

## Part 2: English Exam Answer

### 1. Definition
**Code Generation** is the final phase of a compiler that converts optimized intermediate code (three-address code) into target machine code or assembly language, while efficiently allocating registers and memory locations.

### 2. Introduction
The code generator takes as input the intermediate representation (three-address code) along with the symbol table, and produces correct, efficient target code. A key responsibility is deciding which values to keep in registers (since register access is much faster than memory access) using structures called **register descriptors** and **address descriptors**.

### 3. Working / Steps (Algorithm using "getReg" approach)

1. **Input:** A sequence of three-address statements (e.g., `x = y op z`).
2. For each three-address instruction `x = y op z`:
   - Call function `getReg(x = y op z)` to determine the register `Rz` to hold the result.
   - Determine location of `y` (register/memory) using **Address Descriptor**.
   - If `y` is not already in a register, generate: `MOV Ry, y`
   - Generate the operation instruction: `OP Rz, Ry, Rz` (target-specific form: e.g. `ADD Rz, Ry`)
   - Update the **Register Descriptor** (what each register currently holds) and **Address Descriptor** (where each variable's current value is located — register/memory/both).
3. At the end of the basic block, store any register-resident live variables back to memory.
4. Repeat for all three-address statements in the block.

**Descriptors used:**
- **Register Descriptor:** Keeps track of what value each register currently holds.
- **Address Descriptor:** Keeps track of where the current value of a variable is stored (register, memory, or both).

### 4. Diagram

```
Three Address Code:
   t1 = b + c
   t2 = t1 * d
   a  = t2

Generated Target Code:
   MOV R1, b        ; R1 = b
   ADD R1, c        ; R1 = b + c   (t1 in R1)
   MOV R2, d        ; R2 = d
   MUL R2, R1       ; R2 = t1 * d  (t2 in R2)
   MOV a, R2        ; store result into a
```

### 5. Example
For expression `a = b + c * 2`:
```
t1 = c * 2
t2 = b + t1
a  = t2
```
Target Code:
```
MOV R1, c
MUL R1, #2
MOV R2, b
ADD R2, R1
MOV a, R2
```

### 6. Four Principal Uses of Registers
1. **To hold values of loop control variables**, since they are accessed repeatedly in each iteration.
2. **To hold intermediate/temporary values** produced during expression evaluation, avoiding repeated memory access.
3. **As base registers**, used to compute effective memory addresses (base + offset).
4. **As index registers**, used to access array elements or step through data structures efficiently.

### 7. Advantages
- Efficient register usage reduces memory access time, speeding up program execution.
- Produces target-specific optimized code.
- Descriptors help avoid redundant load/store instructions.

### 8. Limitations
- Limited number of physical registers can cause **register spilling** (values pushed back to memory).
- Algorithm needs to be re-tuned for each target machine architecture.
- Poor register allocation can offset the benefits of optimization.

### 9. Applications
- Used in the back-end of every real compiler (GCC, LLVM, javac).
- Essential for generating efficient assembly for embedded systems, where speed and memory matter most.

### 10. Conclusion
Code generation converts intermediate three-address code into efficient target machine instructions using register and address descriptors to make optimal use of the limited but fast CPU registers, which is critical to producing high-performance executable code.

---

## Part 3: Diagram
(Use the Three Address Code → Target Code mapping table above as the diagram.)

---

## Part 4: Examiner Keywords
**Code Generation**, **Three Address Code (TAC)**, **Register Descriptor**, **Address Descriptor**, getReg, Target Machine Code, Register Allocation, **Base Register**, **Index Register**

---

## Part 5: PYQ Notes
- **Expected Marks:** 8 marks (theory + 4 uses of registers often asked as a sub-part)
- **Previous Frequency:** High — appeared as a direct combined question
- **Common Mistakes:** Students explain code optimization instead of code generation (confusing the two phases); forgetting to mention register/address descriptors
- **Related Questions:** "What is a basic block and DAG representation?", "Explain code optimization techniques"

---

## Part 6: Revision Box
- Code generation = last phase, TAC → machine code
- Uses Register Descriptor (what's in each register) + Address Descriptor (where each variable is)
- 4 register uses: loop variables, temporary/intermediate values, base register, index register
- Register access >> memory access in speed
- Register spilling = problem when registers run out

---

## Part 7: Expected Viva Questions
1. What is the difference between a register descriptor and an address descriptor?
2. Why are registers preferred over memory for temporary storage?
3. What is register spilling?
4. What is the input to the code generation phase?
5. Name one real compiler backend that performs code generation (e.g., LLVM).

---

## Part 8: Memory Trick
**"LTBI" — Loop variable, Temporary value, Base register, Index register** (4 uses of registers)

---
---

# Overall Priority Summary

| # | Topic | Probability | Unit Covered |
|---|---|---|---|
| 1 | Compiler Phases + Tools | ★★★★★ | Introduction to Compilers |
| 2 | Left Recursion Elimination | ★★★★★ | Syntax Analysis (Top-Down) |
| 3 | FIRST/FOLLOW + LL(1) Table | ★★★★★ | Predictive Parsing |
| 4 | Type Checking & Conversion | ★★★★☆ | Semantic Analysis |
| 5 | Code Generation + Registers | ★★★★☆ | Code Generation |

These 5 questions together cover almost the entire CD syllabus breadth (front-end to back-end) with the topics most repeated in actual DBATU papers.

---
---

# Q6

**Question:**
What is Lexical Analysis? Explain the role of Lexical Analyzer with the help of tokens, lexemes, and patterns. Write regular expressions/rules to recognize identifiers and constants.

**Probability:** ★★★★★ (Very High)

**Why Important:**
- Foundational Unit 1/2 topic — appears every cycle in some form (define + role + token/lexeme/pattern distinction).
- Often combined with a small regular expression / Lex program question.
- Very easy to score full marks if the token vs lexeme vs pattern distinction is memorized precisely.

---

## Part 1: Hinglish Concept

**Ye hota kya hai?**
Lexical Analyzer compiler ka **pehla phase** hai. Iska kaam hai source code ko character-by-character padhna aur usko chhote-chhote meaningful pieces me todna, jinhe **tokens** kehte hai.

**Real life example:** Socho tumhe ek sentence di gayi: "Ram khaata hai roti." Isko tum words me todoge: "Ram" | "khaata" | "hai" | "roti" | "." — bas yehi lexical analyzer karta hai code ke sath. `int a = 5;` ko todega: `int` | `a` | `=` | `5` | `;`

**Teen important terms yaad rakho:**
- **Lexeme** = actual sequence of characters (jaise `a`, `5`, `int`)
- **Token** = category/class jisme lexeme aata hai (jaise identifier, keyword, number)
- **Pattern** = rule (regular expression) jo batata hai ki ek lexeme kaise banta hai (jaise identifier ka pattern = letter followed by letters/digits)

**Ye kyu use hota hai?**
Bina tokens banaye, parser ke liye grammar rules apply karna possible nahi hai. Lexical analyzer bhi whitespace aur comments hata deta hai jo unnecessary hote hai.

**Exam me isse kya puch sakte hai?**
- Define + role of lexical analyzer
- Difference between token, lexeme, pattern
- Regular expressions for identifier/constant
- Sometimes: write a simple Lex program

---

## Part 2: English Exam Answer

### 1. Definition
**Lexical Analysis** is the first phase of a compiler that reads the source program character by character and converts it into a sequence of meaningful units called **tokens**, while removing whitespace and comments.

### 2. Introduction
The lexical analyzer (also called scanner) acts as an interface between the source code and the parser. It groups characters into lexemes based on defined patterns and classifies each lexeme into a token type, also entering identifiers into the symbol table.

### 3. Working / Steps

1. Read source code character by character using a buffer.
2. Group characters into a **lexeme** (longest matching sequence).
3. Match the lexeme against a **pattern** (regular expression) to identify its **token** class.
4. Skip whitespace, tabs, newlines, and comments.
5. Enter identifiers/constants into the **Symbol Table**.
6. Pass the generated token stream to the Syntax Analyzer.
7. Report **lexical errors** (e.g., illegal characters) if no pattern matches.

**Key Term Distinctions:**

| Term | Meaning | Example |
|---|---|---|
| Lexeme | Actual character sequence | `total`, `25`, `if` |
| Token | Category name | `<id, "total">`, `<num, 25>`, `<keyword, if>` |
| Pattern | Rule describing the lexeme | letter (letter\|digit)* |

**Regular Expressions:**
- Identifier: `letter (letter | digit)*`
- Constant (integer): `digit digit*`

### 4. Diagram

```
   Source Code
       |
   +-------------------+
   | Remove whitespace, |
   | comments           |
   +-------------------+
       |
   +-------------------+
   | Match against      |
   | patterns (regex)   |
   +-------------------+
       |
   +-------------------+
   | Generate Token     |
   | <token-name, value>|
   +-------------------+
       |
   To Syntax Analyzer
       |
   (Identifiers also go to Symbol Table)
```

### 5. Example
For: `sum = a + 25;`

| Lexeme | Token |
|---|---|
| sum | `<id, "sum">` |
| = | `<assign-op>` |
| a | `<id, "a">` |
| + | `<add-op>` |
| 25 | `<num, 25>` |
| ; | `<semicolon>` |

### 6. Advantages
- Simplifies the parser's job by providing a clean token stream.
- Removes irrelevant details (whitespace, comments) early.
- Improves compilation efficiency by separating scanning from parsing.

### 7. Limitations
- Cannot detect syntax errors (only detects invalid tokens, not invalid arrangement).
- Needs re-scanning of the buffer in some lookahead situations.
- Cannot understand context/meaning (that is semantic analysis's job).

### 8. Applications
- Used in every compiler and interpreter front-end.
- Tools like **Lex/Flex** auto-generate lexical analyzers from regex-based rules.
- Applied in syntax highlighters, code editors, and static analysis tools.

### 9. Conclusion
Lexical analysis converts raw source code into a structured stream of tokens using patterns and lexemes, forming the essential first step that enables all later compiler phases to process the program correctly.

---

## Part 3: Diagram
(Use the Source Code → Remove whitespace → Match pattern → Token flow diagram above.)

---

## Part 4: Examiner Keywords
**Lexical Analyzer**, **Token**, **Lexeme**, **Pattern**, Regular Expression, Scanner, Symbol Table, Lexical Error, **Lex/Flex**

---

## Part 5: PYQ Notes
- **Expected Marks:** 6 marks
- **Previous Frequency:** Very high — token/lexeme/pattern distinction asked almost every cycle
- **Common Mistakes:** Mixing up token and lexeme definitions; writing pattern as if it's the same as lexeme
- **Related Questions:** "What is a Lex tool? Write structure of a Lex program", "What are lexical errors?"

---

## Part 6: Revision Box
- Lexeme = actual text; Token = category; Pattern = rule (regex)
- Lexical analyzer removes whitespace/comments
- Output: token stream `<token-name, attribute-value>`
- Identifiers go into symbol table here
- Tool: Lex/Flex generates lexical analyzers from regex

---

## Part 7: Expected Viva Questions
1. Differentiate between token, lexeme, and pattern.
2. What happens if the lexical analyzer encounters an unrecognized character?
3. What is the regular expression for an identifier?
4. Name a tool used to generate lexical analyzers.
5. Does the lexical analyzer check grammar rules?

---

## Part 8: Memory Trick
**"Lexeme dikhta hai, Token bolta hai kaun hai, Pattern batata hai kaise bana."**

---
---

# Q7

**Question:**
What is a Symbol Table? Explain its data structure, entries, and operations performed on it.

**Probability:** ★★★★☆ (High)

**Why Important:**
- Cross-cutting topic asked either standalone or combined with lexical/semantic analysis questions.
- Frequently appears as a short 6-mark theory question — easy guaranteed marks.
- Tests understanding of how compiler phases communicate.

---

## Part 1: Hinglish Concept

**Ye hota kya hai?**
Symbol Table ek **data structure** hai jisme compiler har variable, function, aur identifier ki **information store** karta hai — jaise naam, type, scope, memory location.

**Real life example:** Socho ek school register hai jisme har student ka naam, roll number, class, aur address likha hota hai. Jab bhi teacher ko kisi student ke baare me jaanna ho, wo register dekh leti hai. Symbol table bhi bilkul aisa hi register hai — jab bhi compiler ko kisi variable `a` ke baare me jaanna ho (uska type kya hai, kaha declare hua), wo symbol table check karta hai.

**Ye kyu use hota hai?**
- Ye check karne ke liye ki variable declare hua hai ya nahi
- Type checking ke liye
- Scope (kis block me variable valid hai) manage karne ke liye
- Code generation ke waqt memory address batane ke liye

**Exam me isse kya puch sakte hai?**
- Definition + fields stored in symbol table entry
- Data structures used to implement it (array, linked list, hash table, tree)
- Operations: insert(), lookup()

---

## Part 2: English Exam Answer

### 1. Definition
A **Symbol Table** is a data structure maintained by the compiler throughout all its phases to store information about identifiers (variables, functions, constants, etc.) appearing in the source program, such as their name, type, scope, and memory location.

### 2. Introduction
The symbol table is created during lexical analysis (when identifiers are first encountered) and used/updated by nearly every subsequent phase — syntax analysis, semantic analysis, and code generation — to verify declarations, check types, and allocate memory.

### 3. Working / Steps

**Information typically stored per entry:**
- Name of identifier
- Type (int, float, etc.)
- Scope (local/global/block)
- Memory location/offset
- Size (for arrays/structures)
- Line number of declaration
- For functions: number and type of parameters, return type

**Operations performed:**
1. **insert(name, attributes):** Adds a new identifier entry into the table.
2. **lookup(name):** Searches for an identifier and returns its attributes; used to verify if a variable is declared before use.

**Data structures used to implement Symbol Table:**
- **Linear List (Array):** Simple, but O(n) search time.
- **Linked List:** Easy insertion, but slow search.
- **Hash Table:** Most commonly used — O(1) average lookup time.
- **Binary Search Tree:** O(log n) search, sorted access.

### 4. Diagram

```
 Symbol Table Entry Structure:

 +--------+-------+-------+--------+------+
 | Name   | Type  | Scope | Offset | Line |
 +--------+-------+-------+--------+------+
 | sum    | int   | local | 4      | 2    |
 | total  | float | global| 8      | 1    |
 +--------+-------+-------+--------+------+

 Usage across phases:
 Lexical Analysis --insert--> Symbol Table <--lookup-- Semantic Analysis
                                     ^
                                     |
                              Code Generator (for address)
```

### 5. Example
For code:
```
int a;
float b;
a = 5;
```
Symbol Table after processing:
| Name | Type | Scope | Address |
|---|---|---|---|
| a | int | global | 1000 |
| b | float | global | 1004 |

### 6. Advantages
- Enables fast verification of variable declaration and type.
- Supports scope management for nested blocks/functions.
- Speeds up code generation via quick memory address lookup.

### 7. Limitations
- Extra memory overhead for maintaining the table.
- Poor choice of data structure (e.g., simple list) can slow down large programs.
- Managing nested scopes correctly adds implementation complexity.

### 8. Applications
- Used throughout the compiler: lexical, syntax, semantic, and code generation phases.
- Essential for implementing scoping rules in block-structured languages (C, Java).

### 9. Conclusion
The symbol table is a central data structure that stores identifier attributes and supports insert/lookup operations, enabling type checking, scope resolution, and memory allocation across all compiler phases.

---

## Part 3: Diagram
(Use the table-entry structure + phase-interaction diagram above.)

---

## Part 4: Examiner Keywords
**Symbol Table**, Identifier, **Insert()**, **Lookup()**, Scope, Attribute, Hash Table, Offset/Memory Address

---

## Part 5: PYQ Notes
- **Expected Marks:** 6 marks
- **Previous Frequency:** High — often a standalone short question
- **Common Mistakes:** Forgetting to mention scope; not naming insert/lookup operations explicitly; skipping data structure options
- **Related Questions:** "How is scope handled in symbol table for nested blocks?", "What is a hash table and why is it preferred for symbol tables?"

---

## Part 6: Revision Box
- Symbol table stores: name, type, scope, address, size
- Two main operations: insert() and lookup()
- Best implementation: hash table (O(1) average)
- Created in lexical analysis, used by all later phases
- Helps in type checking, scoping, and code generation

---

## Part 7: Expected Viva Questions
1. What two main operations does a symbol table support?
2. Which data structure gives the fastest average lookup time?
3. Why is the symbol table needed during code generation?
4. What information is NOT typically stored in a symbol table? (e.g., actual runtime values)
5. How is scope handled for nested blocks in a symbol table?

---

## Part 8: Memory Trick
**"Symbol Table = School Register of Compiler"** (har student/variable ka record ek jagah)

---
---

# Q8

**Question:**
What is Code Optimization? Explain the concept of Directed Acyclic Graph (DAG) for basic blocks with a suitable example. State different types of code optimization techniques.

**Probability:** ★★★★☆ (High)

**Why Important:**
- Repeated theory + numerical combo in Unit 5/6 (Code Optimization).
- DAG construction is a favorite numerical since it's easy to grade and test understanding of redundancy elimination.
- Often worth 8 marks due to the diagram + example requirement.

---

## Part 1: Hinglish Concept

**Ye hota kya hai?**
Code Optimization matlab intermediate code ko **improve karna** — taaki wo kam time le, kam memory use kare, lekin result wahi rahe jo pehle tha.

**Real life example:** Socho tum ghar se office jaate ho ek lambe raste se, lekin ek chhota shortcut bhi hai jo same jagah pohchata hai. Optimization matlab hai wo shortcut dhoondna — same destination (result), lekin kam effort (time/memory) me.

**DAG (Directed Acyclic Graph) kya hai?**
DAG ek graph hai jo ek **basic block** (statements ka group jisme koi jump nahi hota) ko represent karta hai. Isse pata chalta hai kaunse **common sub-expressions** repeat ho rahe hain, taaki unhe dobara calculate na karna pade — ek hi baar calculate karo, use kar lo bar bar.

**Ye kyu use hota hai?**
- Duplicate calculations hatane ke liye (common subexpression elimination)
- Dead code (jo kabhi use hi nahi hota) hatane ke liye
- Loop ko fast banane ke liye

**Exam me isse kya puch sakte hai?**
- Define code optimization + types
- DAG banana ek diye gaye expression/basic block ke liye
- DAG se common subexpressions identify karna

---

## Part 2: English Exam Answer

### 1. Definition
**Code Optimization** is the phase of compilation that improves the intermediate code by making it execute faster and/or consume less memory, without changing the program's output/meaning.

### 2. Introduction
Optimization can be applied at different levels — machine-independent (on intermediate code) or machine-dependent (on target code). One key technique for local optimization within a basic block is representing it as a **DAG (Directed Acyclic Graph)**, which reveals redundant computations.

### 3. Working / Steps

**Types of Code Optimization:**
1. **Local Optimization:** Applied within a single basic block (e.g., DAG-based).
2. **Global Optimization:** Applied across the entire flow graph/function.
3. **Common Sub-expression Elimination:** Avoid recomputing the same expression.
4. **Dead Code Elimination:** Remove code whose result is never used.
5. **Loop Optimization:** Reduce work done inside loops (e.g., moving invariant code outside).
6. **Constant Folding:** Evaluate constant expressions at compile time (e.g., `2*3` → `6`).
7. **Strength Reduction:** Replace expensive operations with cheaper ones (e.g., `x*2` → `x+x`).

**Steps to construct a DAG for a basic block:**
1. Create a leaf node for each initial value of a variable/constant.
2. For each statement `x = y op z`, create an interior node labeled `op` with children `y` and `z`.
3. If an identical node (same operator, same children) already exists, reuse it instead of creating a new one — this reveals **common sub-expressions**.
4. Label each node with the variable(s) it currently represents.

### 4. Diagram — DAG Example

For the basic block:
```
t1 = b + c
t2 = a + t1
t3 = b + c
t4 = t2 + t3
```

DAG construction:
```
              t4
             /  \
           t2    t3
          /  \   /
         a   t1(=t3, shared!)
              \
             +
            / \
           b   c
```

Since `t1 = b+c` and `t3 = b+c` compute the **same expression**, they share the same DAG node — showing that `t3` is redundant and can be eliminated, directly using `t1`'s value instead.

### 5. Example
Optimized code after DAG analysis:
```
t1 = b + c
t2 = a + t1
t4 = t2 + t1     // t3 removed, reuse t1
```

### 6. Advantages
- Reduces number of redundant computations, improving speed.
- Reduces code size (fewer instructions).
- DAG makes redundancy visually/structurally obvious.

### 7. Limitations
- DAG only optimizes within a single basic block (local scope) — misses global redundancy.
- Constructing and analyzing DAGs adds compilation time.
- Aggressive optimization can sometimes make debugging harder.

### 8. Applications
- Used in compiler back-ends (GCC, LLVM) to generate efficient code.
- Applied in performance-critical software like embedded systems and game engines.

### 9. Conclusion
Code optimization improves intermediate code efficiency without altering program behavior, and the DAG representation of basic blocks is a powerful tool to detect and eliminate common sub-expressions, directly reducing redundant computation.

---

## Part 3: Diagram
(Use the DAG tree structure above showing shared nodes for common sub-expressions.)

---

## Part 4: Examiner Keywords
**Code Optimization**, **DAG (Directed Acyclic Graph)**, Basic Block, **Common Sub-expression Elimination**, Dead Code Elimination, Constant Folding, Strength Reduction, Loop Optimization

---

## Part 5: PYQ Notes
- **Expected Marks:** 8 marks
- **Previous Frequency:** High — DAG numerical is a favorite
- **Common Mistakes:** Not reusing/sharing nodes for identical sub-expressions; forgetting to label final result variables on nodes
- **Related Questions:** "What is a basic block?", "Explain peephole optimization"

---

## Part 6: Revision Box
- Optimization = faster/smaller code, same output
- Types: local, global, common sub-expr elimination, dead code elimination, loop optimization, constant folding, strength reduction
- DAG built for one basic block at a time
- Shared nodes in DAG = common sub-expressions (redundant code)
- DAG helps eliminate redundant computation automatically

---

## Part 7: Expected Viva Questions
1. What is a basic block?
2. How does a DAG help identify common sub-expressions?
3. Give an example of constant folding.
4. What is the difference between local and global optimization?
5. What is strength reduction? Give an example.

---

## Part 8: Memory Trick
**"DAG = Duplicate Andar Gayab"** (DAG makes duplicate/redundant computations disappear by sharing nodes)

---
---

# Updated Overall Priority Summary

| # | Topic | Probability | Unit Covered |
|---|---|---|---|
| 1 | Compiler Phases + Tools | ★★★★★ | Introduction to Compilers |
| 2 | Left Recursion Elimination | ★★★★★ | Syntax Analysis (Top-Down) |
| 3 | FIRST/FOLLOW + LL(1) Table | ★★★★★ | Predictive Parsing |
| 4 | Type Checking & Conversion | ★★★★☆ | Semantic Analysis |
| 5 | Code Generation + Registers | ★★★★☆ | Code Generation |
| 6 | Lexical Analysis (Token/Lexeme/Pattern) | ★★★★★ | Lexical Analysis |
| 7 | Symbol Table | ★★★★☆ | Cross-cutting (all phases) |
| 8 | Code Optimization + DAG | ★★★★☆ | Code Optimization |

Remaining high-value topic not yet covered: **LR Parsing (SLR/CLR construction, LR(0) items, handle, shift-reduce parsing)** — this is the last major numerical-heavy topic in Unit 2/3.

---
---

# Q9

**Question:**
What is LR Parsing? Explain Shift-Reduce parsing with LR(0) items. Construct the SLR parsing table for the grammar:
S → AA , A → aA | b

**Probability:** ★★★★★ (Very High)

**Why Important:**
- LR parsing is the single most numerical-heavy, highest-weight topic in Unit 2/3 — almost guaranteed to appear as an 8–10 mark question.
- Tests multiple sub-skills together: augmented grammar, LR(0) items, canonical collection, action/goto table — examiners love this because it's easy to grade step-by-step.
- Completes full syllabus coverage when combined with Q1–Q8.

---

## Part 1: Hinglish Concept

**Ye hota kya hai?**
LR Parsing ek **bottom-up parsing** technique hai. "LR" ka matlab hai: **L**eft to right input scan, **R**ightmost derivation in reverse. Ye parser input ko left se right padhta hai, aur dheere-dheere use reduce karke wapas **start symbol** tak le jaata hai.

**Real life example:** Socho tumhe ek jigsaw puzzle diya gaya hai finished picture ke bina. Top-down parsing (LL) me tum pehle guess karte ho "ye final picture kaisi hogi" phir pieces fit karte ho. LR (bottom-up) me tum ulta karte ho — pehle chhote-chhote pieces jodo (reduce karo), aur end me poori picture (start symbol) ban jaati hai.

**Shift-Reduce ka matlab:**
- **Shift** = agla input symbol stack par push karo
- **Reduce** = stack ke top par jo pattern match kare ek grammar rule ke RHS se, use LHS se replace kar do

**LR(0) items kya hai?**
Ek production me ek **dot (.)** rakhte hai jo batata hai ki abhi tak kitna part parse ho chuka hai. Jaise `A → a.b` matlab `a` already parse ho chuka, `b` abhi baaki hai.

**Ye kyu use hota hai?**
LR parsers zyada powerful hote hai LL parsers se — wo left recursive grammars bhi handle kar sakte hai, aur zyada grammars ko parse kar sakte hai bina modify kiye.

**Exam me isse kya puch sakte hai?**
- Augmented grammar banana
- Canonical collection of LR(0) items (states) banana
- SLR parsing table (ACTION + GOTO) banana
- Given input string ko parse karke dikhana (stack-based trace)

---

## Part 2: English Exam Answer

### 1. Definition
**LR Parsing** is a bottom-up parsing technique that scans input from **L**eft to right and produces a **R**ightmost derivation in reverse, using a stack and a parsing table (ACTION and GOTO) to decide between shift and reduce actions.

### 2. Introduction
LR parsers are more powerful than LL parsers — they can handle a larger class of grammars, including most unambiguous context-free grammars used in real programming languages, without requiring left-recursion elimination. **SLR (Simple LR)** is the simplest variant, built using LR(0) items and FOLLOW sets.

### 3. Working / Steps

**Step 1: Augment the Grammar**
Add a new start symbol S' with production `S' → S`.

**Step 2: Construct Canonical Collection of LR(0) Items**
- An **LR(0) item** is a production with a dot (.) indicating parsing progress, e.g., `A → a.Ab`.
- Compute **closure(I)**: if `A → α.Bβ` is in I, add all `B → .γ` productions to I.
- Compute **goto(I, X)**: closure of items moved past symbol X.
- Build states (I0, I1, I2, ...) starting from closure of `S' → .S`.

**Step 3: Build SLR Parsing Table**
- If `A → α.aβ` is in state Ii and goto(Ii, a) = Ij → **ACTION[i, a] = shift j**
- If `A → α.` is in state Ii → **ACTION[i, a] = reduce A→α** for all `a` in FOLLOW(A)
- If `S' → S.` is in state Ii → **ACTION[i, $] = accept**
- If goto(Ii, A) = Ij for non-terminal A → **GOTO[i, A] = j**

**Step 4: Parse the input using stack + table** (shift symbols/states, reduce using productions, until accept).

### Worked Example — Grammar: S → AA , A → aA | b

**Augmented Grammar:**
```
S' → S
S  → AA
A  → aA | b
```

**Canonical Collection (LR(0) items) — key states:**
```
I0: S' → .S , S → .AA , A → .aA , A → .b
I1: S' → S.                          (on S from I0)
I2: S → A.A , A → .aA , A → .b       (on A from I0)
I3: A → a.A , A → .aA , A → .b       (on a from I0)
I4: A → b.                            (on b from I0)
I5: S → AA.                           (on A from I2)
I6: A → aA.                           (on A from I3)
```

**SLR Parsing Table:**

| State | a (shift) | b (shift) | $ | S (goto) | A (goto) |
|---|---|---|---|---|---|
| I0 | s3 | s4 | | 1 | 2 |
| I1 | | | accept | | |
| I2 | s3 | s4 | | | 5 |
| I3 | s3 | s4 | | | 6 |
| I4 | r(A→b) | r(A→b) | r(A→b) | | |
| I5 | r(S→AA) | r(S→AA) | r(S→AA) | | |
| I6 | r(A→aA) | r(A→aA) | r(A→aA) | | |

### 4. Diagram

```
     LR PARSER MODEL

   Input: a1 a2 a3 ... an $
                |
     +--------------------+
     |   STACK             | <---- ACTION/GOTO Table
     |  (states + symbols) |
     +--------------------+
                |
        shift / reduce / accept / error
```

### 5. Example — Parsing "aab" using the table above
| Stack | Input | Action |
|---|---|---|
| 0 | aab$ | shift (s3) |
| 0 a3 | ab$ | shift (s3) |
| 0 a3 a3 | b$ | shift (s4) |
| 0 a3 a3 b4 | $ | reduce A→b |
| 0 a3 a3 A6 | $ | reduce A→aA |
| 0 a3 A6 | $ | reduce A→aA |
| 0 A2 | $ | ... continues until S accepted |

### 6. Advantages
- Handles a wider range of grammars than LL parsers (including left-recursive ones).
- Detects syntax errors as soon as possible while scanning left to right.
- Table-driven — efficient and fast once built.

### 7. Limitations
- Constructing the parsing table by hand is time-consuming and error-prone.
- SLR is weaker than CLR/LALR — some grammars cause shift-reduce or reduce-reduce conflicts in SLR that CLR can resolve.
- Requires more implementation effort compared to simple recursive descent.

### 8. Applications
- Used in real-world parser generators like **YACC/Bison**.
- Basis for parsing most modern programming languages (C, Java use LALR variants).

### 9. Conclusion
LR parsing is a robust bottom-up technique that uses a stack, LR(0) items, and an ACTION/GOTO table to parse a wide class of grammars efficiently, forming the backbone of most real-world parser generator tools like YACC.

---

## Part 3: Diagram
(Draw the LR Parser Model box diagram above: Input → Stack ↔ ACTION/GOTO Table → shift/reduce/accept.)

---

## Part 4: Examiner Keywords
**LR Parsing**, Bottom-Up Parsing, **Shift**, **Reduce**, LR(0) Item, **Closure**, **Goto**, Augmented Grammar, **SLR Parsing Table**, ACTION table, GOTO table, Handle, Shift-Reduce Conflict

---

## Part 5: PYQ Notes
- **Expected Marks:** 10 marks (highest-weight numerical topic in the paper)
- **Previous Frequency:** Very high — appears almost every cycle with a small grammar
- **Common Mistakes:** Forgetting to augment the grammar (S' → S) first; wrong FOLLOW set used for reduce actions; forgetting the "accept" action at S'→S.
- **Related Questions:** "Differentiate LL and LR parsing", "What is a shift-reduce conflict?", "Explain CLR/LALR parsing"

---

## Part 6: Revision Box
- LR = Left-to-right scan, Rightmost derivation in reverse
- Always augment grammar first: S' → S
- Dot (.) in item shows parsing progress
- Shift = push input symbol; Reduce = replace RHS with LHS using a production
- Reduce action added for all terminals in FOLLOW(A) — that's what makes it "SLR"
- Accept happens only when S'→S. is reached with $ as lookahead

---

## Part 7: Expected Viva Questions
1. What does LR stand for?
2. Why is the grammar augmented before constructing LR items?
3. What is the difference between shift and reduce actions?
4. What is a shift-reduce conflict, and when does it occur?
5. How is SLR different from CLR/LALR parsing?

---

## Part 8: Memory Trick
**"SLR banate waqt: Augment → Items (closure+goto) → Table (Action+Goto) → Parse (Shift/Reduce)"** — remember as **A-I-T-P**.

---
---

# Final Overall Priority Summary — Full Syllabus Coverage

| # | Topic | Probability | Unit Covered |
|---|---|---|---|
| 1 | Compiler Phases + Tools | ★★★★★ | Introduction to Compilers |
| 2 | Left Recursion Elimination | ★★★★★ | Syntax Analysis (Top-Down) |
| 3 | FIRST/FOLLOW + LL(1) Table | ★★★★★ | Predictive Parsing |
| 4 | Type Checking & Conversion | ★★★★☆ | Semantic Analysis |
| 5 | Code Generation + Registers | ★★★★☆ | Code Generation |
| 6 | Lexical Analysis (Token/Lexeme/Pattern) | ★★★★★ | Lexical Analysis |
| 7 | Symbol Table | ★★★★☆ | Cross-cutting (all phases) |
| 8 | Code Optimization + DAG | ★★★★☆ | Code Optimization |
| 9 | LR Parsing (SLR Table Construction) | ★★★★★ | Bottom-Up Parsing |

**This 9-question set now covers every major unit of DBATU Compiler Design (BTCOC601):** Introduction → Lexical Analysis → Top-Down Parsing → Bottom-Up Parsing → Semantic Analysis → Symbol Table → Intermediate Code → Optimization → Code Generation.

If you want, I can add a couple of "backup" questions next (Recursive Descent Parsing, Ambiguous Grammar/Left Factoring, or Peephole Optimization) to cover any remaining low-probability gaps.

---
---

# Q10

**Question:**
What is Left Factoring? Explain with algorithm and eliminate left factoring from the grammar:
S → iEtS | iEtSeS | a , E → b

**Probability:** ★★★★☆ (High)

**Why Important:**
- Frequently paired with left recursion in the same question paper (both are "grammar transformation" topics).
- Tests the exact same skill area as Q2, so preparing both together is efficient.
- Classic if-then-else grammar example is a DBATU favorite.

---

## Part 1: Hinglish Concept

**Ye hota kya hai?**
Left Factoring tab karte hai jab ek non-terminal ke **do ya zyada productions** same prefix (shuruaat) se start hote hai. Jaise `S → iEtS` aur `S → iEtSeS` — dono `iEtS` se start ho rahe hai.

**Problem kya hai?**
Top-down parser ko decide karna padta hai kaunsa production use kare, lekin agar shuruaat same hai to parser ko **pata hi nahi chalega** kaunsa choose kare bina aage dekhe (ye backtracking maangega, jo LL(1) parser allow nahi karta).

**Real life example:** Socho tumse koi bole "main jaa raha hoon market" ya "main jaa raha hoon school" — jab tak tum poora sun na lo, tumhe pata nahi chalega kaha jaa raha hai, kyuki shuruaat same hai "main jaa raha hoon". Left factoring is ambiguity ko hata deta hai.

**Formula yaad rakho:**
Agar: `A → αβ1 | αβ2`
To convert karo:
```
A  → αA'
A' → β1 | β2
```

**Exam me isse kya puch sakte hai?**
- Definition + algorithm
- Direct numerical: given grammar (usually if-then-else style), left factor it

---

## Part 2: English Exam Answer

### 1. Definition
**Left Factoring** is a grammar transformation technique used when two or more productions of a non-terminal share a common prefix, making the grammar suitable for top-down (predictive) parsing by delaying the decision until enough input is seen.

### 2. Introduction
When a top-down parser sees a common prefix in multiple productions of the same non-terminal, it cannot decide which production to use by looking at just one input symbol — causing ambiguity in table-driven (LL(1)) parsing. Left factoring rewrites the grammar to factor out the common prefix into a single path, followed by a new non-terminal that resolves the choice.

### 3. Working / Steps (Algorithm)

For a production of the form:
```
A → αβ1 | αβ2 | ... | αβn
```
(where α is the common prefix)

Rewrite as:
```
A  → αA'
A' → β1 | β2 | ... | βn
```

**Steps to solve a numerical:**
1. Identify productions of a non-terminal sharing a common prefix α.
2. Factor out α, introduce a new non-terminal A'.
3. Move remaining parts (β1, β2, ...) as alternatives of A'.
4. Repeat until no common prefixes remain.

### 4. Diagram

```
BEFORE:                    AFTER:
   A                          A
  / \                         |
 α   α                        α
 |   |                        |
 β1  β2                       A'
                             /  \
                            β1   β2
```

### 5. Example — Solving the Given Grammar

**Given:**
```
S → iEtS | iEtSeS | a
E → b
```

**Step 1:** Productions `iEtS` and `iEtSeS` share common prefix `iEtS`.

**Step 2:** Factor out `iEtS`:
```
S → iEtSS' | a
S' → eS | ε
```

**Final Grammar (Left-Factored):**
```
S  → iEtSS' | a
S' → eS | ε
E  → b
```

This models the classic **if-then-else** ambiguity: `i` = if, `t` = then, `e` = else, `a` = other statement, `E` = condition (b).

### 6. Advantages
- Makes the grammar deterministic for top-down/LL(1) parsing (removes the need for backtracking).
- Preserves the language generated by the original grammar.
- Simplifies parser table construction (avoids multiple entries in the same table cell).

### 7. Limitations
- Does not remove inherent ambiguity in the grammar (e.g., dangling-else problem still needs separate disambiguation rules).
- Can make the grammar less readable with extra non-terminals.
- Only handles common-prefix problems, not left recursion (a separate technique).

### 8. Applications
- Essential preprocessing before building predictive/recursive-descent parsers for constructs like if-else statements.
- Used in designing grammars for real compilers to avoid parser conflicts.

### 9. Conclusion
Left factoring resolves the ambiguity caused by common prefixes among productions of a non-terminal by factoring out the shared part, enabling deterministic, backtrack-free top-down parsing while preserving the original language.

---

## Part 3: Diagram
(Use the before/after tree diagram above showing the common prefix α factored out.)

---

## Part 4: Examiner Keywords
**Left Factoring**, Common Prefix, **A → αA' , A' → β1 | β2**, Top-Down Parsing, Predictive Parser, Backtracking, Dangling-else

---

## Part 5: PYQ Notes
- **Expected Marks:** 6–8 marks
- **Previous Frequency:** High — often clubbed with left recursion in the same question or asked separately with an if-then-else grammar
- **Common Mistakes:** Forgetting to add ε as an alternative in A'; not fully factoring when more than 2 productions share the prefix
- **Related Questions:** "What is left recursion? Difference between left recursion and left factoring", "Explain dangling-else problem"

---

## Part 6: Revision Box
- Left factoring: A → αβ1 | αβ2 (common prefix α)
- Formula: A → αA' , A' → β1 | β2
- Classic example: if-then-else grammar (S → iEtS | iEtSeS | a)
- Goal: remove ambiguity for top-down parser decision-making
- Different from left recursion — left recursion is about self-reference, left factoring is about shared prefixes

---

## Part 7: Expected Viva Questions
1. What is the difference between left recursion and left factoring?
2. Why does a common prefix cause a problem for LL(1) parsers?
3. What is the dangling-else problem?
4. Give the general formula for left factoring.
5. Does left factoring change the language generated by the grammar?

---

## Part 8: Memory Trick
**"Common shuruaat nikalo bahar, baaki sab naye A' ke andar."**

---
---

# Q11

**Question:**
What is Ambiguous Grammar? Explain with an example. How can ambiguity be resolved?

**Probability:** ★★★☆☆ (Moderate)

**Why Important:**
- Frequently asked as a short theory question (2–4 marks) alongside left recursion/left factoring questions.
- Conceptually important — often tested as a viva/short-answer topic even if not a full 8-mark question.
- Directly connects to the classic dangling-else and expression grammar examples already covered.

---

## Part 1: Hinglish Concept

**Ye hota kya hai?**
Ek grammar **ambiguous** hoti hai jab kisi ek string ke liye **do ya zyada different parse trees (ya derivations)** ban sakte hai. Matlab compiler confuse ho jaata hai ki string ka sahi structure/meaning kya hai.

**Real life example:** Socho sentence hai: "I saw a man with a telescope." Isko do tarike se samjha ja sakta hai — "maine ek aadmi ko dekha jiske paas telescope tha" YA "maine telescope se ek aadmi ko dekha". Dono meaning valid hai — yehi ambiguity hai!

**Compiler me example:** `id + id * id` — agar grammar clear precedence rule na de, to ye do tarike se parse ho sakta hai: `(id + id) * id` ya `id + (id * id)`. Dono different results denge!

**Ye kyu problem hai?**
Compiler ko exactly ek hi meaning chahiye hoti hai apne code ko execute karne ke liye — do meanings allow nahi kar sakte.

**Kaise resolve karte hai?**
- Operator **precedence** aur **associativity** rules add karke
- Grammar ko **rewrite** karke taaki har string ka ek hi parse tree bane

**Exam me isse kya puch sakte hai?**
- Define ambiguous grammar with example
- Show two different parse trees for the same string
- How to remove ambiguity (rewrite grammar)

---

## Part 2: English Exam Answer

### 1. Definition
A **grammar** is said to be **ambiguous** if there exists at least one string in the language that can be generated by **more than one distinct parse tree** (or more than one leftmost/rightmost derivation).

### 2. Introduction
Ambiguity is undesirable in programming language grammars because a compiler must derive exactly one meaning (structure) for every valid program. Ambiguous grammars can be resolved either by rewriting the grammar or by applying disambiguating rules such as operator precedence.

### 3. Working / Steps

**Classic Ambiguous Grammar Example:**
```
E → E + E | E * E | id
```

For the string `id + id * id`, two different parse trees can be formed:

**Parse Tree 1** (interprets as `id + (id * id)`):
```
        E
      / | \
     E  +  E
     |    / | \
    id   E  *  E
         |     |
        id    id
```

**Parse Tree 2** (interprets as `(id + id) * id`):
```
        E
      / | \
     E  *  E
    /|\     |
   E + E   id
   |   |
  id  id
```

Since two different trees exist for the same string, the grammar is **ambiguous**.

**How to Resolve Ambiguity:**
1. **Rewrite the grammar** using precedence levels (as seen in Q2/Q3's grammar):
```
E → E + T | T
T → T * F | F
F → (E) | id
```
This forces `*` to bind tighter than `+`, giving a single unique parse tree.

2. **Use precedence and associativity declarations** (used in tools like YACC) instead of rewriting the grammar — assign precedence levels to operators directly.

### 4. Diagram
(Use the two parse-tree diagrams above to visually demonstrate ambiguity — this is the most important diagram examiners look for.)

### 5. Example
See parse trees above for `id + id * id`.

### 6. Advantages (of resolving ambiguity)
- Ensures a program has exactly one meaning/interpretation.
- Enables deterministic parsing (needed for both LL and LR parsers).
- Improves reliability and predictability of compiled programs.

### 7. Limitations
- Rewriting grammar to remove ambiguity can make it longer/more complex (more non-terminals).
- Not all ambiguous grammars have a simple equivalent unambiguous grammar (some languages are inherently ambiguous).
- Requires care to preserve the original intended language while removing ambiguity.

### 8. Applications
- Essential in designing arithmetic expression grammars (respecting operator precedence).
- Directly relevant to the dangling-else problem in if-else statement grammars.

### 9. Conclusion
An ambiguous grammar allows multiple valid parse trees for the same string, which is unacceptable for compilers since each program must have a single, unambiguous interpretation; this is resolved by rewriting the grammar with precedence levels or using explicit precedence/associativity rules.

---

## Part 3: Diagram
(Two parse trees for `id + id * id`, shown above — draw both side by side to demonstrate ambiguity clearly.)

---

## Part 4: Examiner Keywords
**Ambiguous Grammar**, Parse Tree, **Multiple Derivations**, Operator Precedence, Associativity, Dangling-else, Unambiguous Grammar

---

## Part 5: PYQ Notes
- **Expected Marks:** 4–6 marks
- **Previous Frequency:** Moderate — often a short-answer or viva-style question
- **Common Mistakes:** Drawing only one parse tree (must show TWO to prove ambiguity); not explaining how to resolve it
- **Related Questions:** "What is the dangling-else problem?", "Differentiate ambiguous and unambiguous grammar with example"

---

## Part 6: Revision Box
- Ambiguous = more than one parse tree for same string
- Classic example: E → E+E | E*E | id
- Proof requires showing 2 different parse trees
- Resolved by: rewriting grammar with precedence levels, OR using precedence/associativity declarations
- Dangling-else is a famous real-world ambiguity example

---

## Part 7: Expected Viva Questions
1. How do you prove a grammar is ambiguous?
2. What is the dangling-else problem?
3. Can every ambiguous grammar be converted to an unambiguous one?
4. How does YACC handle ambiguity without rewriting the grammar?
5. Is the grammar E → E+T|T, T→T*F|F, F→(E)|id ambiguous? Why not?

---

## Part 8: Memory Trick
**"Ek string, do trees = Ambiguous. Ek string, ek tree = Safe."**

---
---

# Q12

**Question:**
What is Peephole Optimization? Explain its techniques with suitable examples.

**Probability:** ★★★☆☆ (Moderate)

**Why Important:**
- Common short-answer companion question to Q8 (Code Optimization/DAG) — often asked as an alternative or additional part in the same unit.
- Easy to score full marks since it's a list-based, example-driven answer.
- Fills the last gap in the Code Optimization sub-topic area.

---

## Part 1: Hinglish Concept

**Ye hota kya hai?**
Peephole Optimization ek **machine-dependent, local optimization** technique hai jisme compiler target code ke ek **chhote se window (peephole)** — jaise 2-3 instructions — ko dekhta hai aur usme se **redundant ya unnecessary instructions hata deta hai** ya replace kar deta hai.

**Real life example:** Socho tum ek essay likh rahe ho aur usme ek line hai "Main gaya, aur phir main wahi jagah wapas aaya jaha se gaya tha." — ye poora sentence hata sakte ho kyuki kuch hua hi nahi (net effect zero). Peephole optimization bhi code me aise hi "useless" ya "redundant" instructions dhoondta hai chhote window me dekh kar.

**Ye kyu use hota hai?**
Final generated machine code me chhoti-chhoti inefficiencies reh jaati hai (jaise ek value ko store karke turant wapas load karna) — peephole optimization inhe pakad kar hata deta hai, jisse code chhota aur fast ho jaata hai.

**Exam me isse kya puch sakte hai?**
- Definition + why it's called "peephole" (chhoti window)
- List techniques with one example each

---

## Part 2: English Exam Answer

### 1. Definition
**Peephole Optimization** is a machine-dependent code optimization technique performed on a small, moving window (peephole) of target instructions — usually a few instructions at a time — to replace them with shorter or faster equivalent instruction sequences.

### 2. Introduction
This is one of the simplest and most effective optimization techniques, applied directly to the generated target code as a final optimization pass. It examines only a few instructions at once (hence "peephole") and looks for well-known improvable patterns.

### 3. Working / Steps — Techniques with Examples

1. **Redundant Instruction Elimination:**
   Removes instructions that have no effect.
   ```
   MOV R1, a
   MOV a, R1      ← redundant, since a already holds this value
   ```
   Optimized: remove the second instruction.

2. **Elimination of Unreachable Code:**
   Removes code that can never be executed.
   ```
   goto L1
   x = 5          ← unreachable, never executed
   L1: ...
   ```
   Optimized: remove the unreachable statement.

3. **Algebraic Simplification:**
   Simplifies expressions using algebraic identities.
   ```
   x = x + 0   →   (removed entirely)
   x = x * 1   →   (removed entirely)
   ```

4. **Strength Reduction:**
   Replaces expensive operations with cheaper equivalent ones.
   ```
   x = y * 2   →   x = y + y
   x = y ** 2  →   x = y * y
   ```

5. **Use of Machine Idioms:**
   Replaces general instruction sequences with efficient machine-specific instructions.
   ```
   x = x + 1   →   INC x   (using increment instruction instead of add)
   ```

6. **Combining Repeated/Equivalent Instructions:**
   Merges instructions that do the same job across a small window.

### 4. Diagram

```
Target Code (before)        Peephole Window          Target Code (after)
  MOV R1, a                 [MOV R1,a]                  MOV R1, a
  MOV a, R1        ---->    [MOV a,R1]     ---->        (removed)
  ADD R1, #0                [ADD R1,#0]                 (removed)
```

### 5. Example
```
Before:
  MOV R1, x
  ADD R1, #0
  MOV x, R1

After Peephole Optimization:
  (all removed — no operation actually changes x)
```

### 6. Advantages
- Simple to implement and gives quick performance improvement.
- Works directly on target code, so it's machine-specific and effective.
- Can be applied as a final cleanup pass after other optimizations.

### 7. Limitations
- Only looks at a small window, so it misses larger/global redundancies.
- Effectiveness depends on the size and pattern-matching rules of the peephole.
- Needs to be re-applied iteratively since removing one instruction can create new optimization opportunities.

### 8. Applications
- Used as the final optimization pass in real compilers (GCC, LLVM back-end).
- Especially useful in embedded systems where code size and speed both matter.

### 9. Conclusion
Peephole optimization is a simple yet effective machine-dependent technique that scans a small window of target instructions to eliminate redundancy, simplify algebraic expressions, and use efficient machine idioms — improving code quality with minimal compilation overhead.

---

## Part 3: Diagram
(Use the "before/after" peephole window diagram above.)

---

## Part 4: Examiner Keywords
**Peephole Optimization**, Redundant Instruction Elimination, **Algebraic Simplification**, Strength Reduction, Machine Idioms, Unreachable Code, Local Window

---

## Part 5: PYQ Notes
- **Expected Marks:** 6 marks
- **Previous Frequency:** Moderate — often asked as an alternate/OR question with DAG-based optimization
- **Common Mistakes:** Confusing peephole optimization (machine-dependent, local) with general code optimization (can be machine-independent, global)
- **Related Questions:** "Differentiate machine-dependent and machine-independent optimization", "What is strength reduction?"

---

## Part 6: Revision Box
- Peephole = small window, machine-dependent, local optimization
- Techniques: redundant instruction elimination, unreachable code removal, algebraic simplification, strength reduction, machine idioms
- Applied as a final pass on target code
- Example: x = x+0 gets removed entirely

---

## Part 7: Expected Viva Questions
1. Why is it called "peephole" optimization?
2. Is peephole optimization machine-dependent or machine-independent?
3. Give an example of strength reduction.
4. What is a machine idiom?
5. When is peephole optimization applied — before or after code generation?

---

## Part 8: Memory Trick
**"RASU-M" — Redundant elimination, Algebraic simplification, Strength reduction, Unreachable code, Machine idioms.**

---
---

# Complete Revision Set — Final Summary

| # | Topic | Probability | Unit Covered |
|---|---|---|---|
| 1 | Compiler Phases + Tools | ★★★★★ | Introduction to Compilers |
| 2 | Left Recursion Elimination | ★★★★★ | Syntax Analysis (Top-Down) |
| 3 | FIRST/FOLLOW + LL(1) Table | ★★★★★ | Predictive Parsing |
| 4 | Type Checking & Conversion | ★★★★☆ | Semantic Analysis |
| 5 | Code Generation + Registers | ★★★★☆ | Code Generation |
| 6 | Lexical Analysis (Token/Lexeme/Pattern) | ★★★★★ | Lexical Analysis |
| 7 | Symbol Table | ★★★★☆ | Cross-cutting (all phases) |
| 8 | Code Optimization + DAG | ★★★★☆ | Code Optimization |
| 9 | LR Parsing (SLR Table Construction) | ★★★★★ | Bottom-Up Parsing |
| 10 | Left Factoring | ★★★★☆ | Syntax Analysis (Top-Down) |
| 11 | Ambiguous Grammar | ★★★☆☆ | Syntax Analysis (Theory) |
| 12 | Peephole Optimization | ★★★☆☆ | Code Optimization |

**This set of 12 questions gives complete, high-efficiency coverage of the entire DBATU Compiler Design (BTCOC601) syllabus** — every unit is represented, weighted toward the most-repeated PYQ patterns.

---
---

# UNIT-WISE ADDITIONAL QUESTIONS (Q13–Q20)

*These 8 questions round out 2 additional questions per unit, so each unit now has strong backup coverage beyond the top-priority set above.*

---
---

# Q13 (Unit 1)

**Question:**
Explain Symbol Table. Discuss its functions, implementation techniques, and applications.

**Probability:** ★★★★☆ (High)

**Why Important:**
- Expands on Q7 with a sharper focus on **functions** and **implementation techniques** — a common variant phrasing in DBATU papers.
- Unit 1 topic, tests deeper understanding than the basic definition-only version.
- High-scoring since it's a structured "list + explain" answer.

---

## Part 1: Hinglish Concept

**Ye hota kya hai?**
Symbol table ek data structure hai jo compiler har identifier (variable, function name) ki details store karne ke liye use karta hai — jaise ek school register jisme har student ki details hoti hai.

**Iske functions kya hai (Ye kyu use hota hai)?**
1. **Store karna** — har identifier ka naam, type, scope save karna
2. **Verify karna** — check karna variable declare hua hai ya nahi (use se pehle)
3. **Type checking me help karna**
4. **Scope resolve karna** — same naam ke variables alag blocks me alag ho sakte hai
5. **Memory address dena** — code generation ke waqt

**Implementation kaise karte hai?**
Ek simple list (array) se lekar hash table tak — hash table sabse fast hoti hai (O(1) average).

**Exam me isse kya puch sakte hai?**
- Functions list karo
- Implementation techniques compare karo (array vs linked list vs hash table vs tree)
- Applications batao (kaha-kaha use hota hai compiler me)

---

## Part 2: English Exam Answer

### 1. Definition
A **Symbol Table** is a data structure used by the compiler to store and manage information about all identifiers (variables, functions, constants, labels) appearing in a source program, throughout the compilation process.

### 2. Introduction
The symbol table is built starting from the lexical analysis phase and is referenced/updated continuously by the syntax analyzer, semantic analyzer, and code generator, making it one of the most important cross-cutting data structures in a compiler.

### 3. Working / Steps

**Functions of Symbol Table:**
1. Stores identifier attributes: name, type, scope, size, memory location.
2. Verifies whether a variable is declared before it is used.
3. Supports type checking by providing type information to the semantic analyzer.
4. Manages scope — allows same identifier name in different blocks/functions.
5. Provides memory offsets/addresses to the code generator.
6. Helps detect duplicate declarations (redeclaration errors).

**Implementation Techniques:**

| Technique | Search Time | Notes |
|---|---|---|
| Linear List (unordered array) | O(n) | Simple, slow for large programs |
| Sorted Array (Binary Search) | O(log n) | Faster search, slower insertion |
| Linked List | O(n) | Easy insertion, slow search |
| Hash Table | O(1) average | Most widely used in real compilers |
| Binary Search Tree | O(log n) | Balanced access, sorted traversal possible |

**Applications:**
- Used in lexical analysis to record new identifiers.
- Used in semantic analysis for type checking and scope resolution.
- Used in code generation for computing variable memory addresses.
- Used in error detection (undeclared variable, redeclaration).

### 4. Diagram

```
   +-------------------------------+
   |         SYMBOL TABLE           |
   +--------+------+-------+--------+
   | Name   | Type | Scope | Address|
   +--------+------+-------+--------+
   | a      | int  | local | 1000   |
   | total  | float| global| 1004   |
   +--------+------+-------+--------+
        ^        ^        ^        ^
        |        |        |        |
     Lexical  Semantic  Semantic  Code
     Analysis Analysis  Analysis  Generator
     (insert) (lookup)  (scope)   (address)
```

### 5. Example
```
int x;
{
   float x;   // different scope, allowed
}
```
Symbol table maintains two separate entries for `x` with different scope levels, avoiding a naming conflict.

### 6. Advantages
- Enables fast identifier lookup across compiler phases.
- Supports proper scoping in block-structured languages.
- Essential for accurate type checking and memory allocation.

### 7. Limitations
- Extra memory and processing overhead.
- Choosing a poor data structure (like linear list) slows down large compilations.
- Managing nested/complex scopes adds implementation difficulty.

### 8. Applications (Recap)
- Used in every phase from lexical analysis to code generation.
- Critical in IDEs too, for features like auto-complete and "go to definition."

### 9. Conclusion
The symbol table is a vital data structure that stores identifier information and supports fast insertion/lookup, using implementations like hash tables for efficiency, and serves nearly every phase of the compiler from lexical analysis to code generation.

---

## Part 3: Diagram
(Use the symbol table + phase-interaction diagram above.)

---

## Part 4: Examiner Keywords
**Symbol Table**, Functions, **Hash Table**, Scope, Insert, Lookup, Memory Offset, Type Checking, Implementation Techniques

---

## Part 5: PYQ Notes
- **Expected Marks:** 6–8 marks
- **Previous Frequency:** High — asked in "functions + implementation" combined format
- **Common Mistakes:** Only listing functions without comparing implementation techniques; forgetting hash table as the preferred method
- **Related Questions:** "Compare data structures used for symbol table implementation"

---

## Part 6: Revision Box
- Functions: store, verify, type-check, scope, address, duplicate detection
- Implementation: array (O(n)), sorted array (O(log n)), hash table (O(1) avg) — hash table is best
- Used across: lexical, semantic, code generation phases
- Applications: type checking, scope resolution, memory allocation, error detection

---

## Part 7: Expected Viva Questions
1. Which implementation gives the fastest average lookup?
2. Name three functions of a symbol table.
3. How does the symbol table help detect a redeclaration error?
4. Why is scope information necessary in a symbol table?
5. Where does the code generator use the symbol table?

---

## Part 8: Memory Trick
**"SVTSMD"** — Store, Verify, Type-check, Scope, Memory address, Duplicate detection (6 functions).

---
---

# Q14 (Unit 1)

**Question:**
Explain Compiler Errors. Differentiate Lexical, Syntax, Semantic, and Logical Errors with suitable examples.

**Probability:** ★★★★☆ (High)

**Why Important:**
- Common Unit 1 theory question testing understanding across all compiler phases at once.
- Comparison/differentiation-style questions are DBATU favorites — easy full marks if a clean table is used.
- Reinforces understanding of what each phase actually detects.

---

## Part 1: Hinglish Concept

**Ye hota kya hai?**
Jab bhi tum code likhte ho, alag-alag tarah ki galtiyan ho sakti hai — kuch compiler khud pakad leta hai, kuch nahi pakad pata.

**4 Types of Errors:**
1. **Lexical Error** — jab koi character/symbol hi galat/illegal ho. Jaise `@a = 5;` — `@` ek valid token nahi hai.
2. **Syntax Error** — jab grammar rule follow nahi hoti. Jaise `if (a > b { }` — closing bracket missing hai.
3. **Semantic Error** — jab meaning galat ho, jaise type mismatch. Jaise `int a = "hello";` — string ko int me daal rahe hai.
4. **Logical Error** — jab code chalta hai, compile bhi ho jaata hai, lekin **result galat** aata hai. Jaise average nikalne ke liye `sum * count` likh diya instead of `sum / count`. Compiler ko ye pakadna possible nahi — sirf program ka output check karke pata chalta hai.

**Real life example:** Socho tum recipe follow kar rahe ho:
- Lexical error = recipe me ek symbol hai jo samajh hi nahi aata
- Syntax error = recipe ke steps galat order me likhe hai, grammar hi galat hai
- Semantic error = step bola "namak daalo 2 kg" — matra ka type/meaning hi galat hai
- Logical error = sab sahi likha, lekin recipe follow karne ke baad khana tasteless nikla — koi step logically galat tha

**Exam me isse kya puch sakte hai?**
- Define + example for each
- Which compiler phase detects which error
- Comparison table

---

## Part 2: English Exam Answer

### 1. Definition
A **compiler error** is any issue encountered by the compiler (or the running program) that prevents correct compilation or correct execution of the source program. Errors are classified based on which compiler phase detects them: Lexical, Syntax, Semantic, or Logical.

### 2. Introduction
Each phase of the compiler is responsible for detecting a specific category of error. Understanding these categories helps in debugging and also shows how compiler phases divide responsibility for correctness checking.

### 3. Working / Steps — Comparison Table

| Error Type | Detected In | Cause | Example |
|---|---|---|---|
| **Lexical Error** | Lexical Analysis | Illegal/unrecognized character or malformed token | `@x = 5;` (`@` is not valid) |
| **Syntax Error** | Syntax Analysis | Violates grammar rules of the language | `if (a > b { }` (missing `)`) |
| **Semantic Error** | Semantic Analysis | Meaning/type-level issues even though syntax is correct | `int a = "hello";` (type mismatch) |
| **Logical Error** | Not detected by compiler — found at runtime by the programmer | Program compiles and runs, but produces incorrect results due to a flawed algorithm/logic | Using `avg = sum * count` instead of `sum / count` |

### 4. Diagram

```
 Source Code
     |
 Lexical Analysis  --> catches Lexical Errors (bad tokens)
     |
 Syntax Analysis   --> catches Syntax Errors (grammar violations)
     |
 Semantic Analysis --> catches Semantic Errors (type mismatches)
     |
 Code Generation & Execution
     |
 Logical Errors --> NOT caught by compiler; found only when output is wrong
```

### 5. Example
```
1. @count = 10;              → Lexical Error ('@' invalid)
2. if (count > 5             → Syntax Error (missing closing parenthesis)
3. int count = "ten";        → Semantic Error (type mismatch)
4. average = total * count;  → Logical Error (should be total / count)
```

### 6. Advantages (of error classification)
- Helps programmers and compiler designers pinpoint exactly where a problem occurs.
- Enables the compiler to give precise, phase-specific error messages.
- Improves debugging efficiency.

### 7. Limitations
- Logical errors cannot be detected by the compiler at all — they require testing and manual debugging.
- Some errors may cascade (one early lexical/syntax error can trigger multiple false subsequent errors).

### 8. Applications
- Directly used in building error handlers/reporting systems in real compilers.
- Important in IDEs for real-time syntax/semantic error highlighting.

### 9. Conclusion
Compiler errors are classified as Lexical, Syntax, Semantic, or Logical based on which phase (or neither, in the case of logical errors) detects them — understanding this classification is key to effective debugging and to appreciating the responsibility each compiler phase carries.

---

## Part 3: Diagram
(Use the phase-wise error detection flow diagram above.)

---

## Part 4: Examiner Keywords
**Lexical Error**, **Syntax Error**, **Semantic Error**, **Logical Error**, Error Handler, Type Mismatch, Grammar Violation, Runtime Error

---

## Part 5: PYQ Notes
- **Expected Marks:** 6 marks
- **Previous Frequency:** High — commonly asked as "differentiate with examples"
- **Common Mistakes:** Confusing semantic and logical errors (semantic = type/meaning issue caught by compiler; logical = compiler can't catch, wrong algorithm)
- **Related Questions:** "What is error recovery? Explain panic mode recovery"

---

## Part 6: Revision Box
- Lexical error = bad token/character (caught by lexical analyzer)
- Syntax error = grammar violation (caught by parser)
- Semantic error = type/meaning issue (caught by semantic analyzer)
- Logical error = compiles fine, wrong output (NOT caught by compiler)
- Order of detection: Lexical → Syntax → Semantic → (Logical found only at runtime)

---

## Part 7: Expected Viva Questions
1. Which error type is never detected by the compiler?
2. Give an example of a semantic error.
3. What is panic mode error recovery?
4. Can a syntax error occur even if there are no lexical errors?
5. Why can't the compiler detect logical errors?

---

## Part 8: Memory Trick
**"LSSL"** — Lexical (token), Syntax (grammar), Semantic (meaning), Logical (result) — in the exact order the compiler would encounter them (except Logical, which comes only after running).

---
---

# Q15 (Unit 2)

**Question:**
Explain Predictive Parsing (LL(1) Parser) with a suitable example.

**Probability:** ★★★★☆ (High)

**Why Important:**
- Direct conceptual counterpart to Q3 (FIRST/FOLLOW + table) — this version focuses on the **parser mechanism itself** (stack-based working), often asked separately.
- Frequently tested with a parsing trace/stack simulation, which is easy to score if practiced.
- Core Unit 2 topic.

---

## Part 1: Hinglish Concept

**Ye hota kya hai?**
Predictive Parser ek **top-down parser** hai jo bina backtracking kiye, sirf **ek input symbol (lookahead)** dekh kar decide kar leta hai ki kaunsa production use karna hai. Isko **LL(1) Parser** bhi kehte hai — 1 lookahead symbol use karta hai isliye "(1)".

**Real life example:** Socho tum ek decision tree follow kar rahe ho jaha har step par sirf agla ek clue dekh kar turant sahi raasta choose kar lete ho — bina peeche jaake dobara try kiye. Ye hi predictive parsing hai.

**Kaise kaam karta hai?**
Ek **stack** hota hai (jisme grammar symbols hote hai) aur ek **input buffer**. Parser stack ke top aur input ke current symbol ko compare karta hai, aur **LL(1) table** dekh kar decide karta hai kya karna hai — expand karna hai ya match karna hai.

**Exam me isse kya puch sakte hai?**
- Explain working with stack-based model
- Trace parsing of a string using stack + input + table

---

## Part 2: English Exam Answer

### 1. Definition
A **Predictive Parser (LL(1) Parser)** is a top-down, table-driven parser that parses input using a stack and a single lookahead symbol, without backtracking, by consulting a precomputed LL(1) parsing table.

### 2. Introduction
Predictive parsing works only for grammars that are left-recursion-free, left-factored, and satisfy the LL(1) property (no conflicting table entries). It uses the FIRST and FOLLOW sets (from Q3) to build the table that drives its stack-based operation.

### 3. Working / Steps

**Components:**
- A **stack** containing grammar symbols, initialized with the start symbol and end marker `$`.
- An **input buffer** containing the input string followed by `$`.
- An **LL(1) parsing table** M[Non-terminal, terminal].

**Algorithm:**
1. Push `$` then the start symbol onto the stack.
2. Compare the top of stack (X) with current input symbol (a):
   - If X is a terminal and X = a → pop X, advance input pointer (**match**).
   - If X is a non-terminal → look up M[X, a]:
     - If it gives a production X → Y1Y2...Yn, pop X and push Yn...Y1 (reversed) onto the stack.
     - If the table entry is blank → **syntax error**.
3. Repeat until stack and input both contain only `$` → **string accepted**.

### 4. Diagram

```
   INPUT: id + id * id $
                |
   +-----------------------+
   |    STACK   <---->  LL(1) TABLE
   |  E$                    |
   +-----------------------+
                |
     match terminal / expand non-terminal
                |
        Accept when stack = $ and input = $
```

### 5. Example — Parsing `id + id * id $` using grammar:
```
E  → T E'
E' → + T E' | ε
T  → F T'
T' → * F T' | ε
F  → (E) | id
```

| Stack | Input | Action |
|---|---|---|
| E$ | id+id*id$ | E → TE' |
| TE'$ | id+id*id$ | T → FT' |
| FT'E'$ | id+id*id$ | F → id |
| idT'E'$ | id+id*id$ | match id |
| T'E'$ | +id*id$ | T' → ε |
| E'$ | +id*id$ | E' → +TE' |
| +TE'$ | +id*id$ | match + |
| TE'$ | id*id$ | ... continues similarly until stack = $ and input = $ (accept) |

### 6. Advantages
- No backtracking needed — fast and deterministic.
- Easy to implement using a simple stack-based algorithm.
- Errors detected as soon as they occur (blank table entry).

### 7. Limitations
- Only works for LL(1) grammars — grammar must be left-recursion-free and left-factored first.
- Cannot handle ambiguous grammars.
- Limited to 1 symbol of lookahead — some languages need more context.

### 8. Applications
- Used to build simple hand-written or table-driven parsers for arithmetic expressions, configuration languages, etc.
- Basis of recursive descent parsers used in many compilers/interpreters.

### 9. Conclusion
Predictive (LL(1)) parsing is an efficient, backtrack-free, top-down parsing technique that uses a stack and a precomputed table (built from FIRST/FOLLOW sets) to parse valid strings by matching terminals and expanding non-terminals one lookahead symbol at a time.

---

## Part 3: Diagram
(Use the stack ↔ table interaction diagram above, along with the parsing trace table.)

---

## Part 4: Examiner Keywords
**Predictive Parser**, **LL(1)**, Stack, Lookahead, **Match**, **Expand**, Parsing Table, Top-Down Parsing, No Backtracking

---

## Part 5: PYQ Notes
- **Expected Marks:** 8 marks (especially when a full parsing trace is required)
- **Previous Frequency:** High — often follows immediately after a FIRST/FOLLOW/table question
- **Common Mistakes:** Pushing production symbols onto stack in the wrong order (must push in reverse); forgetting to include `$` at the bottom of stack and end of input
- **Related Questions:** "What is a recursive descent parser?", "Difference between recursive descent and predictive parsing"

---

## Part 6: Revision Box
- LL(1) = Left-to-right scan, Leftmost derivation, 1 lookahead
- Uses stack + input buffer + LL(1) table
- Match terminal = pop & advance; non-terminal = expand using table
- Push production symbols in REVERSE order onto stack
- Accept when both stack and input reach `$`

---

## Part 7: Expected Viva Questions
1. Why must production symbols be pushed onto the stack in reverse order?
2. What causes a "syntax error" during predictive parsing?
3. What is the difference between predictive parsing and recursive descent parsing?
4. What are the 3 components used in table-driven predictive parsing?
5. Why can't predictive parsing handle left-recursive grammars directly?

---

## Part 8: Memory Trick
**"Stack Top se Match karo, ya Table se Expand karo — jab tak dono $ pe na aa jaye."**

---
---

# Q16 (Unit 2)

**Question:**
Differentiate FIRST and FOLLOW sets. Explain the construction of an LL(1) Parsing Table.

**Probability:** ★★★★☆ (High)

**Why Important:**
- A "differentiate" framing of Q3 — DBATU often asks the same core concept in a comparison format, so it's worth preparing this exact phrasing separately.
- Table construction rules are often asked as a standalone theory question, even without a full numerical.

---

## Part 1: Hinglish Concept

Ye same concept hai jo Q3 me cover kiya (FIRST/FOLLOW), bas is baar seedha **"differentiate"** the format me pucha jaata hai, aur table banane ke steps zyada explicitly puchte hai.

**Yaad rakhne wali baat:** FIRST ek **non-terminal ke andar** dekhta hai (uske definition ke first symbol), FOLLOW **grammar ke bahar** dekhta hai (us non-terminal ke context me uske baad kya aata hai). Ye dono ekdum opposite direction me kaam karte hai lekin dono milke LL(1) table banate hai.

---

## Part 2: English Exam Answer

### 1. Definition
**FIRST(A):** The set of terminal symbols that can appear as the first symbol of some string derived from A.
**FOLLOW(A):** The set of terminal symbols that can appear immediately after A in some sentential form derived from the start symbol.

### 2. Introduction
While FIRST looks *inward* into what a non-terminal itself can generate, FOLLOW looks *outward* into the grammar context surrounding that non-terminal. Both are essential inputs for constructing the LL(1) parsing table.

### 3. Working / Steps

**Differentiation Table:**

| Aspect | FIRST | FOLLOW |
|---|---|---|
| Meaning | Terminals that begin strings derived from A | Terminals that can follow A in some derivation |
| Direction | Looks into A's own productions | Looks at what comes after A elsewhere in grammar |
| Computed for | Any grammar symbol (terminal or non-terminal) | Only non-terminals |
| Includes `$`? | No | Yes, for the start symbol |
| Includes ε? | Yes, if A can derive ε | No, ε is never part of FOLLOW |

**Construction of LL(1) Parsing Table (Algorithm):**
1. Compute FIRST and FOLLOW sets for all non-terminals.
2. For each production A → α:
   - For every terminal `a` in FIRST(α): set Table[A, a] = A → α.
   - If ε ∈ FIRST(α): for every terminal `b` in FOLLOW(A), set Table[A, b] = A → α.
3. All undefined table entries are marked as **error**.
4. If any cell gets more than one production → grammar is **not LL(1)**.

### 4. Diagram

```
 FIRST(A) -------> looks INSIDE A's productions
 FOLLOW(A) ------> looks at context AFTER A appears

           +-----------------------------+
 A -> α    |  FIRST(α) --> Table[A, a]   |
           |  if ε in FIRST(α):          |
           |   FOLLOW(A) --> Table[A, b] |
           +-----------------------------+
```

### 5. Example
For `E' → +TE' | ε`:
- FIRST(E') = {+, ε}
- Since ε ∈ FIRST(E'), we also add `E' → ε` under every terminal in FOLLOW(E') = {), $}
- Table entries: Table[E', +] = E'→+TE' ; Table[E', )] = E'→ε ; Table[E', $] = E'→ε

### 6. Advantages
- Clear separation of "what can start" vs "what can follow" simplifies table construction.
- Table-driven approach avoids backtracking during parsing.

### 7. Limitations
- Computing FIRST/FOLLOW by hand for large grammars is tedious and error-prone.
- If a table cell has multiple entries, the grammar cannot be parsed with a simple LL(1) parser.

### 8. Applications
- Backbone of predictive parser and parser generator construction (e.g., ANTLR).

### 9. Conclusion
FIRST and FOLLOW sets serve complementary roles — FIRST determines which productions apply based on the current input symbol, while FOLLOW extends this to handle ε-productions — together enabling systematic construction of the LL(1) parsing table.

---

## Part 3: Diagram
(Use the FIRST/FOLLOW → Table construction diagram above.)

---

## Part 4: Examiner Keywords
**FIRST**, **FOLLOW**, LL(1) Table, Epsilon Production, Lookahead, Table Construction Rule

---

## Part 5: PYQ Notes
- **Expected Marks:** 6–8 marks
- **Previous Frequency:** High — the "differentiate" framing is a repeated variant
- **Common Mistakes:** Saying FOLLOW includes ε (it never does); forgetting FOLLOW is defined only for non-terminals
- **Related Questions:** See Q3 for the fully worked numerical example.

---

## Part 6: Revision Box
- FIRST = what can start a derivation from A
- FOLLOW = what can come right after A
- FIRST computed for any symbol; FOLLOW only for non-terminals
- ε can be in FIRST, never in FOLLOW
- Table rule: FIRST(α) → normal entries; ε in FIRST(α) → also use FOLLOW(A)

---

## Part 7: Expected Viva Questions
1. Can FOLLOW ever contain ε?
2. Is FIRST defined for terminals too?
3. What happens if a table cell has two productions?
4. Why does FOLLOW(start symbol) always include `$`?
5. Give one real difference between FIRST and FOLLOW.

---

## Part 8: Memory Trick
**"FIRST = Andar dekho, FOLLOW = Bahar dekho."**

---
---

# Q17 (Unit 3)

**Question:**
Explain Operator Precedence Parsing with a suitable example.

**Probability:** ★★★★☆ (High)

**Why Important:**
- A distinct bottom-up parsing technique from LR parsing — commonly tested as a separate Unit 3 question.
- Simpler than full LR parsing, so it's a good "quick win" if LR parsing feels too heavy.
- Tests understanding of precedence relations between terminals.

---

## Part 1: Hinglish Concept

**Ye hota kya hai?**
Operator Precedence Parsing ek **bottom-up parsing technique** hai jo sirf un grammars ke liye kaam karti hai jisme operators (`+`, `*`, etc.) ke beech clear **precedence relations** define ho.

**Real life example:** Tumhe pata hai maths me `*` `+` se pehle solve hota hai (BODMAS rule). Operator precedence parser bhi bilkul yehi karta hai — do operators ke beech relation define karta hai: kaun "chhota" (yields precedence <), "bada" (yields precedence >), ya "barabar" (=) hai.

**3 Relations:**
- `a ⋖ b` : a ka precedence b se kam hai (a yields precedence to b)
- `a ⋗ b` : a ka precedence b se zyada hai
- `a ≐ b` : dono barabar precedence ke hai (usually matching brackets)

**Ye kyu use hota hai?**
Simple arithmetic expression jaisi grammars ko parse karne ke liye — bina poori LR table banaye, sirf ek chhoti precedence table se kaam chal jaata hai.

**Exam me isse kya puch sakte hai?**
- Define + explain the 3 relations
- Construct a precedence table for a small grammar
- Parse a string using the precedence relations

---

## Part 2: English Exam Answer

### 1. Definition
**Operator Precedence Parsing** is a simple bottom-up parsing technique applicable to a restricted class of grammars called **operator grammars** (no two adjacent non-terminals, no ε-productions), which uses precedence relations between terminal symbols to guide shift/reduce decisions.

### 2. Introduction
Instead of building a full LR parsing table, operator precedence parsing defines three simple relations between pairs of terminals — `⋖` (yields precedence), `⋗` (takes precedence), and `≐` (equal precedence) — to decide when to shift and when to reduce.

### 3. Working / Steps

**Precedence Relations:**
- `a ⋖ b`: a has lower precedence than b → shift.
- `a ⋗ b`: a has higher precedence than b → reduce.
- `a ≐ b`: equal precedence (typically matched brackets) → shift.

**Algorithm:**
1. Construct a precedence relation table between all pairs of terminals based on operator precedence and associativity.
2. Initialize a stack with `$`.
3. Scan input; compare the topmost terminal on the stack with the current input symbol using the precedence table.
4. If relation is `⋖` or `≐` → **shift** the input symbol.
5. If relation is `⋗` → **reduce** by popping the handle from the stack.
6. Repeat until input and stack are exhausted, then accept if valid.

### 4. Diagram

```
Precedence Table for + and * (with id):

     |  id  |  +   |  *   |  $  |
-----|------|------|------|-----|
 id  |      |  ⋗   |  ⋗   |  ⋗  |
 +   |  ⋖   |  ⋗   |  ⋖   |  ⋗  |
 *   |  ⋖   |  ⋗   |  ⋗   |  ⋗  |
 $   |  ⋖   |  ⋖   |  ⋖   |     |
```

### 5. Example
For expression `id + id * id`, since `*` has higher precedence than `+` (i.e., `+ ⋖ *`), the parser shifts through `*` first, ensuring `id*id` is reduced before combining with `+`, correctly reflecting operator precedence — matching real mathematical evaluation order.

### 6. Advantages
- Simple to implement without constructing a full LR automaton.
- Fast for small, well-structured operator grammars.
- Easy to understand and hand-trace.

### 7. Limitations
- Works only for a limited class of grammars (operator grammars).
- Cannot handle grammars with adjacent non-terminals or ε-productions.
- Less powerful than full LR parsing — cannot handle arbitrary context-free grammars.

### 8. Applications
- Historically used in early compilers for parsing arithmetic expressions.
- Useful in simple expression evaluators and calculators.

### 9. Conclusion
Operator precedence parsing is a lightweight bottom-up technique that uses precedence relations between terminal symbols to correctly parse operator-based expressions, trading some generality for simplicity compared to full LR parsing.

---

## Part 3: Diagram
(Use the precedence relation table above.)

---

## Part 4: Examiner Keywords
**Operator Precedence Parsing**, Operator Grammar, **Yields Precedence (⋖)**, **Takes Precedence (⋗)**, Equal Precedence (≐), Shift, Reduce, Handle

---

## Part 5: PYQ Notes
- **Expected Marks:** 6–8 marks
- **Previous Frequency:** High — asked as a distinct alternative to full LR parsing questions
- **Common Mistakes:** Confusing the direction of ⋖ and ⋗; forgetting that operator grammars cannot have two adjacent non-terminals
- **Related Questions:** "What is an operator grammar?"

---

## Part 6: Revision Box
- Operator precedence parsing works only on operator grammars
- 3 relations: ⋖ (shift), ⋗ (reduce), ≐ (equal, shift — usually brackets)
- Simpler than full LR table but less powerful
- Table built based on operator precedence + associativity
- Used mainly for arithmetic expression parsing

---

## Part 7: Expected Viva Questions
1. What is an operator grammar?
2. What does the `⋗` relation mean?
3. Why can't operator precedence parsing handle all context-free grammars?
4. How is bracket matching handled in this technique?
5. Compare operator precedence parsing with LR parsing in terms of power.

---

## Part 8: Memory Trick
**"⋖ = Shift (chhota, aage badho), ⋗ = Reduce (bada, wapas simplify karo)."**

---
---

# Q18 (Unit 3)

**Question:**
Explain LR Parsing. Compare LR(0), SLR(1), CLR(1), and LALR(1) Parsers.

**Probability:** ★★★★★ (Very High)

**Why Important:**
- Direct extension of Q9 — this comparison-style question is extremely common as either a standalone theory question or the "theory part" before an SLR table numerical.
- Tests conceptual depth beyond just SLR construction — a favorite for full marks if a clean comparison table is used.
- One of the highest-weight topics in the entire syllabus.

---

## Part 1: Hinglish Concept

**Ye hota kya hai?**
LR parsing family me 4 variants hote hai — sab **bottom-up** parsers hai, bas unke **power aur complexity** alag hai:
- **LR(0):** Sabse simple, lookahead use hi nahi karta decision lene ke liye (sirf items ka structure dekhta hai)
- **SLR(1):** LR(0) items + FOLLOW set use karta hai reduce decide karne ke liye (Q9 me yehi banaya tha)
- **CLR(1) (Canonical LR):** Har item ke sath specific lookahead attach karta hai — sabse powerful, lekin bahut zyada states banti hai (bada table)
- **LALR(1):** CLR(1) jaisa powerful (lagbhag), lekin similar states ko merge karke table chhota kar deta hai — practically most compilers isi ko use karte hai (jaise YACC)

**Real life example:** Socho 4 log same kaam kar rahe hai — checking documents:
- LR(0) = bina kuch dekhe hi approve/reject kar deta hai (bahut basic)
- SLR = ek general rule list dekh kar decide karta hai (FOLLOW set)
- CLR = har case ko individually, poori detail ke sath check karta hai (sabse accurate lekin slow/bada)
- LALR = CLR jaisa hi accurate, lekin similar cases ko group karke fast kar deta hai

**Exam me isse kya puch sakte hai?**
- Explain each briefly
- Comparison table: power, table size, conflicts

---

## Part 2: English Exam Answer

### 1. Definition
**LR Parsing** is a family of bottom-up parsing techniques that scan input left to right and construct a rightmost derivation in reverse. The family includes four variants — **LR(0)**, **SLR(1)**, **CLR(1)**, and **LALR(1)** — differing in how much lookahead information they use and how large their parsing tables become.

### 2. Introduction
As grammars become more complex, plain LR(0) items are often insufficient to avoid conflicts. Each successive variant (SLR → CLR → LALR) adds more precision using lookahead symbols, trading off table size against parsing power.

### 3. Working / Steps — Explanation of Each Variant

1. **LR(0):** Uses only LR(0) items (no lookahead) to decide shift/reduce actions. Weakest — many grammars cause conflicts.

2. **SLR(1) (Simple LR):** Uses LR(0) items, but resolves reduce actions using the **FOLLOW set** of the non-terminal. Simple to construct, moderate power (see Q9 for full example).

3. **CLR(1) (Canonical LR):** Uses **LR(1) items**, where each item carries a specific lookahead symbol relevant to that particular context (not the whole FOLLOW set). Most powerful and precise, but produces a very large number of states/table size.

4. **LALR(1) (Look-Ahead LR):** Constructs the same states as CLR(1), but then **merges states with identical cores** (same productions, different lookaheads combined). Almost as powerful as CLR(1), with a table size close to SLR(1) — this is the most practically used variant.

### 4. Diagram

```
   Parsing Power:   LR(0)  <  SLR(1)  <  LALR(1)  <=  CLR(1)
   Table Size:      LR(0)  <  SLR(1)  ~  LALR(1)  <<  CLR(1)

        (weakest, smallest)  ------------------->  (strongest, largest)
```

### 5. Comparison Table

| Feature | LR(0) | SLR(1) | CLR(1) | LALR(1) |
|---|---|---|---|---|
| Lookahead used | None | FOLLOW set | Specific per-item lookahead | Specific (merged states) |
| Parsing Power | Lowest | Moderate | Highest | High (almost = CLR) |
| Number of States | Fewer | Same as LR(0) | Very large | Same as SLR(1)/LR(0) |
| Conflicts | Most likely | Some resolved | Fewest | Slightly more than CLR (due to merging) |
| Practical Use | Rarely used alone | Used for simple grammars | Rare (table too large) | Most widely used (e.g., YACC) |

### 6. Advantages
- Provides a spectrum of trade-offs between simplicity and power, letting compiler designers choose based on grammar complexity.
- LALR(1) in particular gives near-CLR power with practical table sizes.

### 7. Limitations
- LR(0) and SLR(1) fail on many real grammars due to conflicts.
- CLR(1) is theoretically the most powerful but impractical due to huge table size.
- LALR(1) merging can occasionally introduce new reduce-reduce conflicts not present in CLR(1).

### 8. Applications
- LALR(1) is used by real-world parser generators like **YACC** and **Bison**.
- SLR(1) is commonly taught and used for simpler academic grammars.

### 9. Conclusion
The four LR parser variants — LR(0), SLR(1), CLR(1), and LALR(1) — represent increasing levels of parsing power achieved by using more precise lookahead information, with LALR(1) offering the best practical balance of power and table size, making it the standard choice in real compilers.

---

## Part 3: Diagram
(Use the power/table-size spectrum diagram and comparison table above.)

---

## Part 4: Examiner Keywords
**LR(0)**, **SLR(1)**, **CLR(1)**, **LALR(1)**, LR(1) Items, Lookahead, State Merging, Reduce-Reduce Conflict, Shift-Reduce Conflict

---

## Part 5: PYQ Notes
- **Expected Marks:** 8 marks (theory-only version); often follows a Q9-style SLR numerical
- **Previous Frequency:** Very high — one of the most consistently repeated theory questions in Unit 3
- **Common Mistakes:** Saying LALR(1) is always stronger than CLR(1) (it's not — merging can lose some precision); confusing SLR's FOLLOW-based approach with CLR's per-item lookahead
- **Related Questions:** See Q9 for the fully worked SLR table construction example.

---

## Part 6: Revision Box
- 4 variants: LR(0) < SLR(1) < LALR(1) ≤ CLR(1) in power
- LR(0): no lookahead
- SLR(1): uses FOLLOW set
- CLR(1): per-item specific lookahead, most powerful, largest table
- LALR(1): merges CLR states with same core → practical, most widely used (YACC)

---

## Part 7: Expected Viva Questions
1. Which LR variant is used by YACC?
2. What is the main difference between SLR and CLR?
3. Why is CLR(1) rarely used in practice despite being most powerful?
4. Can LALR(1) introduce conflicts that didn't exist in CLR(1)?
5. Rank the 4 LR variants by parsing power.

---

## Part 8: Memory Trick
**"Sabse Simple Complex Le Aao"** — SLR, (LR0 basic), CLR, LALR — order of increasing sophistication: **LR(0) → SLR → LALR → CLR** in table complexity terms, but power-wise LALR sits just under CLR.

---
---

# Q19 (Unit 4)

**Question:**
Explain Syntax Tree and Directed Acyclic Graph (DAG). State their applications in compiler design.

**Probability:** ★★★★☆ (High)

**Why Important:**
- Bridges Unit 2 (parsing/syntax trees) and Unit 4 (DAG/optimization) — a comparison-style question DBATU likes to ask.
- Reinforces the DAG concept from Q8 but from a "compare with syntax tree" angle.
- Good scoring opportunity since both structures are visually easy to draw and explain.

---

## Part 1: Hinglish Concept

**Ye hota kya hai?**
**Syntax Tree** ek tree hai jo ek expression/statement ka structure dikhata hai — har operation ek node hoti hai, aur agar same sub-expression do baar aaye, to tree me wo do baar (alag nodes) dikhega, chahe wo same ho.

**DAG (Directed Acyclic Graph)** bhi structure dikhata hai, lekin agar same sub-expression repeat ho, to DAG usko **ek hi node** me represent karta hai (share karta hai) — repeat nahi karta.

**Real life example:** Socho tumhe do baar "2+3" calculate karna hai apni recipe me. Syntax tree har baar alag se "2+3" likhega (do jagah), jaise ek notebook me repeat likh dena. DAG smart hai — ek baar "2+3" calculate karke result ko dono jagah reuse kar lega (ek hi node share karega).

**Ye kyu use hote hai?**
- Syntax tree: structure samajhne ke liye, code generation ke basic representation ke liye
- DAG: redundant calculations hatane (optimization) ke liye

**Exam me isse kya puch sakte hai?**
- Difference between syntax tree and DAG
- Construct both for a given expression
- Applications of each in compiler phases

---

## Part 2: English Exam Answer

### 1. Definition
A **Syntax Tree** is a tree representation of an expression/statement where each interior node represents an operator and each leaf represents an operand, with every occurrence of a sub-expression represented separately.
A **DAG (Directed Acyclic Graph)** is a similar graph representation, but identical (common) sub-expressions are represented by a single shared node instead of being duplicated.

### 2. Introduction
Both structures are built during/after semantic analysis to represent the structure of expressions within a basic block. While the syntax tree faithfully mirrors the expression's structure (including duplicates), the DAG compresses this by merging identical sub-expressions, directly enabling optimization.

### 3. Working / Steps

**Difference Table:**

| Feature | Syntax Tree | DAG |
|---|---|---|
| Common sub-expressions | Represented separately (duplicated) | Represented once (shared node) |
| Structure | Strict tree (no shared nodes) | Graph (nodes can have multiple parents) |
| Purpose | Represents syntactic structure | Reveals redundancy for optimization |
| Size | Larger (duplicates included) | Smaller (redundancy removed) |

**Construction rule for both:** for `x = y op z`, create a node labeled `op` with children `y` and `z` — the ONLY difference is that DAG reuses an existing identical node if available, while a syntax tree always creates a new one.

### 4. Diagram

For expression: `a = (b + c) * (b + c)`

**Syntax Tree (duplicated):**
```
              =
            /   \
           a     *
                / \
               +   +
              / \ / \
             b  c b  c
```

**DAG (shared node):**
```
              =
            /   \
           a     *
                / \
               +---+ (same node reused for both (b+c))
              / \
             b   c
```

### 5. Example
As shown above, the DAG uses only ONE `+` node for both occurrences of `b + c`, while the syntax tree has two separate `+` nodes — showing the DAG's advantage in spotting redundancy.

### 6. Advantages
- **Syntax Tree:** Simple, faithful representation; easy to generate directly from grammar/parse tree.
- **DAG:** Automatically reveals and eliminates common sub-expressions, reducing code size and computation.

### 7. Limitations
- **Syntax Tree:** Does not detect redundant computations — can lead to inefficient code if used directly for code generation.
- **DAG:** Slightly more complex to construct than a syntax tree due to the need to check for existing identical nodes.

### 8. Applications
- **Syntax Tree:** Used for generating intermediate code, representing program structure for semantic analysis.
- **DAG:** Used in code optimization phase (see Q8) for common sub-expression elimination within basic blocks; also used to determine which computations are needed for the final result.

### 9. Conclusion
Both syntax trees and DAGs represent the structure of an expression, but a DAG improves upon the syntax tree by merging identical sub-expressions into shared nodes, making it a valuable tool for detecting redundancy and enabling code optimization.

---

## Part 3: Diagram
(Use both tree diagrams above, drawn side by side to clearly show the shared node in the DAG.)

---

## Part 4: Examiner Keywords
**Syntax Tree**, **DAG (Directed Acyclic Graph)**, Shared Node, Common Sub-expression, Basic Block, Redundancy Elimination

---

## Part 5: PYQ Notes
- **Expected Marks:** 6–8 marks
- **Previous Frequency:** High — often asked as "differentiate with example"
- **Common Mistakes:** Drawing identical trees for both (missing the point of node-sharing in DAG); not clearly labeling shared nodes
- **Related Questions:** See Q8 for a full DAG-based optimization numerical.

---

## Part 6: Revision Box
- Syntax tree: duplicates common sub-expressions
- DAG: shares/merges identical sub-expressions into one node
- Both built from expressions within a basic block
- DAG size ≤ Syntax tree size always
- DAG directly enables optimization; syntax tree does not

---

## Part 7: Expected Viva Questions
1. What is the key structural difference between a syntax tree and a DAG?
2. Why is a DAG smaller than the equivalent syntax tree?
3. How does a DAG help in code optimization?
4. Can a DAG have a node with multiple parents? Can a syntax tree?
5. Which structure would you prefer for detecting common sub-expressions?

---

## Part 8: Memory Trick
**"Tree = Twice likhta hai, DAG = ek baar likh ke Adjust kar leta hai (share karta hai)."**

---
---

# Q20 (Unit 4)

**Question:**
Explain Code Optimization Techniques. Differentiate Machine Independent and Machine Dependent Code Optimization.

**Probability:** ★★★★★ (Very High)

**Why Important:**
- Ties together Q8 (DAG-based optimization) and Q12 (Peephole optimization) into a single high-level comparison — a very common way DBATU frames the "big picture" optimization question.
- Comparison-style questions are consistently repeated and easy to score with a clean table.
- One of the highest-probability Unit 4 questions overall.

---

## Part 1: Hinglish Concept

**Ye hota kya hai?**
Code optimization do broad categories me divide hota hai:
1. **Machine Independent Optimization** — ye optimization **kisi bhi machine/hardware ke liye same** hoti hai. Ye intermediate code (jaise three-address code) par apply hoti hai, target machine ki details ka koi role nahi hota.
2. **Machine Dependent Optimization** — ye optimization **specific machine/hardware ko dhyan me rakh kar** ki jaati hai — jaise register allocation, kyuki har machine ke registers alag number/type ke hote hai.

**Real life example:** Socho tum ek recipe optimize kar rahe ho:
- Machine independent = "ek step hata do jo useless hai" — ye kisi bhi kitchen me apply hoga
- Machine dependent = "is specific oven me temperature 180°C use karo kyuki ye oven fast heat karta hai" — ye specific equipment ke hisaab se hai

**Exam me isse kya puch sakte hai?**
- List optimization techniques
- Differentiate machine dependent vs independent with examples

---

## Part 2: English Exam Answer

### 1. Definition
**Code Optimization** is the process of improving intermediate or target code to make it execute faster and/or use less memory, without changing the program's meaning. It is classified into **Machine Independent** and **Machine Dependent** optimization.

### 2. Introduction
Machine-independent optimization works on the intermediate representation (like three-address code) and applies regardless of the target hardware. Machine-dependent optimization is applied to the final target code and depends on the specific architecture (registers, instruction set) of the machine.

### 3. Working / Steps

**Machine Independent Optimization Techniques (apply to intermediate code):**
1. Common Sub-expression Elimination (using DAG — see Q8)
2. Dead Code Elimination
3. Constant Folding (evaluate constants at compile time)
4. Loop Optimization (code motion, loop-invariant computation removal)
5. Copy Propagation

**Machine Dependent Optimization Techniques (apply to target code):**
1. Register Allocation and Assignment (see Q5)
2. Peephole Optimization (see Q12)
3. Instruction Scheduling (reordering instructions to use pipeline efficiently)
4. Use of Machine-Specific Instructions (Machine Idioms)

**Differentiation Table:**

| Feature | Machine Independent | Machine Dependent |
|---|---|---|
| Applied on | Intermediate code | Target/machine code |
| Depends on hardware? | No | Yes |
| Examples | Constant folding, dead code elimination, common sub-expr elimination | Register allocation, peephole optimization, instruction scheduling |
| Portability | Same across all target machines | Specific to a particular CPU architecture |
| When applied | Before code generation | During/after code generation |

### 4. Diagram

```
   Intermediate Code
         |
   +----------------------------+
   | Machine-Independent Opt.    |
   | (constant folding, DAG,     |
   |  dead code elimination)     |
   +----------------------------+
         |
   Code Generation
         |
   +----------------------------+
   | Machine-Dependent Opt.       |
   | (register allocation,        |
   |  peephole optimization)      |
   +----------------------------+
         |
   Final Target Code
```

### 5. Example
```
Machine Independent: x = 2 + 3       →  x = 5   (constant folding)
Machine Dependent:   MOV R1,x; ADD R1,#0  →  (removed, peephole optimization)
```

### 6. Advantages
- Machine-independent optimization improves portability — same optimized intermediate code works for any target.
- Machine-dependent optimization extracts maximum performance from specific hardware (registers, instruction sets).

### 7. Limitations
- Machine-independent optimization alone cannot exploit hardware-specific speedups.
- Machine-dependent optimization must be redone/retuned for every new target architecture.

### 8. Applications
- Machine-independent techniques are used in the "middle-end" of compilers like LLVM (target-agnostic optimization passes).
- Machine-dependent techniques are used in the compiler back-end when generating code for specific CPUs (x86, ARM, etc.).

### 9. Conclusion
Code optimization improves program efficiency through two complementary layers — machine-independent techniques applied to intermediate code for portability, and machine-dependent techniques applied to target code for exploiting specific hardware features — together producing fast, efficient executables.

---

## Part 3: Diagram
(Use the pipeline diagram above showing where each type of optimization is applied relative to code generation.)

---

## Part 4: Examiner Keywords
**Machine Independent Optimization**, **Machine Dependent Optimization**, Constant Folding, Dead Code Elimination, Register Allocation, Peephole Optimization, Instruction Scheduling

---

## Part 5: PYQ Notes
- **Expected Marks:** 8 marks
- **Previous Frequency:** Very high — this "big picture" comparison is one of the most repeated Unit 4 questions
- **Common Mistakes:** Placing peephole optimization under machine-independent (it's machine-dependent); not giving distinct examples for each category
- **Related Questions:** See Q8 (DAG) and Q12 (Peephole) for detailed worked examples of specific techniques.

---

## Part 6: Revision Box
- Machine Independent = works on intermediate code, hardware-agnostic
  → constant folding, dead code elimination, common sub-expr elimination, loop optimization
- Machine Dependent = works on target code, hardware-specific
  → register allocation, peephole optimization, instruction scheduling
- Independent happens BEFORE code generation; Dependent happens DURING/AFTER

---

## Part 7: Expected Viva Questions
1. Is peephole optimization machine-dependent or machine-independent?
2. Give one example each of machine-dependent and machine-independent optimization.
3. Why is register allocation considered machine-dependent?
4. At what stage is machine-independent optimization typically applied?
5. Name a real compiler tool that performs machine-independent optimization passes.

---

## Part 8: Memory Trick
**"Independent = Idea level (intermediate code), Dependent = Device level (target machine)."**

---
---

# COMPLETE MASTER SUMMARY — All 20 Questions

| # | Topic | Probability | Unit |
|---|---|---|---|
| 1 | Compiler Phases + Tools | ★★★★★ | Unit 1 |
| 6 | Lexical Analysis (Token/Lexeme/Pattern) | ★★★★★ | Unit 1 |
| 13 | Symbol Table (Functions/Implementation/Applications) | ★★★★☆ | Unit 1 |
| 14 | Compiler Errors (Lexical/Syntax/Semantic/Logical) | ★★★★☆ | Unit 1 |
| 2 | Left Recursion Elimination | ★★★★★ | Unit 2 |
| 3 | FIRST/FOLLOW + LL(1) Table | ★★★★★ | Unit 2 |
| 10 | Left Factoring | ★★★★☆ | Unit 2 |
| 11 | Ambiguous Grammar | ★★★☆☆ | Unit 2 |
| 15 | Predictive Parsing (LL(1) Parser Working) | ★★★★☆ | Unit 2 |
| 16 | Differentiate FIRST/FOLLOW + Table Construction | ★★★★☆ | Unit 2 |
| 9 | LR Parsing (SLR Table Construction) | ★★★★★ | Unit 3 |
| 17 | Operator Precedence Parsing | ★★★★☆ | Unit 3 |
| 18 | LR(0) vs SLR(1) vs CLR(1) vs LALR(1) Comparison | ★★★★★ | Unit 3 |
| 4 | Type Checking & Conversion | ★★★★☆ | Unit 4 |
| 7 | Symbol Table (basic) | ★★★★☆ | Unit 4/cross-cutting |
| 8 | Code Optimization + DAG | ★★★★☆ | Unit 4 |
| 12 | Peephole Optimization | ★★★☆☆ | Unit 4 |
| 19 | Syntax Tree vs DAG | ★★★★☆ | Unit 4 |
| 20 | Machine Independent vs Dependent Optimization | ★★★★★ | Unit 4 |
| 5 | Code Generation + Registers | ★★★★☆ | Unit 5/6 |

**You now have a complete 20-question bank covering every unit in depth, from basic definitions to full numericals (left recursion, LL(1) table, SLR table, DAG).**

---
---

# GAP-FILL QUESTIONS (Q21–Q30)

*Added based on a 10-paper PYQ frequency analysis to close remaining coverage gaps — includes the two highest-frequency topics overall (Basic Blocks/Flow Graph and SDD/SDT), plus other partially/un-covered areas.*

---
---

# Q21

**Question:**
What is a Basic Block and a Flow Graph? Explain the algorithm to identify leaders and construct basic blocks. Construct the flow graph for the given three-address code.

**Probability:** ★★★★★ (Very High — most repeated numeric problem, 6/10 papers)

**Why Important:**
- The single most repeated **numeric** question across 10 analyzed papers.
- Tests understanding of intermediate code structure — foundation for code optimization (DAG, Q8) and code generation (Q5).
- Almost always uses a loop/array-processing TAC snippet — the method transfers directly to any variant.

---

## Part 1: Hinglish Concept

**Ye hota kya hai?**
**Basic Block** ek group hai three-address code statements ka jisme **control sirf shuru me enter karta hai aur sirf end me exit karta hai** — beech me koi jump in/out nahi hota.

**Flow Graph** ek diagram hai jisme har **basic block ek node** hota hai, aur arrows batate hai ki ek block ke baad control kaunse block me jaa sakta hai.

**Real life example:** Socho ek train journey hai jisme kuch **fixed stations** hai jaha train ruk sakti hai (basic blocks), aur beech me kahin bhi train ruk nahi sakti bina station ke. Flow graph batata hai ki ek station se train agle kaunse station(s) tak jaa sakti hai.

**Leaders kaise dhoondte hai (basic block ka start):**
1. Pehla statement hamesha leader hota hai
2. Jo bhi statement kisi goto ka **target** hai, wo leader hai
3. Jo bhi statement kisi goto/conditional-goto ke **turant baad** aata hai, wo leader hai

**Ye kyu use hota hai?**
Optimization (jaise DAG, common subexpression elimination) hamesha ek basic block ke andar hi ki jaati hai — isliye pehle blocks identify karna zaroori hai.

**Exam me isse kya puch sakte hai?**
- Definition of basic block + flow graph
- Leader-finding algorithm
- Given TAC, find leaders → blocks → draw flow graph

---

## Part 2: English Exam Answer

### 1. Definition
A **Basic Block** is a maximal sequence of consecutive three-address statements in which control enters only at the beginning (the first statement) and leaves only at the end (the last statement), with no jumps into or out of the middle.
A **Flow Graph** is a directed graph whose nodes are basic blocks and whose edges represent the possible flow of control between them (B1 → B2 if control can pass from B1 to B2).

### 2. Introduction
Before performing optimization, a compiler divides the intermediate code (three-address code) into basic blocks so that local optimizations (like DAG-based common sub-expression elimination) can be applied within each block, and global optimizations can be applied across the flow graph.

### 3. Working / Steps

**Algorithm to find Leaders:**
1. The first statement of the program is a leader.
2. Any statement that is the target of a conditional or unconditional `goto` is a leader.
3. Any statement that immediately follows a `goto` or conditional `goto` is a leader.

**Constructing Basic Blocks:** Each basic block consists of a leader and all statements up to (but not including) the next leader.

**Constructing Flow Graph:** Add an edge B1 → B2 if control can flow from the last statement of B1 to the first statement (leader) of B2, either by falling through or via a jump.

### 4. Diagram

```
Flow Graph structure:

     +--------+
     |   B1   |
     +--------+
         |
         v
     +--------+
     |   B2   |<---+
     +--------+    |
         |         |
         +---------+   (self-loop / back-edge if B2 jumps to itself)
```

### 5. Example — Worked Problem (classic array-multiplication loop)

**Given TAC:**
```
(1) prod := 0
(2) i := 1
(3) t1 := 4*i
(4) t2 := a[t1]
(5) t3 := 4*i
(6) t4 := b[t3]
(7) t5 := t2*t4
(8) t6 := prod+t5
(9) prod := t6
(10) t7 := i+1
(11) i := t7
(12) if i<=20 goto (3)
```

**Step 1 — Find Leaders:**
- Statement 1 → leader (first statement)
- Statement 3 → leader (target of goto in statement 12)

**Step 2 — Form Basic Blocks:**
- **B1:** statements 1–2 (`prod := 0`, `i := 1`)
- **B2:** statements 3–12 (loop body, since statement 3 is the target of the back-edge)

**Step 3 — Flow Graph:**
```
B1 → B2               (falls through into loop)
B2 → B2 (self-loop)   (statement 12 jumps back to statement 3)
```

### 6. Advantages
- Basic blocks enable safe, localized optimization without affecting control flow correctness.
- Flow graphs make loop structures (like back-edges) visually obvious, aiding loop optimization.

### 7. Limitations
- Basic block identification only works correctly on straight-line/goto-based intermediate code — needs adaptation for more complex control structures.
- Very fine-grained basic blocks (e.g., due to many jumps) can limit the scope of optimization.

### 8. Applications
- Essential first step before DAG construction (Q8/Q19) and code optimization (Q20).
- Used in loop optimization to detect loops (via back-edges in the flow graph).

### 9. Conclusion
Basic blocks and flow graphs provide a structured way to represent a program's control flow, using the leader-finding algorithm to correctly partition intermediate code — this partitioning is the essential first step before any meaningful code optimization can be performed.

---

## Part 3: Diagram
(Use the flow graph structure above; for the worked example, draw exactly: B1 → B2, with a self-loop arrow on B2.)

---

## Part 4: Examiner Keywords
**Basic Block**, **Flow Graph**, **Leader**, Three-Address Code, Back-edge, Self-loop, Control Flow

---

## Part 5: PYQ Notes
- **Expected Marks:** 8–10 marks (theory + numeric combined)
- **Previous Frequency:** Very high — 6/10 papers, almost always with a 10-12 line TAC using array/loop code
- **Common Mistakes:** Forgetting rule 3 (statement after a goto is also a leader); miscounting which statement is the "target" vs the statement "after" the goto
- **Related Questions:** See Q8 for DAG construction within a basic block (natural follow-up question).

---

## Part 6: Revision Box
- Basic block = control enters at start, exits at end only
- Flow graph = nodes are basic blocks, edges show control flow
- Leader rules: (1) first statement, (2) goto target, (3) statement right after a goto
- Block = leader + statements until next leader
- Self-loop in flow graph = loop back-edge (e.g., `goto` back to loop start)

---

## Part 7: Expected Viva Questions
1. What are the three rules for identifying a leader?
2. Why can't a jump occur into the middle of a basic block?
3. What does a self-loop in a flow graph represent?
4. Why is basic block identification necessary before optimization?
5. What is a back-edge?

---

## Part 8: Memory Trick
**"FTG" — First statement, Target of goto, statement after Goto (3 leader rules).**

---
---

# Q22

**Question:**
What are Syntax Directed Definitions (SDD) and Syntax Directed Translation (SDT)? Explain synthesized and inherited attributes. Construct the annotated parse tree for a given expression.

**Probability:** ★★★★★ (Very High — highest overall frequency, 8/10 papers)

**Why Important:**
- The **single most repeated topic** across all 10 analyzed papers (8/10) — higher priority than even the compiler-phases question.
- Tests semantic analysis concepts and directly connects grammar rules to actual computed values.
- Repeats with only the arithmetic expression changed — one memorized rule table solves any variant.

---

## Part 1: Hinglish Concept

**Ye hota kya hai?**
**SDD (Syntax Directed Definition):** Ek context-free grammar hai jisme har production ke sath **semantic rules** attach hote hai — jo batate hai ki value kaise calculate hogi. Ye sirf "kya karna hai" batata hai, "kaise/kis order me" nahi (declarative).

**SDT (Syntax Directed Translation):** SDD jaisa hi hai, lekin semantic actions **directly production ke andar embed** hote hai `{ }` brackets me, aur ek specific order me execute hote hai parsing ke dauraan.

**Real life example:** Socho tum ek form fill kar rahe ho jisme kuch fields **neeche wale fields se calculate hoti hai** (jaise "Total" = sum of items — ye **synthesized**, bottom se upar aata hai), aur kuch fields **upar se neeche pass hoti hai** (jaise "Currency Type" jo poore form me same rehta hai upar se diya gaya — ye **inherited**, upar se neeche jaata hai).

**Do types of attributes:**
- **Synthesized attribute:** Children se calculate hota hai (bottom-up). Jaise `E.val = E1.val + T.val`
- **Inherited attribute:** Parent/siblings se milta hai (top-down/left-to-right)

**Ye kyu use hota hai?**
Compiler ko expression ka **actual value/meaning** nikalna hota hai parse tree se — SDD/SDT yehi karne ka tarika batate hai.

**Exam me isse kya puch sakte hai?**
- Define SDD/SDT + synthesized/inherited attributes
- Given rule table, annotate parse tree for an expression (calculate final value)
- Write SDT rules to generate Three Address Code

---

## Part 2: English Exam Answer

### 1. Definition
A **Syntax Directed Definition (SDD)** is a context-free grammar where each production is associated with a set of semantic rules that define how attribute values are computed, without specifying the order of evaluation.
A **Syntax Directed Translation (SDT)** is an SDD where semantic actions are embedded directly within the productions and executed in a specific order during parsing.

### 2. Introduction
SDDs and SDTs allow a compiler to compute meaningful values (like expression results, types, or generated code) while parsing, by attaching rules to grammar productions. Attributes are classified as synthesized or inherited based on the direction in which their values flow through the parse tree.

### 3. Working / Steps

**Attribute Types:**
- **Synthesized Attribute:** Computed from the values of child nodes (flows bottom-up). Example: `E.val = E1.val + T.val`.
- **Inherited Attribute:** Computed from parent or sibling nodes (flows top-down or left-to-right). Example: passing a declared `type` down to each identifier in a declaration list.

**SDD Rule Table for Arithmetic Expression:**

| Production | Semantic Rule |
|---|---|
| L → E n | L.val = E.val |
| E → E1 + T | E.val = E1.val + T.val |
| E → T | E.val = T.val |
| T → T1 * F | T.val = T1.val × F.val |
| T → F | T.val = F.val |
| F → (E) | F.val = E.val |
| F → digit | F.val = digit.lexval |

**SDT Rules for generating Three Address Code:**
```
S → id = E     { gen(id.name = E.place); }
E → E1 + T     { E.place = newTemp(); gen(E.place = E1.place + T.place); }
E → T          { E.place = T.place; }
T → T1 * F     { T.place = newTemp(); gen(T.place = T1.place * F.place); }
T → F          { T.place = F.place; }
F → id         { F.place = id.name; }
```

### 4. Diagram — Annotated Parse Tree for `3*5+4`

```
                E.val=19
               /    |    \
           E.val=15 +   T.val=4
          /            |
      T.val=15         F.val=4
     /   |   \             |
  T.val=3 * F.val=5    digit(4)
    |            |
  F.val=3     digit(5)
    |
  digit(3)
```

**Bottom-up computation:** F.val=3, F.val=5 → T.val = 3×5 = 15; F.val=4 → T.val = 4; E.val = 15 + 4 = **19**.

### 5. Example — SDT for `a+b*c`
Applying the TAC-generating SDT rules:
```
t1 = b * c
t2 = a + t1
```

### 6. Advantages
- SDDs give a clean, declarative way to specify semantics without worrying about evaluation order.
- SDTs (with embedded actions) are directly implementable during single-pass parsing, generating code on the fly.
- Enables systematic computation of types, values, and intermediate code.

### 7. Limitations
- Complex inherited attribute dependencies can require multiple tree traversals.
- Not all SDDs can be easily converted into an efficient one-pass SDT (order of evaluation matters).
- Attribute grammars can become hard to manage for large/complex languages.

### 8. Applications
- Used in semantic analysis phase for type-checking.
- Used directly to generate three-address/intermediate code during parsing.
- Basis of tools like YACC, which allow embedding semantic actions in grammar rules.

### 9. Conclusion
Syntax Directed Definitions and Translations connect grammar productions to computed meanings using synthesized and inherited attributes, enabling a compiler to evaluate expressions, check types, and generate intermediate code directly during parsing — making this one of the most fundamental and frequently tested topics in compiler design.

---

## Part 3: Diagram
(Use the annotated parse tree for `3*5+4` above — practice drawing it exactly as shown with values at each node.)

---

## Part 4: Examiner Keywords
**SDD**, **SDT**, **Synthesized Attribute**, **Inherited Attribute**, Annotated Parse Tree, Semantic Rule, `newTemp()`, `gen()`

---

## Part 5: PYQ Notes
- **Expected Marks:** 8–10 marks (the single highest-priority topic based on frequency — 8/10 papers)
- **Previous Frequency:** Extremely high — repeats with only the expression changed (e.g., `3*5+4`, `a+b*c`)
- **Common Mistakes:** Mixing up synthesized (bottom-up) and inherited (top-down) directions; forgetting `newTemp()` when generating TAC in SDT
- **Related Questions:** "What is L-attributed and S-attributed grammar?", "Write SDT for if-else statement" (see Q25)

---

## Part 6: Revision Box
- SDD = grammar + semantic rules (declarative, order not fixed)
- SDT = SDD with embedded actions `{ }`, executed in fixed order
- Synthesized = from children (bottom-up); Inherited = from parent/siblings (top-down)
- Memorize the E→E+T / T→T*F / F→digit rule table — it solves any expression variant
- TAC-generating SDT uses `newTemp()` and `gen()`

---

## Part 7: Expected Viva Questions
1. What is the difference between SDD and SDT?
2. Give an example of a synthesized attribute vs an inherited attribute.
3. What does `newTemp()` do in an SDT rule?
4. Is `E.val = E1.val + T.val` synthesized or inherited? Why?
5. Why do inherited attributes sometimes require special evaluation order?

---

## Part 8: Memory Trick
**"Synthesized = Sons/children batate hai (bottom-up), Inherited = Inherited from parent (top-down)."**

---
---

# Q23

**Question:**
Explain Regular Expressions, Finite Automata, and their conversion using Thompson's Construction (RE→NFA) and Subset Construction (NFA→DFA).

**Probability:** ★★★★☆ (High — 6/10 papers)

**Why Important:**
- Core Unit 1 topic connecting lexical analysis theory to formal automata — frequently tested with a specific regex to convert.
- Tests two distinct algorithms together — high mark value (8-10 marks).
- The construction method transfers directly to any regex variant given in the exam.

---

## Part 1: Hinglish Concept

**Ye hota kya hai?**
**Regular Expression (RE)** ek formula hai jo batata hai kis pattern ke strings valid hai (jaise identifier ka pattern). Lexical analyzer inhi patterns ko match karke tokens banata hai.

Lekin compiler ko RE ko directly "run" karna mushkil hai, isliye usse pehle **NFA (Non-deterministic Finite Automaton)** me convert karte hai (Thompson's Construction se), phir **DFA (Deterministic Finite Automaton)** me (Subset Construction se) — kyuki DFA implement karna easy aur fast hota hai.

**Real life example:** Socho RE ek recipe hai jo bata rahi hai "kya-kya ingredients chahiye" (general description). NFA usse ek rough step-by-step process me convert karta hai jisme multiple raste ho sakte hai ek hi result tak pohochne ke (non-deterministic — confusion allowed). DFA usse ek **clear, single-path** process bana deta hai — har step par exactly ek hi decision hota hai.

**Ye kyu use hota hai?**
- Thompson's Construction: RE → NFA banane ke liye (small NFAs jodo union/concat/star operations se)
- Subset Construction: NFA → DFA (kyuki DFA fast aur deterministic hota hai, lexical analyzer ke liye best)

**Exam me isse kya puch sakte hai?**
- Ek diya gaya regex (jaise `(a|b)*abb`) ka NFA banao Thompson's Construction se
- Fir usko DFA me convert karo Subset Construction se

---

## Part 2: English Exam Answer

### 1. Definition
A **Regular Expression** is a notation used to describe patterns of strings (used to define tokens in lexical analysis). **Thompson's Construction** converts a regular expression into an equivalent **NFA**. **Subset Construction** converts an NFA into an equivalent **DFA**.

### 2. Introduction
Since directly matching a regular expression against input is inefficient, compilers convert regular expressions into automata: first an NFA (which may have multiple possible transitions or ε-moves), then a DFA (with exactly one transition per input symbol per state), which is fast and simple to implement as a lexical analyzer.

### 3. Working / Steps

**Thompson's Construction Rules (RE → NFA):**
1. For a single symbol `a`: create a 2-state NFA with a transition on `a`.
2. For **union** `r1|r2`: create a new start state with ε-transitions to both NFAs' starts, and both NFAs' ends have ε-transitions to a new final state.
3. For **concatenation** `r1r2`: connect the final state of r1's NFA to the start state of r2's NFA via ε.
4. For **Kleene star** `r*`: add ε-transitions allowing the NFA to repeat zero or more times, with a bypass ε-transition for zero occurrences.

**Subset Construction Algorithm (NFA → DFA):**
1. Compute **ε-closure** of the NFA's start state → this becomes the DFA's start state.
2. For each DFA state (a set of NFA states) and each input symbol, compute `move()` followed by `ε-closure()` to get the next DFA state.
3. Repeat until no new DFA states are generated.
4. Any DFA state containing an NFA accepting state becomes a DFA accepting state.

### 4. Diagram

```
Thompson's Construction for (a|b):

        ε      a      ε
   S -----> ( )----->( ) -----> F
     \                          ^
      \    ε      b      ε    /
       -->( )----->( )-------
```

```
Subset Construction (general idea):

   NFA states {1,2,3} --a--> {2,4}   (a DFA state)
   NFA states {2,4}   --b--> {5}     (another DFA state)
   ... continue until closed under all transitions
```

### 5. Example
For regex `(a|b)*abb` (a very common exam regex):
- Build NFA for `a`, `b` individually.
- Combine using union for `(a|b)`.
- Apply Kleene star for `(a|b)*`.
- Concatenate with NFA for `a`, `b`, `b` in sequence.
- Apply subset construction to merge NFA states into DFA states, tracing ε-closures at each step, until a minimal DFA is obtained that accepts strings ending in `abb`.

### 6. Advantages
- NFA is easy to construct directly and compositionally from a regular expression.
- DFA (after conversion) allows fast, deterministic string matching — ideal for a lexical analyzer.

### 7. Limitations
- Subset construction can cause exponential blow-up in the number of DFA states in the worst case.
- Thompson's Construction NFAs contain many ε-transitions, making direct NFA simulation slower than DFA.

### 8. Applications
- Core mechanism inside lexical analyzer generators like **Lex/Flex**.
- Used broadly in pattern matching (e.g., grep, regex engines).

### 9. Conclusion
Thompson's Construction and Subset Construction together provide a systematic pipeline — Regular Expression → NFA → DFA — that transforms a human-readable pattern into an efficient, deterministic automaton usable for fast token recognition in a lexical analyzer.

---

## Part 3: Diagram
(Use the Thompson's Construction diagram for union above as a template; practice one full NFA→DFA conversion by hand for a given regex.)

---

## Part 4: Examiner Keywords
**Regular Expression**, **NFA**, **DFA**, **Thompson's Construction**, **Subset Construction**, ε-transition, ε-closure, move()

---

## Part 5: PYQ Notes
- **Expected Marks:** 8–10 marks
- **Previous Frequency:** High — 6/10 papers, usually with a specific regex like `(a+b)*abb` or `(a|b*ab)*`
- **Common Mistakes:** Forgetting the bypass ε-transition for Kleene star (zero occurrences); not computing ε-closure correctly during subset construction
- **Related Questions:** "What is the difference between NFA and DFA?", "Minimize the given DFA"

---

## Part 6: Revision Box
- RE → NFA: Thompson's Construction (union, concatenation, Kleene star rules with ε-transitions)
- NFA → DFA: Subset Construction (ε-closure + move() for each state/symbol)
- DFA state = a SET of NFA states
- DFA is deterministic (1 transition per symbol per state); NFA can have multiple/none
- Practiced regex forms: `(a+b)*abb`, `(a|b*ab)*`

---

## Part 7: Expected Viva Questions
1. What is an ε-transition?
2. Why convert NFA to DFA instead of using NFA directly?
3. What is ε-closure?
4. Can a DFA blow up in states compared to its NFA?
5. Which tool uses these constructions internally to build lexical analyzers?

---

## Part 8: Memory Trick
**"RE se NFA banta hai Thompson se, NFA se DFA banta hai Subset se — dono me ε-closure yaad rakho."**

---
---

# Q24

**Question:**
Explain Input Buffering. What is the two-buffer scheme, and how do sentinels improve its efficiency?

**Probability:** ★★★☆☆ (Moderate — 3/10 papers)

**Why Important:**
- Practical, implementation-focused Unit 1 topic that's often overlooked but appears consistently as a short theory question.
- Tests understanding of why lexical analyzers are engineered a certain way (efficiency-focused).
- Easy full marks if the sentinel trick is clearly explained.

---

## Part 1: Hinglish Concept

**Ye hota kya hai?**
Lexical analyzer ko source code character-by-character padhna padta hai, aur bar-bar disk se ek-ek character read karna **bahut slow** hota hai. Isliye compiler use karta hai **buffering** — bade chunks (buffers) me data pehle se load kar leta hai memory me.

**Two-Buffer Scheme:** Do buffers use karte hai (jaise buffer A aur buffer B) — jab ek buffer khatam hota hai, to dusra already fill ho chuka hota hai (background me), isliye reading kabhi rukti nahi.

**Sentinel kya hai?**
Har buffer ke **end me ek special character** (jaise `eof`) rakh dete hai. Ye batata hai "buffer khatam ho gaya, doosre buffer par jao." Isse fayda ye hota hai ki normally har character read karte waqt do checks karne padte — (1) kya ye buffer ka end hai? (2) kya ye match kar raha hai? Sentinel dono checks ko **ek** me combine kar deta hai — bas character check karo, agar sentinel mile to phir end-check karo.

**Real life example:** Socho tum ek kitaab padh rahe ho aur har page ke end me ek "bookmark" laga rakha hai jo bata deta hai "page khatam, agla page palto" — bina har line ke baad manually check kiye "kya ye last line hai?"

**Ye kyu use hota hai?**
Performance improve karne ke liye — bar-bar do alag checks (buffer-end + character-match) karne ke bajaye, sirf ek hi check karna padta hai.

**Exam me isse kya puch sakte hai?**
- Explain two-buffer scheme with diagram
- Explain role of sentinel

---

## Part 2: English Exam Answer

### 1. Definition
**Input Buffering** is a technique used by the lexical analyzer to efficiently read the source program using large buffers instead of reading one character at a time, minimizing costly I/O operations.

### 2. Introduction
Lexical analyzers often need to "look ahead" beyond the current character to decide where a token ends. Reading character-by-character directly from disk is slow, so a buffering scheme using two alternating buffers, combined with sentinel characters, is used for efficiency.

### 3. Working / Steps

**Two-Buffer Scheme:**
1. Two buffers, each of size N (e.g., a disk block size), are used.
2. When the pointer reaches the end of buffer 1, buffer 2 is refilled from the input (or vice versa), and scanning continues seamlessly.
3. Two pointers are maintained: `lexemeBegin` (start of current lexeme) and `forward` (scans ahead to find the end of the lexeme).

**Role of Sentinels:**
1. A special character (usually `eof`, not part of the source language) is placed at the end of each buffer.
2. While scanning, the `forward` pointer only needs to check: "Is this character the sentinel?" If yes, then perform the extra check for actual end-of-buffer vs true end-of-input.
3. This merges the two checks (buffer-end test + character test) into a single test in the common case, significantly speeding up the scanning loop.

### 4. Diagram

```
   Buffer 1                    Buffer 2
+---------------+eof+---------------+eof
| E = M * C**2  |   |               |
+---------------+   +---------------+
        ^                    ^
   lexemeBegin           forward pointer
   (moves forward one buffer at a time, using sentinel to detect switch)
```

### 5. Example
While scanning the identifier `count`, the `forward` pointer advances character by character (`c`,`o`,`u`,`n`,`t`); if the pointer reaches the sentinel `eof` at the end of buffer 1, the lexical analyzer checks whether this is a true end-of-file or just end-of-buffer, and if it's just end-of-buffer, it reloads buffer 2 and continues scanning without missing any characters.

### 6. Advantages
- Reduces the number of expensive I/O read operations by reading in large chunks.
- Sentinel-based checking reduces the number of comparisons per character from two to effectively one in most cases, improving speed.

### 7. Limitations
- Requires careful buffer management to avoid losing characters at buffer boundaries.
- Slightly more complex to implement correctly compared to naive character-by-character reading.

### 8. Applications
- Used in the implementation of real lexical analyzers (including those generated by Lex/Flex).
- General technique also applicable to any high-performance stream-processing system.

### 9. Conclusion
Input buffering using a two-buffer scheme with sentinels allows a lexical analyzer to efficiently scan source code in large chunks while minimizing the number of checks per character, making token recognition fast and I/O-efficient.

---

## Part 3: Diagram
(Use the two-buffer + sentinel diagram above.)

---

## Part 4: Examiner Keywords
**Input Buffering**, **Two-Buffer Scheme**, **Sentinel**, `lexemeBegin`, `forward` pointer, eof character, I/O efficiency

---

## Part 5: PYQ Notes
- **Expected Marks:** 4–6 marks
- **Previous Frequency:** Moderate — 3/10 papers, usually a short theory question
- **Common Mistakes:** Not explaining WHY sentinels help (the "merge two checks into one" reasoning is often missed); confusing sentinel with just "any end marker"
- **Related Questions:** "Explain the role of lexemeBegin and forward pointers"

---

## Part 6: Revision Box
- Two buffers used so reading is never interrupted while one refills
- Sentinel = special character (eof) placed at end of each buffer
- Sentinel merges buffer-end check + character-match check into one test
- Pointers: lexemeBegin (start of token) and forward (scans ahead)

---

## Part 7: Expected Viva Questions
1. Why use two buffers instead of one?
2. What character is typically used as a sentinel?
3. How does a sentinel improve performance?
4. What are the roles of the lexemeBegin and forward pointers?
5. What happens when the forward pointer reaches the sentinel?

---

## Part 8: Memory Trick
**"Sentinel = Bookmark jo batata hai 'page khatam, agla uthao' — bina har line check kiye."**

---
---

# Q25

**Question:**
Explain Intermediate Code Generation for control statements: if-else, while loop, and switch statement, with the translation scheme and generated three-address code.

**Probability:** ★★★★☆ (High — 4/10 papers)

**Why Important:**
- Direct application of SDT (Q22) to real control structures — a natural follow-up question examiners like to ask.
- Tests practical TAC generation using labels and jumps, a skill needed for the code generation phase (Q5).
- Covers three distinct control structures in one unified answer.

---

## Part 1: Hinglish Concept

**Ye hota kya hai?**
Jab tumhare code me `if-else`, `while`, ya `switch` jaise control statements hote hai, compiler unhe **three-address code (TAC)** me convert karta hai jisme **labels aur conditional/unconditional jumps (goto)** use hote hai — kyuki TAC me directly `if-else` jaisa structure nahi hota, sirf comparisons aur jumps hote hai.

**Real life example:** Socho ek instruction manual hai: "Agar switch ON hai, to step 5 par jao, nahi to step 8 par jao." Ye bilkul TAC jaisa hai — condition check karo, phir kisi specific line number (label) par jump karo.

**Teen important cheezein:**
- `if E goto L` — agar E true hai to L par jao
- `goto L` — hamesha L par jao
- `L:` — ek label jo batata hai "yaha se code shuru hota hai"

**Ye kyu use hota hai?**
Kyuki target machine code me bhi conditional/unconditional jumps hi hote hai (no native if-else/while) — TAC isi form me pehle se convert kar deta hai taaki code generation aasan ho.

**Exam me isse kya puch sakte hai?**
- SDT rules for if-else/while
- TAC for a given code snippet using if/while/switch

---

## Part 2: English Exam Answer

### 1. Definition
**Intermediate Code Generation for control statements** converts high-level control constructs (if-else, while, switch) into three-address code using conditional (`if...goto`) and unconditional (`goto`) jump instructions along with labels.

### 2. Introduction
Since target machine code has no native if-else/while/switch instructions — only comparisons and jumps — the compiler must translate these high-level constructs into a sequence of TAC statements using labels (`L1`, `L2`, ...) to mark jump targets.

### 3. Working / Steps

**Translation Scheme for `if (E) S1 else S2`:**
```
      code for E, jumping to Ltrue if true, Lfalse if false
Ltrue:  code for S1
        goto Lnext
Lfalse: code for S2
Lnext:
```

**Translation Scheme for `while (E) S`:**
```
Lbegin: code for E, jumping to Ltrue if true, Lnext if false
Ltrue:  code for S
        goto Lbegin
Lnext:
```

**Translation Scheme for `switch (E) { case v1: S1 ... default: Sn }`:**
```
        code to evaluate E into temp t
        goto Ltest
L1:     code for S1
        goto Lnext
L2:     code for S2
        goto Lnext
...
Ldefault: code for Sn
        goto Lnext
Ltest:  if t = v1 goto L1
        if t = v2 goto L2
        ...
        goto Ldefault
Lnext:
```

### 4. Diagram

```
IF-ELSE                  WHILE                    SWITCH
  |                        |                         |
Test E                  Lbegin: Test E          Evaluate E → t
 / \                      /   \                       |
true false             true   false             Compare t with
 |     |                 |      |                each case value
code   code            code    exit               |         |
S1     S2                |                     matching   default
 \     /                 goto Lbegin              case      case
  \   /                    |                        |         |
  Lnext                  Lnext                     Lnext -----
```

### 5. Example — TAC for `if (a < b) x = 1; else x = 2;`
```
      if a < b goto L1
      goto L2
L1:   x = 1
      goto L3
L2:   x = 2
L3:
```

**Example — TAC for `while (a < b) { a = a + 1; }`**
```
L1: if a < b goto L2
    goto L3
L2: a = a + 1
    goto L1
L3:
```

### 6. Advantages
- Converts all control structures into a uniform representation (jumps + labels), simplifying code generation.
- Machine-independent — this intermediate form works for any target architecture.

### 7. Limitations
- Excessive use of labels/jumps can make the intermediate code harder to read/debug manually.
- Requires careful back-patching techniques when labels are not known in advance (common in single-pass compilers).

### 8. Applications
- Core technique used in every compiler's intermediate code generation phase for control-flow constructs.
- Basis for later constructing the flow graph (see Q21) from generated TAC.

### 9. Conclusion
Intermediate code generation for control statements systematically converts if-else, while, and switch constructs into three-address code using conditional/unconditional jumps and labels, providing a uniform, machine-independent representation that is later used to build flow graphs and generate target code.

---

## Part 3: Diagram
(Use the three side-by-side control-flow diagrams above for if-else, while, and switch.)

---

## Part 4: Examiner Keywords
**Intermediate Code**, **Three-Address Code**, `if...goto`, `goto`, **Label**, Control Statement Translation, Back-patching

---

## Part 5: PYQ Notes
- **Expected Marks:** 8 marks
- **Previous Frequency:** High — 4/10 papers, if-else and while are most commonly asked
- **Common Mistakes:** Forgetting the `goto Lnext` after the true branch in if-else (causing fall-through into the else branch); mislabeling jump targets
- **Related Questions:** "What is back-patching?", see Q21 for constructing a flow graph from this TAC.

---

## Part 6: Revision Box
- if-else: test E → true/false branches → both converge at Lnext
- while: test at top (Lbegin), body loops back to Lbegin, exits to Lnext
- switch: evaluate E once, then compare against each case value, jump accordingly
- Always remember `goto Lnext` after each branch to avoid fall-through bugs
- Labels (L1, L2, ...) mark jump targets

---

## Part 7: Expected Viva Questions
1. Why does target code need labels and jumps instead of if-else directly?
2. What is back-patching, and when is it needed?
3. Where is the condition tested in a while loop's TAC — top or bottom?
4. What happens if you forget the `goto Lnext` after the true branch in if-else TAC?
5. How is a switch statement's default case handled in TAC?

---

## Part 8: Memory Trick
**"Test → True/False → Jump → Label — for if, aur Loop back to Label — for while."**

---
---

# Q26

**Question:**
Explain the Design Issues of a Code Generator.

**Probability:** ★★★★☆ (High — 6/10 papers; tightens the partial coverage from Q5)

**Why Important:**
- A distinct standalone theory question, separate from the register-focused numeric of Q5 — tests the full breadth of code generator responsibilities.
- Frequently asked as a pure "list and explain" question, easy to score fully if the 6 issues are memorized precisely.

---

## Part 1: Hinglish Concept

**Ye hota kya hai?**
Code generator banate waqt compiler designer ko **6 major design decisions** leni padti hai — jaise input format kya hoga, target code kis form me hoga, memory kaise manage hogi, etc.

**6 issues yaad rakho:**
1. **Input** — code generator ko kya diya jaa raha hai (TAC, DAG + symbol table)
2. **Target Program** — output kis form me chahiye (absolute machine code, relocatable code, ya assembly)
3. **Memory Management** — variables ko memory addresses assign karna
4. **Instruction Selection** — kaunsi instructions use karni hai (efficient vs inefficient choices)
5. **Register Allocation** — kaunsi values registers me rakhni hai (limited registers hote hai)
6. **Evaluation Order** — expressions kis order me calculate karni hai (order se efficiency change ho sakti hai)

**Ye kyu important hai?**
Har decision final code ki **speed aur size** par directly asar dalti hai.

**Exam me isse kya puch sakte hai?**
- List + explain all 6 issues
- Small numeric: generate code for a given assignment statement

---

## Part 2: English Exam Answer

### 1. Definition
**Design Issues of a Code Generator** refer to the key decisions a compiler designer must make while building the code generation phase, which directly affect the efficiency and correctness of the generated target code.

### 2. Introduction
The code generator is the final phase of the compiler, translating optimized intermediate representation into target code. Its design involves multiple interdependent choices, since good decisions in one area (e.g., instruction selection) can be undermined by poor decisions in another (e.g., register allocation).

### 3. Working / Steps — The Six Design Issues

1. **Input to the Code Generator:** The intermediate representation (three-address code, DAG, etc.) along with the symbol table (for memory addresses and types).

2. **Target Program:** The form of the output — absolute machine code (directly executable), relocatable machine code (needs linking), or assembly language (needs an assembler).

3. **Memory Management:** Mapping variable/temporary names in the intermediate code to actual memory locations/offsets, using information from the symbol table.

4. **Instruction Selection:** Choosing the most efficient machine instructions to implement each intermediate code statement — affects code quality, speed, and uniformity.

5. **Register Allocation and Assignment:** Deciding which values should be kept in the limited, fast CPU registers at any given time (see Q5 for the four principal uses of registers).

6. **Choice of Evaluation Order:** Deciding the order in which computations are performed — since different orders can affect the number of registers needed and overall efficiency.

### 4. Diagram

```
        +----------------------------+
        |   Intermediate Code + ST   |  <-- (1) Input
        +----------------------------+
                    |
        +----------------------------+
        |  Decide Target Form         |  <-- (2) Target Program
        +----------------------------+
                    |
        +----------------------------+
        |  Assign Memory Addresses    |  <-- (3) Memory Management
        +----------------------------+
                    |
        +----------------------------+
        |  Choose Instructions        |  <-- (4) Instruction Selection
        +----------------------------+
                    |
        +----------------------------+
        |  Allocate Registers         |  <-- (5) Register Allocation
        +----------------------------+
                    |
        +----------------------------+
        |  Decide Evaluation Order    |  <-- (6) Evaluation Order
        +----------------------------+
```

### 5. Example — Numeric Variant
For:
```
x = b * c
y = a + x
```
Assuming all variables are in memory, simple generated code:
```
MOV b, R0
MUL c, R0
MOV R0, x
MOV a, R1
ADD x, R1
MOV R1, y
```
**Cost:** measured as the count of instructions/memory references — "cost of an instruction = 1 + cost of source/destination addressing modes" if the question asks about addressing-mode cost.

### 6. Advantages
- Systematic breakdown of the code generation problem into manageable design decisions.
- Helps balance trade-offs between code speed, size, and compiler complexity.

### 7. Limitations
- Optimal solutions for instruction selection and register allocation are both NP-hard in general — practical compilers use heuristics.
- Design choices are highly machine-dependent; a good design for one architecture may be poor for another.

### 8. Applications
- These design issues are directly addressed in the back-end of every real compiler (GCC, LLVM).
- Also relevant when designing code generators for virtual machines/bytecode interpreters (like the JVM).

### 9. Conclusion
The design of a code generator involves six interrelated decisions — input format, target program form, memory management, instruction selection, register allocation, and evaluation order — each of which impacts the efficiency and quality of the final generated code.

---

## Part 3: Diagram
(Use the six-step vertical flow diagram above.)

---

## Part 4: Examiner Keywords
**Code Generator Design Issues**, Target Program, **Instruction Selection**, **Register Allocation**, Memory Management, Evaluation Order, Addressing Mode Cost

---

## Part 5: PYQ Notes
- **Expected Marks:** 6–8 marks
- **Previous Frequency:** High — 6/10 papers, often paired with a small code-gen numeric
- **Common Mistakes:** Only listing 4-5 issues (forgetting "evaluation order" or "target program form"); not explaining WHY each issue matters
- **Related Questions:** See Q5 for the register descriptor/address descriptor based code generation algorithm.

---

## Part 6: Revision Box
- 6 issues: Input, Target Program, Memory Management, Instruction Selection, Register Allocation, Evaluation Order
- Input = IR + symbol table
- Target program can be absolute, relocatable, or assembly code
- Instruction selection and register allocation are both NP-hard in general (heuristics used)
- Cost = instruction count / addressing mode cost

---

## Part 7: Expected Viva Questions
1. Name the six design issues of a code generator.
2. What are the three possible forms of target program output?
3. Why is instruction selection considered a hard problem?
4. How does evaluation order affect register usage?
5. What information does the code generator take from the symbol table?

---

## Part 8: Memory Trick
**"I-T-M-I-R-E"** — Input, Target program, Memory management, Instruction selection, Register allocation, Evaluation order.

---
---

# Q27

**Question:**
Differentiate between Top-Down and Bottom-Up Parsing. Explain the Shift-Reduce Parsing technique with its four actions.

**Probability:** ★★★★☆ (High — 5/10 papers; tightens partial coverage)

**Why Important:**
- A dedicated comparison question distinct from the specific parser numericals (LL(1) in Q3/Q15, LR in Q9/Q18) — tests conceptual big-picture understanding.
- Shift-reduce actions are a foundational concept underlying all bottom-up parsers (Q9, Q17, Q18).

---

## Part 1: Hinglish Concept

**Ye hota kya hai?**
Parsing ke do main approaches hote hai:
- **Top-Down:** Start symbol se shuru karke neeche (leaves/tokens) tak jaate hai — root se leaves tak tree banate hai
- **Bottom-Up:** Tokens (leaves) se shuru karke upar (start symbol) tak jaate hai — leaves se root tak tree banate hai

**Real life example:** Socho tumhe ek building banani hai. Top-down matlab pehle overall design (blueprint) socho, phir details fill karo. Bottom-up matlab pehle chhoti-chhoti bricks jodo, dheere-dheere poori building bana lo.

**Shift-Reduce Parsing (bottom-up ka core mechanism):**
4 actions hote hai:
1. **Shift** — agla input symbol stack par push karo
2. **Reduce** — stack ke top ka pattern kisi production ke RHS se match kare, to use LHS se replace karo
3. **Accept** — jab poora input successfully start symbol tak reduce ho jaye
4. **Error** — jab na shift ho sakta hai na reduce

**Exam me isse kya puch sakte hai?**
- Comparison table (top-down vs bottom-up)
- Explain 4 shift-reduce actions with example trace

---

## Part 2: English Exam Answer

### 1. Definition
**Top-Down Parsing** builds the parse tree starting from the root (start symbol) down to the leaves (input tokens), using leftmost derivation.
**Bottom-Up Parsing** builds the parse tree starting from the leaves (input tokens) up to the root (start symbol), using rightmost derivation in reverse.

### 2. Introduction
These represent the two fundamental strategies for syntax analysis. Top-down parsers (like LL(1), recursive descent) predict which production to use in advance, while bottom-up parsers (like shift-reduce, LR) build up structure incrementally and only decide the production once the full right-hand side is recognized on the stack.

### 3. Working / Steps

**Comparison Table:**

| Aspect | Top-Down | Bottom-Up |
|---|---|---|
| Derivation | Leftmost derivation | Rightmost derivation in reverse |
| Tree building direction | Root → leaves | Leaves → root |
| Example parsers | Recursive descent, LL(1) | Shift-reduce, LR(0), SLR, LALR, CLR |
| Left recursion | Not allowed (causes infinite loop) | Allowed |
| Parsing power | Less powerful | More powerful (handles a larger class of grammars) |

**Shift-Reduce Parsing — 4 Actions:**
1. **Shift:** Push the next input symbol onto the stack.
2. **Reduce:** If the top of the stack matches the RHS of a production (a "handle"), pop it and push the corresponding LHS non-terminal.
3. **Accept:** When the stack contains only the start symbol and the input is fully consumed — parsing is successful.
4. **Error:** When neither shift nor reduce can be applied — syntax error detected.

### 4. Diagram

```
TOP-DOWN                         BOTTOM-UP
 (Root to Leaves)                 (Leaves to Root)

      S                                S
     /|\                              /|\
    A B C          vs               A B C
   /     \                         /     \
  a       c                       a       c
(predict, then match)      (recognize handle, then reduce)
```

### 5. Example — Shift-Reduce Trace for `id + id` with grammar `E → E+T | T`, `T → id`
| Stack | Input | Action |
|---|---|---|
| $ | id+id$ | Shift |
| $id | +id$ | Reduce (T→id) |
| $T | +id$ | Reduce (E→T) |
| $E | +id$ | Shift |
| $E+ | id$ | Shift |
| $E+id | $ | Reduce (T→id) |
| $E+T | $ | Reduce (E→E+T) |
| $E | $ | Accept |

### 6. Advantages
- Bottom-up parsers handle a larger class of grammars (including left-recursive ones) than top-down parsers.
- Top-down parsers (especially recursive descent) are simpler to hand-write and understand.

### 7. Limitations
- Top-down parsers cannot handle left recursion directly (must be eliminated first — see Q2).
- Bottom-up parsers require more complex table construction (see Q9, Q18).

### 8. Applications
- Top-down: used for simple grammars, hand-written parsers, and educational compilers.
- Bottom-up: used in real-world parser generators like YACC/Bison (LALR-based).

### 9. Conclusion
Top-down and bottom-up parsing represent two fundamentally different strategies for constructing a parse tree, with bottom-up (shift-reduce) parsing offering greater power at the cost of more complex table-driven implementation, forming the basis of the LR parser family covered in Q9 and Q18.

---

## Part 3: Diagram
(Use the root-to-leaves vs leaves-to-root diagram above, alongside the shift-reduce trace table.)

---

## Part 4: Examiner Keywords
**Top-Down Parsing**, **Bottom-Up Parsing**, **Shift**, **Reduce**, **Accept**, **Error**, Handle, Leftmost Derivation, Rightmost Derivation

---

## Part 5: PYQ Notes
- **Expected Marks:** 6–8 marks
- **Previous Frequency:** High — 5/10 papers, often as a standalone comparison question
- **Common Mistakes:** Confusing "leftmost derivation" with "left-to-right scanning" (both parsers scan left to right, but derivation direction differs); not naming all 4 shift-reduce actions
- **Related Questions:** See Q9/Q18 for full LR parsing tables that formalize the reduce decision.

---

## Part 6: Revision Box
- Top-down: root→leaves, leftmost derivation, no left recursion allowed
- Bottom-up: leaves→root, rightmost derivation in reverse, left recursion allowed
- Shift-reduce actions: Shift, Reduce, Accept, Error
- A "handle" is the substring reduced at each step
- Bottom-up parsers are more powerful overall

---

## Part 7: Expected Viva Questions
1. What is a "handle" in shift-reduce parsing?
2. Why can't top-down parsers handle left-recursive grammars?
3. Name two example parsers for each category (top-down and bottom-up).
4. What triggers the "Error" action in shift-reduce parsing?
5. Which type of parsing is more powerful, and why?

---

## Part 8: Memory Trick
**"Top-Down = Top se Design karo (predict), Bottom-Up = Bricks se Upar banao (recognize then reduce)."**

---
---

# Q28

**Question:**
Explain the different intermediate representations of Three-Address Code: Quadruples, Triples, and Indirect Triples, with examples.

**Probability:** ★★★☆☆ (Moderate — 3/10 papers; tightens partial coverage)

**Why Important:**
- Fills a specific gap — the three concrete *implementation formats* of TAC, distinct from the TAC concept itself (already covered via Q1, Q22, Q25).
- Comparison-style question, easy to score with a clear table and example.

---

## Part 1: Hinglish Concept

**Ye hota kya hai?**
Three-Address Code (TAC) ko actually **store karne ke 3 tarike** hote hai compiler ke andar:
1. **Quadruples** — 4 fields: (operator, arg1, arg2, result) — sabse simple, har statement apna result naam store karta hai
2. **Triples** — 3 fields: (operator, arg1, arg2) — result ko naam nahi dete, balki us statement ke **position number** se refer karte hai
3. **Indirect Triples** — triples ki list banate hai, lekin ek **alag pointer list** rakhte hai jo batati hai kis order me execute karna hai — isse triples ko reorder karna aasan ho jaata hai bina unhe move kiye

**Real life example:** Socho tum ek TODO list bana rahe ho:
- Quadruples = har task ka apna naam hai (Task_A, Task_B) — directly refer kar sakte ho
- Triples = tasks numbered hai (Task #1, #2) — refer karne ke liye number use karte ho
- Indirect Triples = tasks numbered hai, lekin ek **alag order list** hai jo batati hai kaunsa task pehle karna hai — agar order badalna ho, to sirf order list badlo, tasks ko nahi

**Ye kyu use hota hai?**
Memory efficiency aur reordering flexibility ke trade-off ke liye — har form ke apne fayde hai.

**Exam me isse kya puch sakte hai?**
- Explain all 3 with example expression converted to each form

---

## Part 2: English Exam Answer

### 1. Definition
Three-address code can be implemented using three data structures: **Quadruples** (4-field records: operator, arg1, arg2, result), **Triples** (3-field records without an explicit result field, referenced by position), and **Indirect Triples** (triples accessed through a separate list of pointers, allowing reordering).

### 2. Introduction
While three-address code conceptually looks like `x = y op z`, compilers must choose a concrete internal representation to store these statements — each representation offers different trade-offs in memory usage and ease of code optimization/reordering.

### 3. Working / Steps

**Quadruples:** Each statement has 4 fields — `(op, arg1, arg2, result)`. The result is an explicitly named temporary or variable.

**Triples:** Each statement has 3 fields — `(op, arg1, arg2)` — with no explicit result field. Instead, the result is referred to by the position (index) of the triple itself.

**Indirect Triples:** Like triples, but an additional list of pointers indicates the order in which triples should be executed — this separates "what the statement computes" from "in what order it is executed," allowing reordering (useful in optimization) without physically moving the triples.

### 4. Diagram — For expression `a = b * -c + b * -c`

**Quadruples:**
| # | op | arg1 | arg2 | result |
|---|---|---|---|---|
| 1 | uminus | c | — | t1 |
| 2 | * | b | t1 | t2 |
| 3 | uminus | c | — | t3 |
| 4 | * | b | t3 | t4 |
| 5 | + | t2 | t4 | t5 |
| 6 | = | t5 | — | a |

**Triples:**
| # | op | arg1 | arg2 |
|---|---|---|---|
| (1) | uminus | c | — |
| (2) | * | b | (1) |
| (3) | uminus | c | — |
| (4) | * | b | (3) |
| (5) | + | (2) | (4) |
| (6) | = | a | (5) |

**Indirect Triples:**
```
Statement List:            Triple List (same as above, unordered):
(1) → points to triple 14      (14) uminus c
(2) → points to triple 15      (15) * b (14)
(3) → points to triple 16      (16) uminus c
...                             ...
```

### 5. Example
As shown above — same expression `a = b*(-c) + b*(-c)` represented in all three forms, showing how triples save the explicit `result` field by using position references instead.

### 6. Advantages
- **Quadruples:** Easy to rearrange (moving a quadruple doesn't affect others, since references are by name, not position) — good for optimization.
- **Triples:** More memory-efficient (no extra result field needed).
- **Indirect Triples:** Combines memory efficiency of triples with the reordering flexibility of quadruples, via the separate pointer list.

### 7. Limitations
- **Quadruples:** Use more memory due to the explicit result field for every statement.
- **Triples:** Reordering is difficult, since moving a triple changes its position number, breaking references from other triples.
- **Indirect Triples:** Slightly more complex to implement due to the extra indirection layer.

### 8. Applications
- Used internally by compilers to store and manipulate intermediate code during optimization passes.
- Choice of representation affects the ease of implementing optimizations like code motion and common sub-expression elimination.

### 9. Conclusion
Quadruples, triples, and indirect triples are three alternative internal representations of three-address code, each balancing memory efficiency against ease of reordering — with indirect triples offering the best combination of both for practical compiler optimization.

---

## Part 3: Diagram
(Use the three side-by-side tables above for the same expression.)

---

## Part 4: Examiner Keywords
**Quadruples**, **Triples**, **Indirect Triples**, Three-Address Code, Position Reference, Pointer List, Reordering

---

## Part 5: PYQ Notes
- **Expected Marks:** 6 marks
- **Previous Frequency:** Moderate — 3/10 papers
- **Common Mistakes:** Forgetting that triples reference results BY POSITION, not by name; not explaining why indirect triples help with reordering
- **Related Questions:** See Q1/Q22 for the general TAC concept these representations are built on.

---

## Part 6: Revision Box
- Quadruples: (op, arg1, arg2, result) — 4 fields, named result
- Triples: (op, arg1, arg2) — 3 fields, referenced by position number
- Indirect Triples: triples + separate pointer/order list — enables reordering
- Quadruples = easiest to reorder; Triples = most memory-efficient; Indirect Triples = best of both

---

## Part 7: Expected Viva Questions
1. What is the main difference between quadruples and triples?
2. Why is reordering difficult with plain triples?
3. How do indirect triples solve the reordering problem?
4. Which representation uses the least memory?
5. Which representation is easiest to use during code optimization?

---

## Part 8: Memory Trick
**"Quad = 4 fields (named), Triple = 3 fields (numbered), Indirect Triple = Triple + Order List."**

---
---

# Q29

**Question:**
How do you check whether a given grammar is LL(1)? Explain with an example.

**Probability:** ★★★☆☆ (Moderate — 3/10 papers; tightens partial coverage)

**Why Important:**
- A distinct question framing from Q3/Q15/Q16 — focuses specifically on the **verification/check** process rather than just building the table.
- Tests deeper understanding of what causes LL(1) conflicts (not just how to compute FIRST/FOLLOW).

---

## Part 1: Hinglish Concept

**Ye hota kya hai?**
Ek grammar **LL(1)** hoti hai agar uska parsing table banate waqt **kisi bhi cell me do ya zyada entries na aaye**. Agar koi cell me conflict ho (2 productions same cell me), to grammar LL(1) NAHI hai.

**Check karne ke conditions (2 alternative productions A → α | β ke liye):**
1. FIRST(α) aur FIRST(β) common nahi hone chahiye (intersection empty honi chahiye)
2. Agar β, ε derive kar sakta hai, to FIRST(α) aur FOLLOW(A) bhi common nahi hone chahiye

**Real life example:** Socho ek traffic signal system hai jisme ek hi condition (green light) do alag actions trigger kar de — ye confusing hai, driver confuse ho jayega. LL(1) grammar me bhi aisa conflict allowed nahi — ek input symbol par sirf EK hi decision honi chahiye.

**Ye kyu important hai?**
Agar grammar LL(1) nahi hai, to usse predictive/LL(1) parser se parse nahi kar sakte — pehle usse left-factor ya left-recursion-free banana padega, ya phir LR parser use karna padega.

**Exam me isse kya puch sakte hai?**
- Given grammar, check if LL(1) using FIRST/FOLLOW conditions
- Identify WHERE the conflict occurs if not LL(1)

---

## Part 2: English Exam Answer

### 1. Definition
A grammar is said to be **LL(1)** if, for every non-terminal with two or more alternative productions, the parser can always decide unambiguously which production to use by looking at only one input symbol (lookahead) — i.e., the LL(1) parsing table has no cell with more than one entry.

### 2. Introduction
Checking LL(1)-ness is important because only LL(1) grammars can be parsed by a simple, backtrack-free predictive parser (Q15). If a grammar fails the LL(1) conditions, it must be transformed (left recursion elimination, left factoring) or a more powerful parser (LR-family) must be used instead.

### 3. Working / Steps

**Conditions for a grammar to be LL(1):** For every non-terminal A with productions `A → α | β`:

1. **FIRST(α) ∩ FIRST(β) = ∅** (FIRST sets of the alternatives must not overlap).
2. If β can derive ε, then **FIRST(α) ∩ FOLLOW(A) = ∅** (and vice versa if α can derive ε).

If both conditions hold for every non-terminal in the grammar, the grammar is LL(1).

**Steps to check:**
1. Compute FIRST and FOLLOW sets for all non-terminals.
2. For each non-terminal with multiple productions, check the two conditions above.
3. If any violation is found → grammar is NOT LL(1) (conflict exists in that cell of the table).

### 4. Diagram

```
   A → α | β

   Condition 1: FIRST(α) ∩ FIRST(β) = ∅  ?
   Condition 2 (if β ⇒* ε): FIRST(α) ∩ FOLLOW(A) = ∅ ?

        Both hold  --------> Grammar is LL(1)
        Any fails  --------> Grammar is NOT LL(1) (conflict)
```

### 5. Example

**Check if the following grammar is LL(1):**
```
S → iEtS | iEtSeS | a
E → b
```
FIRST of both `iEtS` and `iEtSeS` = `{i}` → **overlap!** Since both alternatives of S start with the same terminal `i`, condition 1 fails.

**Conclusion:** This grammar is **NOT LL(1)** as written — it must first be **left-factored** (see Q10) into:
```
S  → iEtSS' | a
S' → eS | ε
```
After left factoring, `S → iEtSS'` and `S → a` have FIRST sets `{i}` and `{a}` respectively — no overlap — so the factored grammar IS LL(1).

### 6. Advantages
- Provides a clear, checkable criterion before attempting to build a predictive parser.
- Helps identify exactly which non-terminal/productions cause the conflict, guiding grammar transformation.

### 7. Limitations
- Even after transformation (left factoring/left recursion removal), some grammars can never be made LL(1) (they are inherently ambiguous or require more lookahead).
- Checking by hand for large grammars is tedious and error-prone.

### 8. Applications
- Used as a pre-check before implementing any table-driven predictive parser.
- Helps decide whether to use an LL parser or switch to an LR-family parser (Q9/Q18) for a given grammar.

### 9. Conclusion
A grammar is LL(1) if and only if the FIRST sets of alternative productions don't overlap, and FIRST/FOLLOW don't overlap when an alternative can derive ε — checking these conditions systematically reveals whether predictive parsing is possible, or whether transformations like left factoring are needed first.

---

## Part 3: Diagram
(Use the condition-check flowchart above.)

---

## Part 4: Examiner Keywords
**LL(1) Grammar**, FIRST, FOLLOW, Conflict, **Predictive Parser**, Left Factoring, Overlap Condition

---

## Part 5: PYQ Notes
- **Expected Marks:** 6–8 marks
- **Previous Frequency:** Moderate — 3/10 papers, often uses the exact `S → iEtS | iEtSeS | a` grammar
- **Common Mistakes:** Only checking condition 1 and forgetting condition 2 (FOLLOW overlap check when ε is derivable); not concluding what transformation fixes the conflict
- **Related Questions:** See Q10 (Left Factoring) for the fix to this exact example.

---

## Part 6: Revision Box
- LL(1) check: FIRST sets of alternatives must not overlap
- If an alternative can derive ε: also check FIRST(other) vs FOLLOW(A) don't overlap
- `S → iEtS | iEtSeS | a` is NOT LL(1) (both start with `i`)
- Fix: left factor the grammar (see Q10), then re-check

---

## Part 7: Expected Viva Questions
1. What are the two conditions for a grammar to be LL(1)?
2. Why does the `S → iEtS | iEtSeS | a` grammar fail the LL(1) check?
3. What fixes a common-prefix LL(1) conflict?
4. Can every grammar be transformed into an LL(1) grammar?
5. What indicates an LL(1) conflict in the parsing table itself?

---

## Part 8: Memory Trick
**"FIRST vs FIRST clash karo mat, aur agar ε ho to FIRST vs FOLLOW bhi clash na kare."**

---
---

# Q30

**Question:**
Explain Register Descriptor and Address Descriptor used in Code Generation, with a suitable example.

**Probability:** ★★★☆☆ (Moderate — 2/10 papers; tightens partial coverage)

**Why Important:**
- Standalone deep-dive on a concept only briefly mentioned in Q5 — often asked as its own distinct short question.
- Tests precise understanding of the bookkeeping used during register allocation.

---

## Part 1: Hinglish Concept

**Ye hota kya hai?**
Code generation ke waqt compiler ko track rakhna padta hai (1) **har register me abhi kya value hai**, aur (2) **har variable ki current value kaha hai** (register me, memory me, ya dono jagah). Ye dono track karne ke liye 2 descriptors use karte hai:

- **Register Descriptor:** Batata hai har register **abhi kya value hold kar raha hai**.
- **Address Descriptor:** Batata hai har variable ki current value **kaha stored hai** — register, memory, ya dono.

**Real life example:** Socho tumhare paas kuch **lockers (registers)** hai aur kuch **items (variables)**. Register Descriptor ek list hai jo batati hai "Locker 1 me kya rakha hai." Address Descriptor ek dusri list hai jo batati hai "ye item kaha rakha hai — locker 1 me, ghar ke store room (memory) me, ya dono jagah."

**Ye kyu use hote hai?**
Jab code generator ko decide karna hota hai "is variable ki value kaha se lu" ya "is register ko reuse kar sakta hu ya nahi", to ye dono descriptors check karta hai.

**Exam me isse kya puch sakte hai?**
- Define both descriptors
- Trace kaise ye update hote hai ek chhoti TAC sequence process karte waqt

---

## Part 2: English Exam Answer

### 1. Definition
A **Register Descriptor** keeps track of what value(s) each available register currently holds. An **Address Descriptor** keeps track of where the current value of each variable is stored — in a register, in memory, or in both.

### 2. Introduction
During code generation (see Q5), the compiler must efficiently decide when to reuse a register versus load/store from memory. Register and address descriptors provide exactly this bookkeeping information, enabling the code generator to avoid unnecessary loads/stores.

### 3. Working / Steps

**Register Descriptor:** Initially, all registers are empty. As code is generated, each register's descriptor is updated to record which variable(s)/temporary(ies) it currently holds.

**Address Descriptor:** Initially, each variable's descriptor states its value is in memory. As computations happen, this descriptor is updated to reflect if the value now also (or only) resides in a register.

**Usage during code generation for `x = y + z`:**
1. Check Address Descriptor of `y` — is it already in a register? If not, generate a load.
2. Check Address Descriptor of `z` — same check.
3. Generate the add instruction into a chosen register (using getReg, informed by the Register Descriptor to find a free/reusable register).
4. Update the Register Descriptor (this register now holds `x`).
5. Update the Address Descriptor of `x` (its value is now in this register; may also update memory later).

### 4. Diagram

```
 Register Descriptor:                Address Descriptor:
 +---------+------------+           +----------+------------------+
 | Register| Holds      |           | Variable | Location(s)      |
 +---------+------------+           +----------+------------------+
 | R1      | y          |           | y        | R1, memory       |
 | R2      | (empty)    |           | x        | R2 (after add)   |
 +---------+------------+           +----------+------------------+
```

### 5. Example
For `x = y + z` (assume y is already in R1, z is in memory):
```
MOV z, R2        ; load z into R2
ADD R1, R2       ; R2 = y + z (i.e., x)
```
Update Register Descriptor: R2 now holds `x`.
Update Address Descriptor: `x` is now in R2 (not yet stored back to memory unless needed).

### 6. Advantages
- Prevents unnecessary redundant loads from memory (if a value is already in a register).
- Enables the code generator to make locally optimal register-reuse decisions.

### 7. Limitations
- Descriptors must be carefully updated after every instruction — a bookkeeping error can cause incorrect code generation.
- Becomes more complex to manage across basic block boundaries.

### 8. Advantages Recap / Applications
- Core mechanism used inside real compiler back-ends (like the "getReg" algorithm) for efficient register allocation.
- Directly supports the code generation algorithm covered in Q5.

### 9. Conclusion
Register and address descriptors are complementary bookkeeping tools used during code generation — the register descriptor tracks what each register holds, while the address descriptor tracks where each variable's value currently resides — together enabling efficient, redundant-load-free target code generation.

---

## Part 3: Diagram
(Use the two-table descriptor diagram above.)

---

## Part 4: Examiner Keywords
**Register Descriptor**, **Address Descriptor**, getReg, Code Generation, Register Reuse, Redundant Load Elimination

---

## Part 5: PYQ Notes
- **Expected Marks:** 4–6 marks
- **Previous Frequency:** Moderate — 2/10 papers, but frequently a viva/short-answer add-on to Q5
- **Common Mistakes:** Mixing up which descriptor tracks registers vs variables; forgetting a variable's address descriptor can list MULTIPLE locations (register AND memory) at once
- **Related Questions:** See Q5 for the full code generation algorithm using these descriptors.

---

## Part 6: Revision Box
- Register Descriptor: tracks what's IN each register
- Address Descriptor: tracks WHERE each variable's value is (register/memory/both)
- Both updated after every generated instruction
- Used to avoid redundant loads and make register reuse decisions
- Core part of the "getReg" function used in code generation (Q5)

---

## Part 7: Expected Viva Questions
1. What is the difference between register descriptor and address descriptor?
2. Can a variable's address descriptor list more than one location at once?
3. Why do these descriptors need to be updated after every instruction?
4. How do these descriptors help avoid redundant memory loads?
5. Which function uses these descriptors to pick a register in code generation?

---

## Part 8: Memory Trick
**"Register Descriptor = 'Locker me kya hai?', Address Descriptor = 'Item kaha hai?'"**

---
---

# FINAL MASTER SUMMARY — All 30 Questions, Gap-Coverage Complete

| # | Topic | Probability | PDF Freq | Unit |
|---|---|---|---|---|
| 21 | Basic Block & Flow Graph | ★★★★★ | 6/10 (Rank 1) | Unit 4/5 |
| 22 | SDD/SDT + Annotated Parse Tree | ★★★★★ | 8/10 (Rank 3, highest overall) | Unit 4 |
| 1 | Compiler Phases + Tools | ★★★★★ | 7/10 (Rank 2) | Unit 1 |
| 26 | Code Generation — Design Issues | ★★★★☆ | 6/10 (Rank 4) | Unit 5/6 |
| 8, 19 | DAG Representation of Basic Blocks | ★★★★☆ | 5/10 (Rank 5) | Unit 4 |
| 6 | Tokens, Lexeme, Pattern | ★★★★★ | 6/10 (Rank 6) | Unit 1 |
| 27 | Top-Down vs Bottom-Up + Shift-Reduce | ★★★★☆ | 5/10 (Rank 7) | Unit 2/3 |
| 3, 15, 16 | FIRST/FOLLOW + Predictive Parsing Table | ★★★★★ | 4/10 (Rank 8) | Unit 2 |
| 2, 10 | Left Recursion + Left Factoring | ★★★★★ | 3/10 (Rank 9, near-guaranteed) | Unit 2 |
| 27 | Shift-Reduce Parsing | ★★★★☆ | 4/10 (Rank 10) | Unit 3 |
| 23 | Regex → NFA → DFA (Thompson's/Subset) | ★★★★☆ | 6/10 (Rank 11) | Unit 1 |
| 8, 12, 20 | Code Optimization (types, techniques) | ★★★★★ | 5/10 (Rank 12) | Unit 4 |
| 7, 13 | Symbol Table | ★★★★☆ | 3/10 (Rank 13) | Unit 1/4 |
| 28 | Three-Address Code / Quadruples-Triples | ★★★☆☆ | 3/10 (Rank 14) | Unit 4 |
| 9, 18 | SLR/LALR/CLR Parsing Table | ★★★★★ | 3/10 (Rank 15) | Unit 3 |
| 24 | Input Buffering (Buffer Pairs & Sentinels) | ★★★☆☆ | 3/10 (Rank 16) | Unit 1 |
| 25 | Intermediate Code Gen (if-else/while/switch) | ★★★★☆ | 4/10 (Rank 17) | Unit 4 |
| 29 | LL(1) Grammar Check | ★★★☆☆ | 3/10 (Rank 18) | Unit 2 |
| 17 | Operator Precedence Parsing | ★★★★☆ | 2/10 (Rank 19) | Unit 3 |
| 5, 30 | Register Allocation / Descriptors | ★★★★☆ | 2/10 (Rank 20) | Unit 5/6 |
| 4 | Type Checking & Conversion | ★★★★☆ | (not in PDF list, still DBATU-common) | Unit 4 |
| 11 | Ambiguous Grammar | ★★★☆☆ | (not in PDF list, still DBATU-common) | Unit 2 |

**Coverage is now effectively 100% of the PDF's frequency-ranked list (all 20 ranked topics addressed), plus 2 extra DBATU-common topics (Type Checking, Ambiguous Grammar) not in the PDF's list but still worth knowing.**

---
---

# HIGH-PRIORITY GAP QUESTIONS (Q31–Q33)

*Added after cross-checking against 10 actual DBATU question papers — these 3 topics appeared across multiple real papers but were missing from the previous 30 questions.*

---
---

# Q31

**Question:**
Explain Runtime Environments. Discuss Stack Allocation and Heap Allocation strategies used to manage memory during program execution.

**Probability:** ★★★★☆ (High)

**Why Important:**
- Appeared across multiple papers under "runtime environments" / "storage allocation strategies" framing.
- Bridges compile-time compiler theory with actual program execution — a distinct Unit 4/5 topic not covered by any of Q1–Q30.
- Tests understanding of how variables are actually stored during execution, complementing the Symbol Table topic (Q7, Q13).

---

## Part 1: Hinglish Concept

**Ye hota kya hai?**
**Runtime Environment** wo setup hai jisme ek program **actually run karte waqt** apna data (variables, function calls) store karta hai. Compiler ko decide karna padta hai ki memory kaise organize hogi jab program chal raha ho.

**3 Main Storage Allocation Strategies:**
1. **Static Allocation:** Memory address **compile time par hi fix** ho jaata hai — jaise global variables. Kabhi change nahi hota.
2. **Stack Allocation:** Har function call ke liye ek **activation record** stack par push hota hai; function khatam hote hi pop ho jaata hai. Local variables yaha store hote hai.
3. **Heap Allocation:** Jab memory ki zaroorat **dynamically** (runtime par) pade, jaise `malloc()` ya `new` — is memory ka size/lifetime pehle se fix nahi hota, programmer manually manage karta hai (ya garbage collector).

**Real life example:** Socho ek restaurant hai:
- **Static** = permanent fixtures (tables jo kabhi move nahi hote) — fixed jagah
- **Stack** = ek waiting queue jisme jo pehle aaya wo pehle jaayega (LIFO) — jaise function calls, jo function last me call hua wo pehle khatam hoga
- **Heap** = ek open storage room jaha kabhi bhi, kisi bhi size ka samaan rakh sakte ho, jab zaroorat ho

**Ye kyu use hota hai?**
Alag-alag data ki lifetime alag hoti hai — kuch hamesha rehta hai (static), kuch function ke sath khatam ho jaata hai (stack), kuch programmer manually control karta hai (heap).

**Exam me isse kya puch sakte hai?**
- Explain each strategy + when it's used
- Compare stack vs heap
- Explain activation record structure

---

## Part 2: English Exam Answer

### 1. Definition
A **Runtime Environment** refers to the memory organization and management scheme used by a compiler to support program execution, including how procedures/functions are allocated storage, how they are called, and how memory is reclaimed.

### 2. Introduction
Different program elements have different lifetimes — some data exists for the entire program run (globals), some exists only during a function call (locals), and some must be dynamically created and destroyed by the programmer (dynamic data). The compiler supports these needs through three storage allocation strategies: static, stack, and heap.

### 3. Working / Steps

**1. Static Allocation:**
- Memory addresses for variables are bound permanently at compile time.
- Used for: global variables, static variables.
- Cannot support recursion (since each variable has only one fixed memory location).

**2. Stack Allocation:**
- Memory is organized as a stack of **activation records** (also called stack frames).
- Each function call pushes a new activation record; when the function returns, its activation record is popped.
- Supports **recursion** naturally, since each call gets its own fresh activation record.
- **Activation Record typically contains:** return address, parameters, local variables, saved registers, control link (pointer to caller's activation record).

**3. Heap Allocation:**
- Used for data whose size or lifetime cannot be determined at compile time (e.g., dynamically created objects, `malloc`/`new`).
- Memory is allocated and freed explicitly (or via garbage collection) at arbitrary times, not necessarily in LIFO order.
- Supports data that must outlive the function that created it.

### 4. Diagram

```
        High Memory
   +-------------------+
   |       Stack        |  <- grows downward (activation records)
   |         |           |
   |         v           |
   |                     |
   |         ^           |
   |         |           |
   |       Heap          |  <- grows upward (dynamic allocation)
   +-------------------+
   |   Static/Global     |
   +-------------------+
   |   Code (Text)       |
   +-------------------+
        Low Memory
```

**Activation Record Structure:**
```
+----------------------+
| Return Value          |
+----------------------+
| Actual Parameters      |
+----------------------+
| Control Link (to caller)|
+----------------------+
| Saved Registers        |
+----------------------+
| Local Variables        |
+----------------------+
| Temporaries            |
+----------------------+
```

### 5. Example
```c
int fact(int n) {
    if (n == 0) return 1;
    return n * fact(n-1);   // recursive call → new activation record on stack each time
}
```
Each recursive call to `fact` creates a new activation record on the stack, holding its own copy of `n` — this is only possible because of stack allocation.

### 6. Advantages
- **Stack allocation:** Automatic and fast memory management; naturally supports recursion.
- **Heap allocation:** Flexible; supports data with unpredictable size/lifetime.
- **Static allocation:** Simple and fast access (fixed address known at compile time).

### 7. Limitations
- **Stack allocation:** Cannot be used for data that must outlive the function call.
- **Heap allocation:** Slower (dynamic management overhead); risk of memory leaks if not freed properly.
- **Static allocation:** No support for recursion; wastes memory if unused for long periods.

### 8. Applications
- Stack allocation is used for all local variables and function call management in virtually every compiled language (C, Java, etc.).
- Heap allocation is used for dynamic data structures (linked lists, trees) and objects with a lifetime beyond a single function call.

### 9. Conclusion
Runtime environments organize memory into static, stack, and heap regions, each suited to data with different lifetimes — static for permanent data, stack for function-call-scoped data (enabling recursion via activation records), and heap for dynamically sized/lifetime data — together forming the memory management backbone of program execution.

---

## Part 3: Diagram
(Use the memory layout diagram + activation record structure above.)

---

## Part 4: Examiner Keywords
**Runtime Environment**, **Activation Record**, **Static Allocation**, **Stack Allocation**, **Heap Allocation**, Control Link, Recursion, Garbage Collection

---

## Part 5: PYQ Notes
- **Expected Marks:** 6 marks
- **Previous Frequency:** Moderate — appeared as "runtime environments" / "storage allocation strategies" in multiple recent papers
- **Common Mistakes:** Saying static allocation supports recursion (it does NOT); forgetting to mention the activation record structure
- **Related Questions:** "What is an activation record? List its fields."

---

## Part 6: Revision Box
- Static allocation: fixed address at compile time, no recursion support
- Stack allocation: activation records, supports recursion, LIFO order
- Heap allocation: dynamic, unpredictable lifetime, manual/GC managed
- Activation record: return address, parameters, control link, locals, temporaries
- Stack = automatic and fast; Heap = flexible but slower

---

## Part 7: Expected Viva Questions
1. Why can't static allocation support recursion?
2. What is a control link in an activation record?
3. Which allocation strategy is used for `malloc()`?
4. Does heap allocation follow LIFO order?
5. Name one field found in every activation record.

---

## Part 8: Memory Trick
**"Static = Fixed ghar, Stack = LIFO queue (function calls), Heap = Open storage jab chahiye tab lo."**

---
---

# Q32

**Question:**
What is the difference between a Parse Tree and an Abstract Syntax Tree (AST)?

**Probability:** ★★★★☆ (High)

**Why Important:**
- Appeared as a distinct standalone question across multiple papers (separate from generic "syntax tree" coverage in Q19).
- Tests precise understanding of how much detail different tree representations retain — a common source of confusion.
- Short, comparison-style question — easy to score full marks with a clean table + example.

---

## Part 1: Hinglish Concept

**Ye hota kya hai?**
**Parse Tree** ek tree hai jo grammar ke **har production rule ko exactly follow karta hai** — har non-terminal, terminal, aur intermediate step tree me dikhta hai. Ye bahut detailed hota hai.

**AST (Abstract Syntax Tree)** ek **simplified/compact version** hai — sirf jo **actually zaroori hai program ka meaning samajhne ke liye**, wahi rakhta hai. Extra grammar details (jaise parentheses, intermediate non-terminals) hata deta hai.

**Real life example:** Socho tumhe ek recipe di gayi hai bahut detail me — "pehle bowl uthao, phir bowl me pani daalo, phir pani me namak daalo..." Ye **Parse Tree** jaisa hai — har chhota step likha hai. AST wahi recipe ek **summary** me deta hai: "Namak wala pani banao" — sirf essential info.

**Ye kyu use hota hai?**
Parse tree parsing ke process ko verify karne ke liye useful hai (grammar follow ho raha hai ya nahi), lekin AST use hota hai **actual compilation ke aage ke steps** (semantic analysis, code generation) me kyuki wo compact aur kaam ki cheez rakhta hai.

**Exam me isse kya puch sakte hai?**
- Difference table
- Draw both for a given expression

---

## Part 2: English Exam Answer

### 1. Definition
A **Parse Tree** is a tree that represents the syntactic structure of an input string exactly according to the grammar, showing every non-terminal and every derivation step. An **Abstract Syntax Tree (AST)** is a condensed, simplified tree that captures only the essential structure and meaning of the program, omitting grammar-specific details like parentheses and intermediate non-terminals.

### 2. Introduction
While the parser builds a parse tree to verify that the input conforms to the grammar, compilers use the more compact AST for all subsequent phases (semantic analysis, intermediate code generation), since it's easier to process and doesn't carry unnecessary grammar artifacts.

### 3. Working / Steps

**Difference Table:**

| Feature | Parse Tree | Abstract Syntax Tree (AST) |
|---|---|---|
| Detail level | Full — shows every grammar rule/derivation | Condensed — only essential structure |
| Nodes | Includes non-terminals, terminals, punctuation | Only operators and operands (meaningful elements) |
| Size | Larger | Smaller/compact |
| Used by | Parser (to verify syntax) | Semantic analyzer, code generator |
| Also called | Concrete Syntax Tree (CST) | Syntax Tree |

### 4. Diagram

For expression `(a + b) * c`:

**Parse Tree (full grammar detail):**
```
                E
              / | \
             T  *  F
            /|\    |
           ( E )    id(c)
             |
           E + T
           |   |
           T  id(b)
           |
          id(a)
```

**Abstract Syntax Tree (condensed):**
```
              *
            /   \
           +     c
          / \
         a   b
```

### 5. Example
The parse tree above includes every grammar-level detail (parentheses, intermediate T and F non-terminals), while the AST reduces it to just the meaningful operators (`*`, `+`) and operands (`a`, `b`, `c`) — both represent the same expression, but the AST is far more compact and directly usable.

### 6. Advantages
- **Parse Tree:** Useful for verifying that parsing followed the grammar correctly; helpful for debugging the parser itself.
- **AST:** Compact, efficient to traverse; directly usable for semantic analysis and code generation.

### 7. Limitations
- **Parse Tree:** Too detailed and large to use directly for later compiler phases — inefficient.
- **AST:** Loses some syntactic details (like exact parenthesization), which are usually not needed after parsing succeeds.

### 8. Applications
- Parse trees are mainly a conceptual/verification tool during syntax analysis.
- ASTs are the actual data structure carried forward into semantic analysis, intermediate code generation, and optimization in real compilers.

### 9. Conclusion
A parse tree faithfully represents every grammar rule applied during parsing, while an abstract syntax tree condenses this into just the essential program structure — compilers use parse trees conceptually during parsing but work with the more efficient AST for all subsequent phases.

---

## Part 3: Diagram
(Use both trees for `(a+b)*c` above, drawn side by side to show the size/detail difference.)

---

## Part 4: Examiner Keywords
**Parse Tree**, **Abstract Syntax Tree (AST)**, Concrete Syntax Tree, Non-terminal, Terminal, Condensed Representation

---

## Part 5: PYQ Notes
- **Expected Marks:** 6 marks
- **Previous Frequency:** High — appeared as a standalone "difference between" question in multiple papers
- **Common Mistakes:** Treating parse tree and AST as identical; not showing the size/detail reduction clearly in the diagram
- **Related Questions:** See Q19 for the related Syntax Tree vs DAG comparison.

---

## Part 6: Revision Box
- Parse Tree = full grammar detail (every rule shown), also called Concrete Syntax Tree
- AST = condensed, only operators + operands
- Parse tree used during parsing (verification); AST used in later phases
- AST is smaller and more efficient to process

---

## Part 7: Expected Viva Questions
1. What is another name for a parse tree?
2. Why do compilers prefer AST over parse tree for later phases?
3. Does an AST show parentheses from the source code?
4. Which tree is larger — parse tree or AST — for the same expression?
5. Which tree is used for semantic analysis?

---

## Part 8: Memory Trick
**"Parse Tree = Poora detail, AST = Asli matlab (essential meaning) only."**

---
---

# Q33

**Question:**
What is Lex? Explain the structure of a Lex specification and the workflow of a lexical analyzer generator.

**Probability:** ★★★★☆ (High)

**Why Important:**
- Appeared across multiple papers under different framings ("What is Lex? Explain", "structure of a lexical specification", "workflow of a lexical analyzer generator").
- Directly extends the theoretical Lexical Analysis topic (Q6) with concrete tool knowledge — bridges theory and practical implementation.
- Easy to score full marks with the 3-section structure clearly memorized.

---

## Part 1: Hinglish Concept

**Ye hota kya hai?**
**Lex** ek **tool/software** hai jo automatically ek **lexical analyzer** generate kar deta hai. Tumhe bas regular expressions likhne hote hai batane ke liye "kya pattern hai aur usse milne par kya karna hai" — Lex baaki sab (actual scanning code) khud bana deta hai.

**Real life example:** Socho tumhe ek machine chahiye jo automatically letters ko sort kare — tumhe bas rule batana hai "agar 'Mr.' se shuru ho to Male folder me daalo, 'Mrs.' se shuru ho to Female folder me daalo." Lex bhi aise hi kaam karta hai — tum rules (regex + action) do, wo automatically ek scanner bana deta hai.

**Lex file ki 3 sections hoti hai:**
1. **Declarations** — regular definitions aur C code declarations (`%{ ... %}`)
2. **Translation Rules** — pattern aur action pairs (`pattern { action }`)
3. **Auxiliary Functions** — extra helper C functions

Teeno sections `%%` se separate hote hai.

**Workflow:**
Lex specification (`.l` file) → **Lex compiler** process karta hai → C code (`lex.yy.c`) generate hota hai → C compiler use karke final **executable lexical analyzer** ban jaata hai.

**Ye kyu use hota hai?**
Manually lexical analyzer likhna time-consuming hai — Lex isse automate kar deta hai, sirf regex rules likhne se.

**Exam me isse kya puch sakte hai?**
- Explain 3-section structure
- Explain the workflow diagram (Lex file → lex.yy.c → executable)
- Small Lex program example

---

## Part 2: English Exam Answer

### 1. Definition
**Lex** is a lexical analyzer generator tool that automatically produces a lexical analyzer (scanner) in C, based on a specification file containing regular expressions and corresponding actions.

### 2. Introduction
Instead of manually writing code to recognize tokens, a compiler developer writes a Lex specification describing token patterns using regular expressions; the Lex tool compiles this into executable C code capable of scanning source input and producing tokens.

### 3. Working / Steps

**Structure of a Lex Specification File (3 sections, separated by `%%`):**

```
{Declarations}
%%
{Translation Rules}
%%
{Auxiliary Functions}
```

1. **Declarations Section:** Contains regular definitions (named patterns) and any C declarations/header includes, enclosed in `%{ ... %}`.
2. **Translation Rules Section:** Contains pattern–action pairs in the form `pattern { action }` — when input matches a pattern, the corresponding C action code executes (often returning a token).
3. **Auxiliary Functions Section:** Contains any additional helper C functions used by the actions (e.g., a `main()` function or utility routines).

**Workflow of a Lexical Analyzer Generator:**
1. Write a Lex specification file (`lexfile.l`) describing patterns and actions.
2. Run it through the **Lex compiler**, which translates it into a C program `lex.yy.c` (this program implements a DFA-based scanner internally, using Thompson's Construction + Subset Construction principles from Q23).
3. Compile `lex.yy.c` using a standard C compiler, linking with the Lex library.
4. The result is an executable lexical analyzer that reads source input and outputs a stream of tokens.

### 4. Diagram

```
   lex.l (Lex specification)
          |
          v
   +----------------+
   |  Lex Compiler   |
   +----------------+
          |
          v
     lex.yy.c (generated C code)
          |
          v
   +----------------+
   |   C Compiler    |
   +----------------+
          |
          v
    a.out (Lexical Analyzer executable)
          |
          v
   Source Program → Tokens
```

### 5. Example — Simple Lex Program (recognizing digits and identifiers)
```
%{
#include <stdio.h>
%}

DIGIT   [0-9]+
LETTER  [a-zA-Z][a-zA-Z0-9]*

%%
{DIGIT}   { printf("NUMBER: %s\n", yytext); }
{LETTER}  { printf("IDENTIFIER: %s\n", yytext); }
%%

int main() {
    yylex();
    return 0;
}
```

### 6. Advantages
- Automates the tedious, error-prone task of manually writing a scanner.
- Regular-expression-based rules are concise and easy to modify.
- Generated scanner is efficient (DFA-based internally).

### 7. Limitations
- Generated code can be less readable/customizable than a hand-written scanner.
- Limited to regular-expression-recognizable patterns (cannot handle context-sensitive lexical rules directly).

### 8. Applications
- Used to build lexical analyzers for real compilers and interpreters.
- Also used in other text-processing tools requiring pattern-based scanning (e.g., simple text parsers, log analyzers).

### 9. Conclusion
Lex is a lexical analyzer generator that converts a simple, regex-based specification (organized into declarations, rules, and auxiliary functions) into an efficient, executable scanner, automating one of the most repetitive parts of compiler construction.

---

## Part 3: Diagram
(Use the workflow diagram above: lex.l → Lex Compiler → lex.yy.c → C Compiler → executable.)

---

## Part 4: Examiner Keywords
**Lex**, Lexical Analyzer Generator, **lex.yy.c**, Declarations, Translation Rules, Auxiliary Functions, `yytext`, `yylex()`

---

## Part 5: PYQ Notes
- **Expected Marks:** 6 marks
- **Previous Frequency:** High — appeared under multiple framings across several papers ("What is Lex?", "structure of lexical specification", "workflow of lexical analyzer generator")
- **Common Mistakes:** Forgetting the `%%` separators between the 3 sections; not mentioning that `lex.yy.c` must still be compiled by a C compiler afterward
- **Related Questions:** "Write a Lex program for [specific task]", see Q23 for the underlying NFA/DFA theory Lex uses internally.

---

## Part 6: Revision Box
- Lex = lexical analyzer generator tool
- 3 sections (separated by `%%`): Declarations, Translation Rules, Auxiliary Functions
- Workflow: lex.l → Lex compiler → lex.yy.c → C compiler → executable scanner
- `yytext` holds the matched lexeme; `yylex()` is the main scanning function
- Internally uses DFA (built via Thompson's + Subset Construction, see Q23)

---

## Part 7: Expected Viva Questions
1. What are the three sections of a Lex specification file?
2. What file does the Lex compiler generate?
3. What does `yytext` represent?
4. Is `lex.yy.c` directly executable, or does it need further compilation?
5. What underlying automata theory does Lex use internally to build the scanner?

---

## Part 8: Memory Trick
**"DTA"** — **D**eclarations, **T**ranslation rules, **A**uxiliary functions (3 sections of a Lex file, separated by `%%`).

---
---

# FINAL MASTER SUMMARY — All 33 Questions

| # | Topic | Probability | Unit |
|---|---|---|---|
| 21 | Basic Block & Flow Graph | ★★★★★ | Unit 4/5 |
| 22 | SDD/SDT + Annotated Parse Tree | ★★★★★ | Unit 4 |
| 1 | Compiler Phases + Tools | ★★★★★ | Unit 1 |
| 26 | Code Generation — Design Issues | ★★★★☆ | Unit 5/6 |
| 8, 19 | DAG Representation of Basic Blocks | ★★★★☆ | Unit 4 |
| 6 | Tokens, Lexeme, Pattern | ★★★★★ | Unit 1 |
| 27 | Top-Down vs Bottom-Up + Shift-Reduce | ★★★★☆ | Unit 2/3 |
| 3, 15, 16 | FIRST/FOLLOW + Predictive Parsing Table | ★★★★★ | Unit 2 |
| 2, 10 | Left Recursion + Left Factoring | ★★★★★ | Unit 2 |
| 23 | Regex → NFA → DFA (Thompson's/Subset) | ★★★★☆ | Unit 1 |
| 8, 12, 20 | Code Optimization (types, techniques) | ★★★★★ | Unit 4 |
| 7, 13 | Symbol Table | ★★★★☆ | Unit 1/4 |
| 28 | Three-Address Code / Quadruples-Triples | ★★★☆☆ | Unit 4 |
| 9, 18 | SLR/LALR/CLR Parsing Table | ★★★★★ | Unit 3 |
| 24 | Input Buffering (Buffer Pairs & Sentinels) | ★★★☆☆ | Unit 1 |
| 25 | Intermediate Code Gen (if-else/while/switch) | ★★★★☆ | Unit 4 |
| 29 | LL(1) Grammar Check | ★★★☆☆ | Unit 2 |
| 17 | Operator Precedence Parsing | ★★★★☆ | Unit 3 |
| 5, 30 | Register Allocation / Descriptors | ★★★★☆ | Unit 5/6 |
| 4 | Type Checking & Conversion | ★★★★☆ | Unit 4 |
| 11 | Ambiguous Grammar | ★★★☆☆ | Unit 2 |
| **31** | **Runtime Environments / Storage Allocation (Stack/Heap)** | ★★★★☆ | Unit 4/5 |
| **32** | **Parse Tree vs Abstract Syntax Tree** | ★★★★☆ | Unit 2/4 |
| **33** | **Lex Tool — Structure & Workflow** | ★★★★☆ | Unit 1 |

**This 33-question bank now covers all high-priority topics confirmed against 10 real DBATU exam papers**, closing the storage allocation, parse-tree-vs-AST, and Lex-tool gaps identified in the cross-check. Let me know if you'd like the cheat sheet updated with Q31–Q33.
