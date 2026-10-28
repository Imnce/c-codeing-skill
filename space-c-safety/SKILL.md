---
name: space-c-safety
description: Write, modify, and review safety-critical embedded C for space/flight software using GJB 5369-2005 (all 138 rules) combined with NASA/JPL rules (Power of Ten, JPL D-60411 LOC-1..4). Use when the user asks for aerospace/flight/space C, GJB 5369, NASA/JPL, or Power of Ten compliance, or invokes /space-c-safety. Do not apply automatically to ordinary C, C++, or Verilog/FPGA RTL.
---

# Space C Safety (GJB 5369-2005 + NASA/JPL)

## Scope

- Language: C only. GJB 8114-2013 and C++ rules are out of scope.
- A review request authorizes findings, not edits.
- Respond in the user's language; rule text here is English.

## Sources

| Key | Source | Classes |
|---|---|---|
| GJB | GJB 5369-2005 *Safe subset of C language for space armament software*, issued 2005-04-11, effective 2005-07-01. Derived from MISRA-C:1998 and LDRA MISRA C Checking (2000). | M = mandatory (强制), A = advisory (推荐) |
| P10 | G. J. Holzmann, *The Power of Ten: Rules for Developing Safety Critical Code*, NASA/JPL LaRS (IEEE Computer, June 2006). | all required |
| JPL | JPL Institutional Coding Standard for C, JPL DOCID D-60411 v1.0, 2009-03-03 (external version; LOC-5/6 MISRA-C:2004 text omitted). | shall / should |

GJB rule IDs below are the standard's clause numbers (e.g. 4.6.1.3). Physical scan page = printed page + 7.

## Combining the sources

1. Honor project tailoring and approved deviations first. Record each deviation with rule ID and justification.
2. Otherwise apply the stricter rule. Known overlaps where the stricter rule wins:
   - Function size: JPL 25 (≤60 lines, ≤6 params) over GJB 4.2.2.2 (≤200 lines) and 4.1.2.3 (≤20 params).
   - Infinite loops: GJB 4.11.2.1 says use cautiously; P10-2/JPL 3 allow one server loop per task, annotated `/* @non-terminating@ */`. All other loops need a statically provable bound.
   - `#undef`: JPL 22 forbids it; GJB 4.1.2.6 only advises against lone `#undef`.
   - Function pointers: GJB 4.4.1.3 and P10-9 forbid them; JPL 29 allows only constant ones. Default to forbidden.
   - Comments: GJB 4.10.2.2 advises against `//`; JPL 1 targets C99, where `//` is legal. Follow the project's C edition; prefer `/* */` when unspecified.
   - `#pragma`: JPL 1 forbids it as implementation-defined; GJB 4.1.2.7 says use cautiously.
3. Never invent rule numbers or attribute a rule to the wrong source. If a conclusion depends on text not covered here (GJB Appendix A naming rules, MISRA LOC-5/6), say so.

## Workflow

1. Establish C edition, compiler and flags, target widths/ABI, RTOS/task model, interrupt usage, and allocation policy from the code and build files. Ask only for facts that change the outcome.
2. Writing code: define input ranges, failure returns, ownership, and loop bounds before editing. Keep the existing ABI and unrelated behavior.
3. Review each changed file against all three sources: types and conversions, bounds, pointers, control flow, preprocessor, initialization, concurrency.
4. Report each finding as `file:line`, rule ID(s), M/A or shall/should, the concrete trigger, impact, and a specific fix. Keep mandatory violations, advisory departures, and engineering advice separate. Do not invent findings for clean code.
5. Verify: compile with all warnings at max (JPL 2, P10-10), e.g. `gcc -std=c99 -Wall -Wextra -pedantic -Wshadow -Wconversion -Wcast-qual -Wcast-align -Wstrict-prototypes -Wmissing-prototypes -Wpointer-arith`, plus any available static analyzer. Report exact commands and results. A clean build is not proof of compliance.

## NASA/JPL Power of Ten (P10)

| ID | Rule |
|---|---|
| P10-1 | Simple control flow only: no `goto`, `setjmp`/`longjmp`, or direct/indirect recursion. |
| P10-2 | Every loop has a fixed upper bound that a checking tool can prove statically. |
| P10-3 | No dynamic memory allocation after initialization. |
| P10-4 | A function fits on one printed page: about 60 lines, one statement or declaration per line. |
| P10-5 | Average at least two assertions per function. Assertions are side-effect-free Boolean tests, and a failure triggers an explicit recovery action (e.g. return an error). |
| P10-6 | Declare data objects at the smallest possible scope. |
| P10-7 | Callers check the return value of every non-void function; each function checks the validity of its parameters. |
| P10-8 | Preprocessor limited to header inclusion and simple macros. No token pasting, no variadic macros, no recursive macros. Macros expand to complete syntactic units. Keep conditional compilation to a minimum. |
| P10-9 | Restrict pointers: at most one level of dereference per expression; no dereferences hidden in macros or typedefs; no function pointers. |
| P10-10 | Compile from day one with all warnings at the most pedantic setting and zero warnings. Run at least one static analyzer daily, with zero warnings. |

## JPL D-60411 (LOC-1 to LOC-4)

| ID | LOC | Level | Rule |
|---|---|---|---|
| JPL 1 | 1 Language | shall | Conform to ISO C99 with no reliance on undefined or unspecified behavior. No `#pragma`; `#error` is allowed. |
| JPL 2 | 1 | shall | Compile with all warnings at the highest level, plus a static analyzer, with zero errors and zero warnings. Rewrite code that confuses the tools instead of suppressing the warning. |
| JPL 3 | 2 Predictable | shall | Every loop has a statically determinable iteration bound. The one exception is a single server loop per task, marked `/* @non-terminating@ */`. |
| JPL 4 | 2 | shall | No direct or indirect recursion. |
| JPL 5 | 2 | shall | No `malloc`, `sbrk`, `alloca`, or similar after task initialization. |
| JPL 6 | 2 | should/shall | Use IPC for task communication and avoid callbacks. A task does not run another task's code or touch its data. Each task receives IPC messages at a single point (shall). |
| JPL 7 | 2 | shall | Never synchronize tasks with task delays. |
| JPL 8 | 2 | should | Each shared data object has a single owning task, and only the owner writes it. Hand over ownership explicitly via IPC. |
| JPL 9 | 2 | should/shall | Avoid locks; if used, avoid nesting. Nested locks are taken in one documented order, and each unlock is in the same function as its lock (shall). |
| JPL 10 | 2 | shall | Use memory protection where available; otherwise use safety margins and barrier patterns, such as a stack guard fill. |
| JPL 11 | 2 | shall | No `goto`, `setjmp`, or `longjmp`. |
| JPL 12 | 2 | shall | In an enum, use `=` on the first member only, unless every member is explicitly initialized. |
| JPL 13 | 3 Defensive | shall | Declare data at the smallest scope; no inner declaration shadows an outer one. Put `extern` declarations in a header that the defining file also includes. Prefer `const`. |
| JPL 14 | 3 | shall | Check or use every non-void return value, or cast the call to `(void)` when the result is irrelevant. |
| JPL 15 | 3 | shall | Public functions check their parameters on entry. For other functions, either the caller or the callee checks. |
| JPL 16 | 3 | shall/should | Use assertions for sanity checks. Every function longer than 10 lines should have at least one. Assertions have no side effects, a failure triggers recovery, and none may be provably always true or always false. |
| JPL 17 | 3 | should | Use typedefs that carry size and signedness (e.g. `I32`, `U16`) in place of basic types. |
| JPL 18 | 3 | shall | Parenthesize compound expressions to make evaluation order explicit. |
| JPL 19 | 3 | shall | Boolean expressions have no side effects. |
| JPL 20 | 4 Clarity | shall | Preprocessor limited to file inclusion and simple macros. No `##`, no variadic macros, no recursive macros, and every macro expands to a complete syntactic unit. Use `#if` only for include guards unless justified in the code. |
| JPL 21 | 4 | shall | No `#define` inside a function or block. |
| JPL 22 | 4 | shall | No `#undef`. |
| JPL 23 | 4 | shall | `#else`, `#elif`, and `#endif` are in the same file as their `#if`. |
| JPL 24 | 4 | should | One statement or declaration per line; a `for` header may stay on one line. |
| JPL 25 | 4 | should | Functions are at most 60 lines with at most 6 parameters. |
| JPL 26 | 4 | should | A declaration has at most two levels of indirection. |
| JPL 27 | 4 | should | A statement has at most two levels of dereference per object. |
| JPL 28 | 4 | should | No dereferences hidden in macros or typedefs. |
| JPL 29 | 4 | should | No non-constant function pointers. |
| JPL 30 | 4 | shall | Convert a function pointer only to an integral type, never to any other type. |
| JPL 31 | 4 | shall | `#include` may be preceded only by other preprocessor directives or comments. |

LOC-5/6 (MISRA-C:2004 shall/should rules) are omitted from the public JPL text. Apply them only when a licensed MISRA copy is available.

## GJB 5369-2005 rules

GJB has 138 rules: 98 mandatory (M) and 40 advisory (A). "Procedure" (过程) means a function.

### 4.1 Declarations and definitions

| ID | Class | Rule |
|---|---|---|
| 4.1.1.1 | M | Do not reuse a function name for any other identifier. |
| 4.1.1.2 | M | Do not reuse a label name for another identifier. |
| 4.1.1.3 | M | No empty fields in a struct definition, such as a nested `struct {...};` that declares no member. |
| 4.1.1.4 | M | Do not put multiple labels on one statement (e.g. `start: begin:`). |
| 4.1.1.5 | M | Give every parameter an explicit type; no implicit-int parameters. |
| 4.1.1.6 | M | Declare parameters in function declarations; no `int f();` prototype for a function that takes parameters. |
| 4.1.1.7 | M | Every parameter has a name as well as a type, including in prototypes. |
| 4.1.1.8 | M | No ellipsis (`...`) in parameter lists. |
| 4.1.1.9 | M | Do not use C or C++ keywords as identifiers (e.g. `new`, `class`, `virtual`, `cout`). |
| 4.1.1.10 | M | Write an empty parameter list as `f(void)`, never `f()`. |
| 4.1.1.11 | M | A macro contains at most one `#` or `##` operator. |
| 4.1.1.12 | M | No function-like macro that is not function-like: its body must be a complete, parenthesized unit (no `#define IF_X(x) if(x) {`). |
| 4.1.1.13 | M | Use macros only for symbolic constants, function-like macros, type qualifiers, and storage-class specifiers. No statement or type keywords in a macro body. |
| 4.1.1.14 | M | Do not redefine reserved or standard names (e.g. `#define FILE ...`). |
| 4.1.1.15 | M | Declare `char` variables explicitly `signed` or `unsigned`. |
| 4.1.1.16 | M | Do not redefine one name in another context, e.g. a function and a struct tag with the same name. |
| 4.1.1.17 | M | Do not redefine a typedef name. |
| 4.1.1.18 | M | Every `#if` has a matching `#endif` in the same file. |
| 4.1.1.19 | M | Arrays have explicit bounds. |
| 4.1.1.20 | M | No absolute paths in `#include`. |
| 4.1.1.21 | M | Struct declarations must be complete. |
| 4.1.1.22 | M | Parameter declarations are consistent in form between declarations and the definition. |
| 4.1.2.1 | A | Typedef the basic types in one shared type-declaration header. |
| 4.1.2.2 | A | Avoid functions as parameters (function-pointer parameters). |
| 4.1.2.3 | A | At most 20 parameters per function (JPL 25 is stricter: 6). |
| 4.1.2.4 | A | Use bit-fields in structs cautiously. |
| 4.1.2.5 | A | Avoid a lone `#define` inside a block. |
| 4.1.2.6 | A | Avoid a lone `#undef` inside a block (JPL 22 forbids `#undef`). |
| 4.1.2.7 | A | Use `#pragma` cautiously (JPL 1 forbids it). |
| 4.1.2.8 | A | Use `union` declarations cautiously. |
| 4.1.2.9 | A | Use unnamed bit-fields in structs cautiously. |

### 4.2 Layout

| ID | Class | Rule |
|---|---|---|
| 4.2.1.1 | M | Enclose function bodies in braces. |
| 4.2.1.2 | M | Enclose loop bodies in braces. |
| 4.2.1.3 | M | Enclose then/else bodies in braces. |
| 4.2.1.4 | M | Parenthesize sub-expressions joined by logical operators: `(x < 0) \|\| ((z + y != 0) && !flag)`. |
| 4.2.1.5 | M | No executable code before `#include`; includes go at the top of the file. |
| 4.2.1.6 | M | Parenthesize every macro parameter in the macro body. |
| 4.2.1.7 | M | A function containing inline assembly contains only assembly. |
| 4.2.1.8 | M | No `'`, `\`, or `/*` characters in header file names. |
| 4.2.1.9 | M | No lone `\` line continuation inside string literals; strings are terminated with `\0`. |
| 4.2.1.10 | M | Define `main` as `int main(void)` or `int main(int, char *[])`. |
| 4.2.2.1 | A | At most 2000 lines per file. |
| 4.2.2.2 | A | At most 200 lines per function (JPL 25 is stricter: 60). |

### 4.3 Branch control

| ID | Class | Rule |
|---|---|---|
| 4.3.1.1 | M | The true branch of an `if` must have an executable statement: no `if (...);`, `{}`, or `{;}`. |
| 4.3.1.2 | M | An `if ... else if` chain ends with `else`. |
| 4.3.1.3 | M | An `else` branch must have an executable statement. |
| 4.3.1.4 | M | Every `switch` has `default`. |
| 4.3.1.5 | M | No empty `switch`. |
| 4.3.1.6 | M | No `switch` containing only `default`. |
| 4.3.1.7 | M | Every `case` ends with `break`. |
| 4.3.1.8 | M | No `case` without an executable statement (no shared fall-through labels). |

### 4.4 Pointers

| ID | Class | Rule |
|---|---|---|
| 4.4.1.1 | M | Do not assign to a pointer parameter (e.g. `p = &w;` inside the function). |
| 4.4.1.2 | M | At most two levels of pointer-to-pointer. |
| 4.4.1.3 | M | No function pointers (do not declare a procedure as a pointer type). |
| 4.4.2.1 | A | Use relational comparison (`<`, `>`) of pointers cautiously. |
| 4.4.2.2 | A | Use pointer arithmetic cautiously. |

### 4.5 Jumps

| ID | Class | Rule |
|---|---|---|
| 4.5.1.1 | M | Do not jump directly out of a function (`longjmp`). |
| 4.5.1.2 | M | No `goto`. |
| 4.5.2.1 | A | Avoid `setjmp`/`longjmp` (P10-1/JPL 11 forbid them). |

### 4.6 Operations

| ID | Class | Rule |
|---|---|---|
| 4.6.1.1 | M | No assignment operator in a non-assignment expression. |
| 4.6.1.2 | M | Array accesses never go out of bounds. |
| 4.6.1.3 | M | No shifts on signed types. |
| 4.6.1.4 | M | Shifts never overflow; the count is less than the operand width. |
| 4.6.1.5 | M | Never assign a negative value to an unsigned variable, including `y = -x`. |
| 4.6.1.6 | M | Signed bit-fields are at least 2 bits wide. |
| 4.6.1.7 | M | Bit-fields are `signed int` or `unsigned int` only (not `unsigned char`). |
| 4.6.1.8 | M | The assigned value's type matches the variable (no `unsigned d = 2.0;`; write `2u`). |
| 4.6.1.9 | M | Assignment types match; no implicit narrowing such as `float = double`. |
| 4.6.1.10 | M | Array subscripts and sizes are integers. |
| 4.6.1.11 | M | No logical NOT applied to a constant (`flag == !1`). |
| 4.6.1.12 | M | No bitwise operators on signed types. |
| 4.6.1.13 | M | No out-of-range enum values. |
| 4.6.1.14 | M | Variables never exceed their defined range. |
| 4.6.1.15 | M | No assignment operator inside a logical expression. |
| 4.6.1.16 | M | Do not combine assignment with `&&` or `\|\|`. |
| 4.6.1.17 | M | Bitwise operators take no Boolean operands. |
| 4.6.1.18 | M | Bitwise operators are not applied to Boolean values. |
| 4.6.2.1 | A | Avoid the comma operator. |
| 4.6.2.2 | A | Beware side effects in `sizeof` operands. |
| 4.6.2.3 | A | Use mixed-type arithmetic cautiously. |
| 4.6.2.4 | A | Avoid code that the design makes unreachable. |

### 4.7 Function calls

| ID | Class | Rule |
|---|---|---|
| 4.7.1.1 | M | The number of arguments matches the number of parameters. |
| 4.7.1.2 | M | The file containing `main` has no function that is not called from within that file; move such functions to the file that calls them. |
| 4.7.1.3 | M | Every `static` function is called within its file; otherwise remove it. |
| 4.7.1.4 | M | Do not use project-banned library functions, library files, or names. |
| 4.7.1.5 | M | No `extern` in files where the project forbids `extern`. |
| 4.7.1.6 | M | Do not call several related (state-sharing) functions in one expression, e.g. `exp_1(&y) + exp_2(&y)`. |
| 4.7.1.7 | M | Do not use a `void` function in an expression. |
| 4.7.1.8 | M | Do not pass `void`-typed variables (`void *`) as arguments. |
| 4.7.1.9 | M | Argument types match parameter types. |
| 4.7.1.10 | M | Function definition and prototype parameter types match. |
| 4.7.2.1 | A | Avoid unused parameters. |
| 4.7.2.2 | A | Avoid using a function other than by calling it (e.g. `if (f)`). |
| 4.7.2.3 | A | Use `abort`, `exit`, and similar cautiously. |

### 4.8 Statements

| ID | Class | Rule |
|---|---|---|
| 4.8.1.1 | M | Do not use `l` or `O` alone as a variable name. |
| 4.8.1.2 | M | No trigraphs (`??<` etc.). |
| 4.8.1.3 | M | Comment every octal constant. |
| 4.8.2.1 | A | Avoid `+=` and `-=`. |
| 4.8.2.2 | A | Use `++` and `--` cautiously. |
| 4.8.2.3 | A | Avoid `continue`. |
| 4.8.2.4 | A | Use the ternary `?:` cautiously. |
| 4.8.2.5 | A | Avoid statements with no effect. |
| 4.8.2.6 | A | Avoid empty statements. |
| 4.8.2.7 | A | Use `register` variables cautiously. |
| 4.8.2.8 | A | Avoid old-style (K&R) parameter definitions. |

### 4.9 Returns

| ID | Class | Rule |
|---|---|---|
| 4.9.1.1 | M | Every function has a `return` statement. |
| 4.9.1.2 | M | `return` in a `void` function carries no value. |
| 4.9.1.3 | M | `return` in a non-void function carries a value. |
| 4.9.1.4 | M | The returned value's type matches the function's return type. |
| 4.9.1.5 | M | Definition and prototype return types match. |

### 4.10 Comments

| ID | Class | Rule |
|---|---|---|
| 4.10.1.1 | M | No nested comments. |
| 4.10.2.1 | A | Avoid comments that add no explanation. |
| 4.10.2.2 | A | Do not use `//` line comments. |

### 4.11 Loops

| ID | Class | Rule |
|---|---|---|
| 4.11.1.1 | M | No unsuitable loop-variable types; use integers, not floating point. |
| 4.11.1.2 | M | Loop variables are local (no global `for` counters). |
| 4.11.2.1 | A | Use infinite loops (`for(;;)`, `while(1)`, `do...while(1)`) cautiously and check them carefully. |
| 4.11.2.2 | A | Avoid `break` in loops; loops have a single exit. |
| 4.11.2.3 | A | Use uncontrollable (constant) loop conditions cautiously, e.g. `while(0)` or `while(defval)`. |

### 4.12 Type conversion

| ID | Class | Rule |
|---|---|---|
| 4.12.1.1 | M | Do not cast a non-pointer value to a pointer in an assignment (`p = (unsigned int *)s;`). |
| 4.12.2.1 | A | When assigning another variable to a pointer, take its address with `&`. |
| 4.12.2.2 | A | Avoid unnecessary casts. |
| 4.12.2.3 | A | Check type agreement between both branches of `?:`. |

### 4.13 Initialization

| ID | Class | Rule |
|---|---|---|
| 4.13.1.1 | M | Initialize either all enum members or only the first. |
| 4.13.1.2 | M | Struct initializer types match the member types. |
| 4.13.1.3 | M | Struct initializer nesting matches the struct definition's braces. |
| 4.13.1.4 | M | Assign every variable before use on every path, including after conditional assignment. |

### 4.14 Comparisons

| ID | Class | Rule |
|---|---|---|
| 4.14.1.1 | M | No `==` or `!=` comparisons of floating-point values. |
| 4.14.1.2 | M | The condition of a logical test must be a logical expression. |
| 4.14.1.3 | M | A `switch` expression must not be a logical expression. |
| 4.14.2.1 | A | Write logical tests explicitly (`if (x != 0)`, not `if (x)`). |

### 4.15 Names, symbols, and variables

| ID | Class | Rule |
|---|---|---|
| 4.15.1.1 | M | An enum member name does not duplicate an existing variable name. |
| 4.15.1.2 | M | A local variable does not share a name with a global. |
| 4.15.1.3 | M | A parameter does not share a name with a global. |
| 4.15.1.4 | M | A parameter does not share a name with a type or other identifier. |
| 4.15.1.5 | M | An inner block does not redefine an existing variable name. |
| 4.15.1.6 | M | No `volatile` variables in complex expressions; read them into a local first. |
| 4.15.2.1 | A | Use characters outside ANSI C cautiously. |
| 4.15.2.2 | A | Use `##` and `#` in macros cautiously (JPL 20 forbids `##`). |

Appendix A (informative variable-naming guidelines) is not covered here.

## Source record

- GJB 5369-2005 scan: `C:\Users\NCE\Downloads\GJB 5369-2005 航天型号软件C语言安全子集.pdf`, 52 pages, SHA-256 `08d24e754dba1bc89359969af6673ab44e445e5a389bba5ff393cbf618bd1d8d`. It is an image-only scan carrying bzfxw.com watermarks, not an authenticated copy. Rules were taken from the table of contents and checked against body pages for the ambiguous ones. Where this paraphrase and the scan differ, the scan governs.
- P10: https://spinroot.com/gerard/pdf/P10.pdf
- JPL D-60411: https://yurichev.com/mirrors/C/JPL_Coding_Standard_C.pdf (external-distribution edition).
