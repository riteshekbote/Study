# DBATU Compiler Design (BTCOC601) — Theory Question & Answer Set
### Simple English Version — Easy to Read and Remember

---

# UNIT 1

---

## Q1. Explain the Phases of Compiler with neat diagram.

**Answer:**

A compiler is a program. It takes code written by a programmer (high-level language) and changes it into code that a computer can run (machine language).

A compiler does this work in small steps. Each step is called a **phase**. There are 6 main phases.

**1. Lexical Analysis**
This phase reads the code letter by letter. It groups letters into small pieces called **tokens**. For example, it can find words like `if`, `x`, `+`, `123`.

**2. Syntax Analysis**
This phase checks if the tokens are arranged in the correct order, as per the grammar rules of the language. It builds a tree shape called a **parse tree**.

**3. Semantic Analysis**
This phase checks the meaning of the code. It checks things like: Are the variable types correct? Is the variable declared before use?

**4. Intermediate Code Generation**
This phase changes the code into a simple, middle-form code. This code is not for any specific computer. It is called **Three Address Code**.

**5. Code Optimization**
This phase improves the code. It makes the code faster or smaller. But the meaning of the code does not change.

**6. Code Generation**
This is the last phase. It changes the code into the final machine code (the code the computer actually runs).

**Diagram:**

```
        Source Program (code written by programmer)
                 |
        Lexical Analyzer  --->  gives Tokens
                 |
        Syntax Analyzer   --->  gives Parse Tree
                 |
        Semantic Analyzer --->  gives Checked Tree
                 |
        Intermediate Code Generator ---> gives Simple Code
                 |
        Code Optimizer    --->  gives Better Code
                 |
        Code Generator    --->  gives Machine Code
```

Two more parts help in every phase:
- **Symbol Table**: It stores information about all variable names (like their type and location).
- **Error Handler**: It catches and reports errors at every phase.

**Simple Example:**
If the code is `a = b + c`, the compiler will:
- Break it into tokens: `a`, `=`, `b`, `+`, `c`
- Check the grammar is correct
- Check the types of a, b, c are correct
- Create simple code like `t1 = b + c` then `a = t1`
- Improve this code if possible
- Convert it to final machine instructions

**Conclusion:**
A compiler works in 6 clear steps. Each step does one small job. Together, these steps convert human-written code into a working program.

---

## Q2. Explain Lexical Analysis. What are Tokens, Lexemes and Patterns?

**Answer:**

**Lexical Analysis** is the first phase of a compiler. In this phase, the compiler reads the program one character at a time. It groups these characters into meaningful pieces. These pieces are called tokens. This phase also removes extra spaces and comments, because they are not needed for the next steps.

There are three important words to remember: **Token**, **Lexeme**, and **Pattern**.

**Token:**
A token is a name or category for a group of characters. For example: `identifier`, `number`, `keyword`.

**Lexeme:**
A lexeme is the actual word or symbol found in the code. For example: `total`, `25`, `if`.

**Pattern:**
A pattern is a rule that tells how a lexeme should look. For example, the pattern for an identifier is: "starts with a letter, then can have letters or digits".

**Simple Table:**

| Word | Meaning | Example |
|---|---|---|
| Token | The category/type | id, num, keyword |
| Lexeme | The actual word | total, 25, if |
| Pattern | The rule to match | letter followed by letters or digits |

**Example:**
For the code: `sum = a + 25;`

| Lexeme | Token |
|---|---|
| sum | identifier |
| = | assignment operator |
| a | identifier |
| + | plus operator |
| 25 | number |
| ; | semicolon |

**Conclusion:**
Lexical Analysis changes the raw program into small, clean tokens. This makes it easy for the next phase (Syntax Analysis) to check the grammar.

---

## Q3. Explain Regular Expressions and their applications.

**Answer:**

A **Regular Expression** is a short way to write a pattern. It tells us what kind of text is allowed. Compilers use regular expressions to describe how tokens should look (like how an identifier or a number should look).

**Basic Rules of Regular Expressions:**
- A single letter matches itself. Example: `a` matches only "a".
- The symbol `|` means "OR". Example: `a|b` means "a" or "b".
- Writing two things together means "one after another" (concatenation). Example: `ab` means "a" then "b".
- The symbol `*` means "zero or more times" (this is called Kleene star). Example: `a*` means "", "a", "aa", "aaa", and so on.

**Simple Examples:**
- Identifier pattern: `letter (letter | digit)*` — This means: start with one letter, then any number of letters or digits.
- Number pattern: `digit digit*` — This means: one digit, followed by any number of more digits.
- A regular expression for keyword `if`: simply `if`.

**Applications of Regular Expressions:**
1. Used to define tokens like identifiers, keywords, numbers in a compiler.
2. Used to build lexical analyzers (like the tool Lex uses regular expressions to build a scanner).
3. Used in text editors and search tools (like "Find and Replace" features).
4. Used in tools like `grep` for pattern searching in files.
5. Used for input validation (like checking if an email address or phone number is in the correct format).

**Conclusion:**
Regular expressions give a short and clear way to describe patterns of characters. Compilers use them to correctly recognize tokens during lexical analysis.

---

## Q4. Explain Input Buffering in Lexical Analyzer.

**Answer:**

**Input Buffering** is a method used by the lexical analyzer to read the source program quickly and smoothly. Instead of reading the code one character at a time from the disk (which is slow), the compiler reads a big chunk of code into memory at once. This chunk is called a **buffer**.

**Why do we need this?**
Reading from the disk again and again is slow. So the compiler reads a large block of characters together and keeps it ready in memory. This saves time.

**Two-Buffer Scheme:**
The compiler uses two buffers, not just one.
1. While the lexical analyzer is reading from Buffer 1, Buffer 2 can be filled in the background.
2. When Buffer 1 finishes, the analyzer moves to Buffer 2 without waiting.
3. This way, reading never stops.

Two pointers are used:
- **lexemeBegin**: shows where the current word (lexeme) starts.
- **forward**: moves ahead to find where the current word ends.

**What is a Sentinel?**
A sentinel is a special character (usually called `eof`) placed at the end of each buffer.

Normally, for every character, the analyzer has to check two things:
1. Is this the end of the buffer?
2. Does this character match the pattern?

Using a sentinel, both checks become one check. The analyzer only needs to look for the sentinel character. If it finds the sentinel, only then it checks if the buffer has really ended. This makes checking faster.

**Diagram:**
```
   Buffer 1                    Buffer 2
+----------------+eof+----------------+eof
| a = b + c      |   |                |
+----------------+   +----------------+
        ^                    ^
   lexemeBegin           forward
```

**Conclusion:**
Input Buffering with a two-buffer scheme and sentinel characters helps the lexical analyzer read the source program quickly, using fewer checks and less time.

---

## Q5. Explain Compiler Construction Tools (LEX & YACC).

**Answer:**

Building a compiler by writing every part by hand is a hard and long job. So, there are special tools that help build parts of a compiler automatically. Two very famous tools are **LEX** and **YACC**.

**LEX (Lexical Analyzer Generator):**
LEX is a tool that creates a lexical analyzer automatically. The programmer only needs to write simple rules (using regular expressions) that describe the tokens. LEX reads these rules and creates a C program that can scan the source code and produce tokens.

A LEX file has three parts, separated by `%%`:
1. **Declarations**: contains regular definitions and C code to include.
2. **Translation Rules**: contains pattern and action pairs (what to do when a pattern is matched).
3. **Auxiliary Functions**: extra helper functions written in C.

**YACC (Yet Another Compiler Compiler):**
YACC is a tool that creates a parser automatically. The programmer writes the grammar rules of the language. YACC reads these rules and creates a program that can check if the input follows the grammar (syntax analysis). YACC is often used together with LEX: LEX creates the tokens, and YACC checks if the tokens follow the grammar.

**How they work together:**
```
Lex Specification file (.l)  --->  Lex compiler  --->  lex.yy.c (C code for scanner)
Yacc Specification file (.y) --->  Yacc compiler --->  y.tab.c (C code for parser)

Both C files are compiled together --->  Final working compiler/parser
```

**Other Compiler Construction Tools:**
- **LLVM**: helps in code generation and optimization.
- **JavaCC**: a parser generator for Java.
- **ANTLR**: another popular parser generator.

**Advantages:**
- Saves a lot of time, since we do not need to write the scanner or parser code by hand.
- Reduces mistakes, since the tool generates correct, tested code.
- Easy to change rules if the language grammar changes.

**Conclusion:**
LEX and YACC are very useful tools in compiler building. LEX creates the lexical analyzer using regular expressions, and YACC creates the parser using grammar rules, saving a lot of manual work.

---

# UNIT 2

---

## Q6. Explain Top-Down Parsing and Bottom-Up Parsing with comparison.

**Answer:**

Parsing means checking if the input program follows the grammar rules, and building a tree structure (called a parse tree) for it. There are two main ways to do parsing: **Top-Down Parsing** and **Bottom-Up Parsing**.

**Top-Down Parsing:**
In this method, we start building the tree from the top (the start symbol) and go down to the bottom (the actual words in the input). We guess which rule to use, and check if it matches the input.
Examples: Recursive Descent Parser, LL(1) Parser (Predictive Parser).

**Bottom-Up Parsing:**
In this method, we start from the bottom (the actual input words) and build the tree upward, until we reach the top (the start symbol). We look at small pieces of input and try to combine them step by step.
Examples: Shift-Reduce Parser, LR Parsers (SLR, CLR, LALR).

**Comparison Table:**

| Point | Top-Down Parsing | Bottom-Up Parsing |
|---|---|---|
| Tree building direction | From root to leaves | From leaves to root |
| Type of derivation used | Leftmost derivation | Rightmost derivation, done in reverse |
| Left recursion | Cannot be used (causes infinite loop) | Can be used without any problem |
| Power | Less powerful, works on simpler grammars | More powerful, works on more grammars |
| Example parsers | Recursive Descent, LL(1) | Shift-Reduce, LR(0), SLR, CLR, LALR |

**Simple way to remember:**
Top-Down = start with the big goal, break it into small parts (like planning a trip first, then filling in details).
Bottom-Up = start with small parts, join them to make the big goal (like building a house brick by brick).

**Conclusion:**
Top-Down and Bottom-Up are two different ways of building a parse tree. Bottom-up parsing is generally more powerful, but top-down parsing is simpler to understand and implement by hand.

---

## Q7. Eliminate Left Recursion with suitable example.

**Answer:**

**Left Recursion** happens when a grammar rule uses itself again, right at the start of its own definition. This causes a big problem: if we try to use a top-down parser on it, the parser will keep repeating itself forever, and never finish (this is called an infinite loop).

**General Rule to Remove Left Recursion:**

If a rule looks like this:
```
A → A alpha | beta
```
(where "alpha" is the extra part, and "beta" does not start with A)

We change it to:
```
A  → beta A'
A' → alpha A' | epsilon
```
(Here, "epsilon" means "nothing" or "empty".)

**Example:**

Take this grammar:
```
E → E + T | T
```

Here, A = E, alpha = "+ T", beta = "T".

Apply the rule:
```
E  → T E'
E' → + T E' | epsilon
```

This new grammar means exactly the same thing as before, but now it does not cause an infinite loop in a top-down parser.

**Why does this work?**
In the new grammar, we always write "T" first, and after that, we can either continue with "+T" many times, or stop (epsilon). This avoids the parser calling itself at the very beginning.

**Conclusion:**
Left recursion is a common problem for top-down parsers. It can always be removed using the simple rule: change `A → Aα | β` into `A → βA'` and `A' → αA' | ε`. This keeps the same language, but makes it safe to parse.

---

## Q8. Explain Left Factoring with example.

**Answer:**

**Left Factoring** is used when two or more rules of the same non-terminal start with the same beginning part (same prefix). This causes confusion for a top-down parser, because it cannot decide which rule to use, just by looking at the first symbol.

**General Rule for Left Factoring:**

If a rule looks like this:
```
A → alpha beta1 | alpha beta2
```
(where "alpha" is the common starting part)

We change it to:
```
A  → alpha A'
A' → beta1 | beta2
```

**Example:**

Take this grammar:
```
S → iEtS | iEtSeS | a
E → b
```

Here, both `iEtS` and `iEtSeS` start with the same part: `iEtS`. This is the common prefix (alpha).

Apply the rule:
```
S  → iEtS S'
S' → eS | epsilon
E  → b
```

**Why is this needed?**
This grammar is like an "if-then-else" statement in programming. Without left factoring, the parser cannot know if it should expect an "else" part or not, just by seeing the beginning of the statement. After left factoring, the parser can first read the common part, and only later decide if there is an "else" (`eS`) or nothing (`epsilon`).

**Conclusion:**
Left factoring removes confusion caused by common starting parts in grammar rules. It helps a top-down parser make a clear decision using just one lookahead symbol.

---

## Q9. Compute FIRST and FOLLOW for the given grammar.

**Answer:**

**FIRST** and **FOLLOW** are two important ideas used in building parsing tables for top-down parsers.

**What is FIRST?**
FIRST of a symbol tells us: "What is the very first letter/token that can appear, if we fully expand this symbol?"

**What is FOLLOW?**
FOLLOW of a non-terminal tells us: "What token can come right after this non-terminal, in some valid sentence of the grammar?"

**Simple Rules for FIRST:**
1. If X is a terminal (like `+`, `id`), then FIRST(X) = {X} itself.
2. If a rule says `X → epsilon`, then epsilon is added to FIRST(X).
3. If a rule says `X → Y1 Y2 Y3...`, we look at FIRST(Y1). If Y1 cannot become empty, FIRST(X) = FIRST(Y1). If Y1 can become empty, we also look at Y2, and so on.

**Simple Rules for FOLLOW:**
1. The start symbol of the grammar always has `$` (end marker) in its FOLLOW set.
2. If a rule says `A → alpha B beta`, then whatever is in FIRST(beta) (except epsilon) is added to FOLLOW(B).
3. If a rule says `A → alpha B` (B is at the very end), or if beta can become empty, then whatever is in FOLLOW(A) is also added to FOLLOW(B).

**Example Grammar:**
```
E  → T E'
E' → + T E' | epsilon
T  → F T'
T' → * F T' | epsilon
F  → ( E ) | id
```

**FIRST Table:**

| Symbol | FIRST |
|---|---|
| E | ( , id |
| E' | + , epsilon |
| T | ( , id |
| T' | * , epsilon |
| F | ( , id |

**FOLLOW Table:**

| Symbol | FOLLOW |
|---|---|
| E | ) , $ |
| E' | ) , $ |
| T | + , ) , $ |
| T' | + , ) , $ |
| F | * , + , ) , $ |

**Conclusion:**
FIRST tells us what a symbol can start with, and FOLLOW tells us what can come right after a symbol. Both are needed to build the parsing table for a top-down parser.

---

## Q10. Construct Predictive Parsing (LL(1)) Table.

**Answer:**

A **Predictive Parser**, also called an **LL(1) Parser**, is a type of top-down parser. It uses a table to decide which rule to use, just by looking at one input symbol ahead (this is called "1 lookahead"). It does not need to guess or go back (no backtracking).

**Steps to Build the LL(1) Table:**
1. First, find the FIRST and FOLLOW sets for every non-terminal (see Q9).
2. For every rule `A → alpha`:
   - Look at FIRST(alpha). For every terminal symbol `a` in FIRST(alpha), place the rule `A → alpha` in the table cell [A, a].
   - If epsilon is in FIRST(alpha), then also look at FOLLOW(A). For every terminal `b` in FOLLOW(A), place the rule `A → alpha` in the table cell [A, b].
3. Every empty cell in the table means an error will occur there.

**Example Table (for the grammar in Q9):**

| | id | + | * | ( | ) | $ |
|---|---|---|---|---|---|---|
| E | E→TE' | | | E→TE' | | |
| E' | | E'→+TE' | | | E'→ε | E'→ε |
| T | T→FT' | | | T→FT' | | |
| T' | | T'→ε | T'→*FT' | | T'→ε | T'→ε |
| F | F→id | | | F→(E) | | |

**How the Parser Uses This Table:**
The parser keeps a stack of symbols and reads input one symbol at a time. If the top of the stack is a terminal and it matches the input, the parser removes it and moves ahead. If the top of the stack is a non-terminal, the parser looks at the table using the non-terminal and the current input symbol, and replaces it with the correct rule from the table.

**Conclusion:**
The LL(1) table tells the parser exactly which rule to use, for every non-terminal and every possible next input symbol. This makes parsing fast and simple, without needing to guess.

---

## Q11. Explain Shift Reduce Parsing with example.

**Answer:**

**Shift-Reduce Parsing** is a type of bottom-up parsing. It uses a stack to build the parse tree from the bottom (leaves) upward to the top (start symbol).

**Four Main Actions:**
1. **Shift**: Take the next input symbol and push it onto the stack.
2. **Reduce**: If the symbols on top of the stack match the right-hand side of a grammar rule, replace them with the left-hand side of that rule.
3. **Accept**: If the stack has only the start symbol, and all input is used, then the string is successfully parsed.
4. **Error**: If neither shift nor reduce can happen, there is a mistake in the input.

**Example:**

Grammar:
```
E → E + T | T
T → id
```

Parsing the input `id + id`:

| Stack | Remaining Input | Action |
|---|---|---|
| empty | id + id | Shift |
| id | + id | Reduce, using T → id |
| T | + id | Reduce, using E → T |
| E | + id | Shift |
| E + | id | Shift |
| E + id | (nothing left) | Reduce, using T → id |
| E + T | (nothing left) | Reduce, using E → E + T |
| E | (nothing left) | Accept |

**Conclusion:**
Shift-Reduce Parsing uses a stack and repeats two main actions, shift and reduce, until the whole input becomes the start symbol. This is the basic idea behind more advanced parsers like LR parsers.

---

## Q12. Differentiate SLR, CLR and LALR Parsers.

**Answer:**

SLR, CLR, and LALR are all types of bottom-up (LR) parsers. They are all similar, but they use different amounts of extra information (called "lookahead") to avoid mistakes, and this changes how big their parsing tables are.

**SLR (Simple LR):**
This is the simplest type. It uses simple items (without lookahead) plus the FOLLOW set to decide when to reduce. It is easy to build, but it is not very powerful. Some grammars will show errors (called conflicts) even though they are not truly wrong.

**CLR (Canonical LR):**
This is the most powerful type. Each item carries its own specific lookahead symbol. This makes CLR very accurate, with very few conflicts. But the table becomes very large, so it needs a lot of memory.

**LALR (Look-Ahead LR):**
This type tries to get the best of both. It builds states like CLR, but then joins together (merges) states that have the same core (only different lookahead). This makes the table almost as small as SLR, but almost as powerful as CLR. This is why LALR is the most commonly used type in real tools, like YACC.

**Comparison Table:**

| Feature | SLR | CLR | LALR |
|---|---|---|---|
| Lookahead used | FOLLOW set | Specific for each item | Specific, but merged states |
| Table Size | Small | Very Large | Small (same as SLR) |
| Parsing Power | Lowest | Highest | Almost as high as CLR |
| Common Use | Simple grammars | Rarely used (too big) | Most widely used (YACC) |

**Simple way to remember:**
SLR = simple but weak.
CLR = strong but very big.
LALR = almost as strong as CLR, but small like SLR. This is why it is used the most.

**Conclusion:**
SLR, CLR, and LALR are three types of LR parsers with different power and table sizes. LALR gives the best balance, so it is the most used one in real compilers.

---

# UNIT 3

---

## Q13. Explain Syntax Directed Definition (SDD) with suitable example.

**Answer:**

A **Syntax Directed Definition (SDD)** is a grammar where every rule has some extra information attached to it. This extra information is called a **semantic rule**. These semantic rules tell us how to calculate a value, using the grammar rule.

**Why do we need SDD?**
When a compiler parses an expression, it also needs to find its meaning or value, not just check if it is correct. SDD helps us calculate this meaning, step-by-step, using the grammar.

**Example:**

Grammar with Semantic Rules:

| Rule | Semantic Rule |
|---|---|
| E → E1 + T | E.val = E1.val + T.val |
| E → T | E.val = T.val |
| T → T1 * F | T.val = T1.val × F.val |
| T → F | T.val = F.val |
| F → ( E ) | F.val = E.val |
| F → digit | F.val = digit.lexval |

**How it works:**
For the expression `3*5+4`, the compiler will:
1. Find F.val = 3 and F.val = 5 (from the digit rules).
2. Calculate T.val = 3 × 5 = 15.
3. Find F.val = 4.
4. Calculate E.val = 15 + 4 = 19.

So the final value of the whole expression is 19.

**Conclusion:**
SDD connects grammar rules with meaning. It lets the compiler calculate the value or meaning of an expression, step by step, while checking that it follows the grammar.

---

## Q14. Differentiate Synthesized and Inherited Attributes with Annotated Parse Tree.

**Answer:**

In a Syntax Directed Definition, every symbol can carry a value. This value is called an **attribute**. There are two types of attributes: **Synthesized** and **Inherited**.

**Synthesized Attribute:**
This value is calculated using the values of the **children** in the parse tree. The value flows from bottom to top.
Example: `E.val = E1.val + T.val` — here, E gets its value from its children, E1 and T.

**Inherited Attribute:**
This value is calculated using the value of the **parent** or a **sibling** in the parse tree. The value flows from top to bottom, or sideways.
Example: passing the type of a variable (like `int`) down to each name in a list of variable declarations.

**Comparison Table:**

| Point | Synthesized Attribute | Inherited Attribute |
|---|---|---|
| Value comes from | Children nodes | Parent or sibling nodes |
| Direction of flow | Bottom to top | Top to bottom (or sideways) |
| Example | E.val = E1.val + T.val | Passing "type" to a declaration list |

**Annotated Parse Tree:**
An "annotated" parse tree is simply a normal parse tree, but with the calculated attribute values written next to each node.

**Example (for 3*5+4):**
```
              E.val = 19
             /    |    \
        E.val=15  +   T.val = 4
        /
    T.val = 15
   /   |   \
 T.val=3 * F.val=5
```

This tree shows the values written (annotated) at every node, calculated using synthesized attributes (children values combine to give the parent value).

**Conclusion:**
Synthesized attributes get their value from children (bottom to top), while inherited attributes get their value from parents or siblings (top to bottom). An annotated parse tree shows these calculated values placed at each node of the tree.

---

## Q15. Explain Syntax Directed Translation (SDT).

**Answer:**

**Syntax Directed Translation (SDT)** is similar to SDD, but instead of just having semantic rules, it has small pieces of code, called **semantic actions**, written directly inside the grammar rule, usually inside curly brackets `{ }`. These actions run at a fixed point during parsing.

**Difference from SDD:**
In SDD, we do not say exactly when the rule should run. In SDT, the action is placed exactly where it should run, inside the rule itself.

**Example: SDT to make Three Address Code**

```
S → id = E        { gen(id.name = E.place); }
E → E1 + T        { E.place = newTemp(); gen(E.place = E1.place + T.place); }
E → T             { E.place = T.place; }
T → T1 * F        { T.place = newTemp(); gen(T.place = T1.place * F.place); }
T → F             { T.place = F.place; }
F → id            { F.place = id.name; }
```

Here, `newTemp()` creates a new temporary variable name (like t1, t2), and `gen()` writes out one line of simple three-address code.

**Example Output:**
For the expression `a + b * c`, this SDT will produce:
```
t1 = b * c
t2 = a + t1
```

**Conclusion:**
SDT places semantic actions directly inside grammar rules, so the compiler knows exactly when to run each action. This is very useful for generating intermediate code while parsing.

---

## Q16. Explain Symbol Table Organization.

**Answer:**

A **Symbol Table** is a special storage area used by the compiler. It keeps information about every name (identifier) used in the program, such as variable names, function names, and constants.

**Information Stored in Symbol Table:**
- Name of the variable/function
- Data type (int, float, etc.)
- Scope (where in the program it is valid, like inside a function or globally)
- Memory address or location
- Size (for arrays)
- Line number where it was declared

**Main Operations on a Symbol Table:**
1. **Insert**: adds a new name and its details into the table.
2. **Lookup**: searches for a name and finds its details.

**Ways to Organize (Implement) a Symbol Table:**

| Method | Search Time | Notes |
|---|---|---|
| Simple List (Array) | Slow | Easy to build, but slow for big programs |
| Sorted Array | Medium | Faster search, but slow to insert new items |
| Linked List | Slow | Easy to insert, but slow to search |
| Hash Table | Fast | Most commonly used, very fast on average |
| Search Tree | Medium | Balanced and organized, medium speed |

**Why is the Symbol Table Important?**
1. It is used to check if a variable is declared before it is used.
2. It helps in checking data types (type checking).
3. It helps manage scope (so the same name can be used in different parts safely).
4. It gives memory addresses to the code generator.

**Conclusion:**
The Symbol Table stores useful information about every name in a program. It is built starting from the lexical analysis phase, and it is used by almost every other phase of the compiler, especially for type checking and memory allocation.

---

# UNIT 4

---

## Q17. Explain Intermediate Code Generation.

**Answer:**

**Intermediate Code Generation** is a phase of the compiler where the source code is changed into a simple, easy-to-handle code. This code is not the final machine code — it is a middle step between the source code and the machine code.

**Why do we need Intermediate Code?**
1. It makes the compiler easier to build for different computers. We can reuse the front part (lexical, syntax, semantic analysis) for many machines, and only change the last part (code generator) for each machine.
2. It makes it easier to do code optimization, because the intermediate code is simple and clear.
3. It helps in detecting errors more easily, since it is simpler than machine code.

**Common Forms of Intermediate Code:**
- **Three Address Code (TAC)**: statements like `x = y op z`, with at most one operator.
- **Abstract Syntax Tree (AST)**: a tree structure showing only the important parts of the program.
- **Control Flow Graph (CFG)**: a graph showing how control moves between different blocks of code.

**Example:**
For the statement `a = b + c * 2`, the intermediate code will be:
```
t1 = c * 2
t2 = b + t1
a = t2
```

**Conclusion:**
Intermediate Code Generation creates a simple, machine-independent form of the program. This helps in easier optimization and makes the compiler simpler to build for different target machines.

---

## Q18. Explain Three Address Code with examples.

**Answer:**

**Three Address Code (TAC)** is a type of intermediate code. Every statement in TAC has at most **three addresses** (values): usually two operands (input values) and one result.

**General Form:**
```
result = operand1 operator operand2
```

**Rules of Three Address Code:**
- Only one operator is allowed in each statement.
- Extra temporary variables (like t1, t2) are created when needed, to break big expressions into smaller steps.

**Example 1:**
For the expression `a = b + c * d`:
```
t1 = c * d
t2 = b + t1
a = t2
```

**Example 2:**
For the expression `x = (a + b) * (c - d)`:
```
t1 = a + b
t2 = c - d
t3 = t1 * t2
x = t3
```

**Example 3 (with condition, using goto):**
For `if (a < b) x = 1; else x = 2;`:
```
if a < b goto L1
goto L2
L1: x = 1
    goto L3
L2: x = 2
L3:
```

**Advantages of Three Address Code:**
- Easy to read and understand.
- Easy to optimize.
- Easy to convert into final machine code.

**Conclusion:**
Three Address Code breaks down complex expressions into small, simple steps, with each step having at most one operator. This makes it easy for the compiler to further optimize and translate the code.

---

## Q19. Explain Quadruples, Triples and Indirect Triples.

**Answer:**

Three Address Code can be stored inside the compiler in different ways. Three common ways are: **Quadruples**, **Triples**, and **Indirect Triples**.

**Quadruples:**
Each statement is stored using 4 parts: operator, first operand, second operand, and result. The result is given its own name.

| # | operator | arg1 | arg2 | result |
|---|---|---|---|---|
| 1 | * | a | b | t1 |
| 2 | + | t1 | c | t2 |

**Triples:**
Each statement is stored using only 3 parts: operator, first operand, second operand. There is no separate result field. Instead, other statements refer to this statement using its position number.

| # | operator | arg1 | arg2 |
|---|---|---|---|
| (0) | * | a | b |
| (1) | + | (0) | c |

**Indirect Triples:**
This is like triples, but we also keep a separate list that tells the order in which the triples should be used. This makes it easy to change the order of statements (useful in optimization), without moving the actual triples.

```
Statement List:            Triple List:
(1) -> points to (100)     (100) * a b
(2) -> points to (101)     (101) + (100) c
```

**Comparison Table:**

| Feature | Quadruples | Triples | Indirect Triples |
|---|---|---|---|
| Number of fields | 4 | 3 | 3 (plus a pointer list) |
| Memory used | More (extra result field) | Less | Less, plus small pointer list |
| Easy to reorder? | Yes, easy | No, hard (position changes) | Yes, easy (only change pointer list) |

**Conclusion:**
Quadruples, Triples, and Indirect Triples are three different ways to store Three Address Code inside a compiler. Each one has a trade-off between memory usage and ease of reordering statements during optimization.

---

## Q20. Generate Three Address Code for a given expression.

**Answer:**

To generate Three Address Code for any expression, we follow simple steps.

**Steps:**
1. Find the operator that should be done first (following normal maths rules, like multiplication before addition, or brackets first).
2. Create a new temporary variable (like t1) to store the result of this first step.
3. Continue this process for the next operator, using the previous temporary variable if needed.
4. Repeat until the whole expression is broken down.

**Example 1:**
Expression: `a = b + c * 2`

Step 1: `c * 2` happens first (multiplication before addition):
```
t1 = c * 2
```
Step 2: Now add `b`:
```
t2 = b + t1
```
Step 3: Assign to `a`:
```
a = t2
```

**Final Answer:**
```
t1 = c * 2
t2 = b + t1
a = t2
```

**Example 2:**
Expression: `y = a * b + a * c`

Step 1: `a * b` first:
```
t1 = a * b
```
Step 2: `a * c` next:
```
t2 = a * c
```
Step 3: Add both:
```
t3 = t1 + t2
```
Step 4: Assign to `y`:
```
y = t3
```

**Conclusion:**
To generate Three Address Code, we always break the expression down step by step, following the normal order of operations, and using temporary variables to store the middle results.

---

# UNIT 5

---

## Q21. Explain Basic Block and Flow Graph with example.

**Answer:**

**Basic Block:**
A basic block is a group of program statements which are always executed together, one after another, with no jumps in the middle. Control enters only at the first statement, and leaves only at the last statement.

**Flow Graph:**
A flow graph is a diagram made of basic blocks. Each basic block is shown as a box (node). Arrows between boxes show which block can run after another block.

**How to Find the Start of Each Basic Block (called a Leader):**
1. The very first statement of the program is always a leader.
2. Any statement that is the target of a jump (goto) is a leader.
3. Any statement that comes right after a jump (goto) is a leader.

Once we find the leaders, each basic block consists of a leader and all statements up to (but not including) the next leader.

**Example:**
```
(1) prod = 0
(2) i = 1
(3) t1 = 4 * i
(4) t2 = a[t1]
...
(12) if i <= 20 goto (3)
```

Here:
- Statement 1 is a leader (first statement).
- Statement 3 is a leader (because statement 12 jumps to it).

So we get 2 basic blocks:
- **B1**: statements 1 to 2
- **B2**: statements 3 to 12

**Flow Graph:**
```
   [ B1 ]
      |
      v
   [ B2 ] <---+
      |       |
      +-------+     (loop back, because of the goto)
```

**Conclusion:**
Basic blocks group together statements with no internal jumps, and a flow graph shows how control moves between these blocks. This is the first and most important step before doing any code optimization.

---

## Q22. Explain DAG (Directed Acyclic Graph) for optimization.

**Answer:**

A **DAG (Directed Acyclic Graph)** is a special diagram used to represent the expressions inside one basic block. In a DAG, if the same calculation appears more than once, it is shown using only **one** node, instead of repeating it.

**Difference between a Syntax Tree and a DAG:**
A syntax tree will repeat a sub-expression every time it appears. A DAG will only create that sub-expression **once**, and reuse (share) the same node wherever it is needed again.

**How Building a DAG Helps in Optimization:**
1. It finds common (repeated) sub-expressions automatically. These repeated calculations can be removed, since they only need to be calculated once.
2. It shows which variables are actually used, helping to remove unused calculations (dead code).
3. It helps in reordering calculations for better performance.

**Example:**

Expression: `a + b + (a + b)`

Since `a + b` appears two times, but it means the exact same thing both times, a DAG will use just **one node** for it.

```
Normal Tree (repeats a+b twice):        DAG (shares a+b, only once):

         +                                     +
        / \                                   / \
       +   +                                 +   +
      /|   |\                               / \ (points back to same node)
     a b   a b                             a   b
```

Since both `+` nodes for `a+b` are the same in a DAG, the compiler knows it only has to calculate `a+b` one time, and can reuse the answer the second time.

**Conclusion:**
A DAG is a smart way to represent expressions, because it avoids repeating the same calculation. This directly helps in code optimization by removing repeated (redundant) work.

---

## Q23. Explain Machine Independent Code Optimization Techniques.

**Answer:**

**Machine Independent Code Optimization** means improving the intermediate code, without thinking about which computer or hardware the program will finally run on. These techniques can be used for any target machine.

**Common Machine Independent Techniques:**

**1. Common Sub-expression Elimination:**
If the same expression is calculated more than once, we calculate it only once, and reuse the answer.
Example: `t1 = a + b` and `t2 = a + b` becomes just `t1 = a + b`, and we use t1 wherever t2 was needed.

**2. Dead Code Elimination:**
If some code calculates a value that is never used anywhere later, we simply remove that code.

**3. Constant Folding:**
If an expression only uses fixed numbers (constants), we calculate the answer at compile time itself, instead of at run time.
Example: `x = 2 * 3` becomes simply `x = 6`.

**4. Algebraic Simplification:**
We use simple maths rules to simplify expressions.
Example: `x = x + 0` can be completely removed, since adding zero does not change anything. `x = x * 1` can also be removed.

**5. Loop Optimization:**
If some calculation inside a loop always gives the same answer every time (does not depend on the loop variable), we move it outside the loop. This is called code motion. This way, it is calculated only once, instead of every time the loop repeats.

**Conclusion:**
Machine Independent optimization techniques improve the intermediate code by removing repeated work, unused code, and unnecessary calculations. Since these techniques do not depend on any specific machine, they can be used for any target computer.

---

## Q24. Explain Machine Dependent Code Optimization.

**Answer:**

**Machine Dependent Code Optimization** means improving the final target code, based on the actual hardware/machine it will run on. These techniques are different for different computers, because every computer has different registers and instructions.

**Common Machine Dependent Techniques:**

**1. Register Allocation:**
Computers have a small number of very fast storage spots called **registers**. This technique decides which values should be kept in registers (instead of slow memory), to make the program run faster.

**2. Peephole Optimization:**
This technique looks at a very small group of instructions (like 2-3 lines) at a time, and tries to replace them with a shorter or faster version.
Example: `MOV R1, x` followed by `MOV x, R1` can be removed completely, since it does nothing useful.

**3. Instruction Scheduling:**
This technique changes the order of instructions, so that the computer's hardware can run them more efficiently (for example, using the CPU pipeline better), without changing the final result.

**4. Using Machine-Specific Instructions:**
Some computers have special, faster instructions for common jobs. This technique uses these special instructions instead of a longer, general instruction.
Example: using an `INC` instruction instead of writing `x = x + 1` using a normal add instruction.

**Difference between Machine Independent and Machine Dependent Optimization:**

| Feature | Machine Independent | Machine Dependent |
|---|---|---|
| Applied on | Intermediate code | Final target/machine code |
| Depends on hardware? | No | Yes |
| Example | Constant folding, dead code removal | Register allocation, peephole optimization |
| When it is applied | Before code generation | During or after code generation |

**Conclusion:**
Machine Dependent optimization improves the final code by using the special features of the actual target computer, like its registers and special instructions. This is done after (or during) code generation, and is different for every different type of computer.

---

## Q25. Explain the Issues in Designing the Code Generator.

**Answer:**

**Code Generation** is the last phase of a compiler. It changes the optimized intermediate code into the final machine code. When building this phase, a compiler designer must think carefully about a few important issues.

**Six Main Issues (Design Decisions):**

**1. Input:**
The code generator needs to know what kind of intermediate code it is getting (like three address code, or a DAG), along with the symbol table (which has variable details).

**2. Target Program:**
The designer must decide what kind of output to produce: ready-to-run machine code, code that needs linking (relocatable code), or assembly language code (which needs another step to become machine code).

**3. Memory Management:**
The code generator must decide where each variable will be stored in memory, using information from the symbol table.

**4. Instruction Selection:**
The code generator must choose the best machine instructions for each intermediate code statement. Choosing good instructions makes the final program faster and smaller.

**5. Register Allocation:**
Since computers have only a small number of fast registers, the code generator must decide which values are kept in registers at any given time, to reduce slow memory access.

**6. Order of Evaluation:**
The order in which calculations are done can change how many registers are needed, and how fast the program runs. So, choosing a good order is also important.

**Example:**
For the code:
```
x = b * c
y = a + x
```
A simple code generator (with all variables in memory) can produce:
```
MOV b, R0
MUL c, R0
MOV R0, x
MOV a, R1
ADD x, R1
MOV R1, y
```

**Conclusion:**
Designing a good code generator means carefully thinking about six main issues: input, target program form, memory management, instruction selection, register allocation, and order of evaluation. Good decisions in each of these areas lead to faster and smaller final programs.

---

*End of Theory Question & Answer Set — All 25 Questions Covered in Simple English (Units 1 to 5).*
