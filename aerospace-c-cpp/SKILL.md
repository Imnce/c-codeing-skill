---
name: aerospace-c-cpp
description: Write, modify, and review C/C++ explicitly intended for aerospace software or subject to GJB coding requirements, using all 204 main-text-reviewed GJB 8114-2013 rules and reporting evidence gaps. Also use when explicitly invoked as $aerospace-c-cpp. Do not automatically apply to ordinary C/C++, Verilog/SystemVerilog, or FPGA RTL tasks.
---

# Aerospace C/C++ Coding

## Activation and scope

Use for explicitly aerospace C/C++ work, explicitly specified GJB coding requirements, or an explicit `$aerospace-c-cpp` invocation. Ordinary C/C++ and Verilog/SystemVerilog/FPGA RTL tasks do not activate this skill automatically. Follow the user's requested response language; otherwise follow the conversation language. Skill instructions and rule explanations are in English.

Support writing, modification, and review. A review request alone authorizes reporting findings, not editing code. This single file contains the complete 204-rule English organization of GJB 8114-2013, checked against the main text of the identified local scan, including required and advisory rules. It is a traceable working aid, not a complete conformity certification tool, an official translation, or an authenticated replacement for the standard.

## Standard selection and applicability

Honor the exact project-specified standard and edition, approved tailoring, and deviations. Do not silently substitute 8114-2013 for GJB 5369-2005 or another edition. If no version is specified, explain that the reviewed GJB 8114-2013 scan is the available reference baseline and establish its applicability to this project; do not label it the latest or currently authoritative edition.

The source's Chapter 1 applies to military safety-critical software written in C/C++; other military software may use it as a reference. It is not exclusively an aerospace standard. Chapters 2-4 reference GB/T 11457 (undated) and GJB/Z 102A-2012, define terms, and distinguish required R rules from advisory A rules. Chapter 5 is shared, but explicitly notes that some forms apply only to C because C++ already rejects them. Chapter 6 is C++ specific. R/A classification is separate from defect severity. Appendices A and B are informative.

GJB 5369-2005 full text, official current status of these standards, and their formal replacement relationship remain unverified and uncovered here. A newer publication date does not establish replacement. For conclusions depending on another edition or missing text, list the exact missing cover/version, scope, clause, notes, and exceptions; suspend only those standard-specific conclusions. Continue independently supported language-safety work with a separate label. Never invent a clause number or transfer an 8114 rule ID to another standard.

## Writing, modification, and review workflow

1. Read project instructions, relevant source, build files, and interfaces. Establish C or C++, language edition, compiler and options, target ABI, platform/RTOS, interrupt and concurrency model, allocation policy, ownership, and project-specific constraints from available evidence. Ask only for information that cannot be established and changes the outcome.
2. State the selected standard/version and tailoring. Identify applicable shared sections and, for C++, applicable dedicated sections. Read the full relevant entries below, including conditions and source discrepancies. For a full review, enumerate all applicable rules; a focused review must state excluded scope and pending checks.
3. For implementation, establish input ranges, output/failure contracts, resource ownership, timing constraints, and object lifetime before editing. Preserve authorized scope, language edition, ABI, and unrelated behavior. For review, report actionable issues without changing files unless fixes are requested. In Git repositories, inspect the worktree and commit each batch of task file changes without including unrelated work; never initialize a repository merely to satisfy that instruction.
4. Check types/conversions, bounds/pointers, initialization, control flow, macros, and resources. For C++, also inspect copying, inheritance, construction/destruction, virtual dispatch, qualifiers, exceptions, and templates. Check cross-file declarations and all relevant configurations where required. Use verified exceptions instead of generic blanket bans.
5. Separate tool diagnostics from manual findings. Corroborate tool output against code and rule applicability. Report each finding with file:line, concrete trigger, impact, standard/version, rule ID, clause, required/advisory classification, printed/PDF page, evidence, and a specific repair. Separate confirmed required-rule violations, advisory departures, engineering advice, approved deviations, and unresolved interpretations. Do not manufacture findings for clean code.
6. Run the available project-relevant checks after authorized fixes. Report exact commands and observed outcomes; distinguish compilation, execution, static analysis, manual review, and checks not run. Successful compilation is not full GJB compliance. Do not claim unexecuted tests passed. State remaining coverage and evidence limitations.

## How to read the rules

Each entry supplies an English paraphrase, review method, conditions/interpretation notes, and an original short counterexample and correction or a concrete scenario. Examples are focused fragments, not complete programs or demonstrations of compliance with every other rule. Surrounding declarations, headers, valid inputs, allocation checks, cleanup, and approved language syntax remain necessary. Intentionally violating examples may fail compilation and must not be executed when they invoke undefined behavior. Comments describing a scenario are not executable tests. Correcting one rule does not establish complete safety.

Source locators give printed pages and one-based physical PDF pages for the local scan; physical PDF page = printed page + 4. A range includes continuation examples. Clause numbers preserve the source's actual heading structure, including single-rule sections without another numbered subheading. Shared entries apply to C/C++ only where the construct exists in the selected language; notes identify C-specific or historical forms.

The per-entry requirement is the standard paraphrase. Additional language-safety checks and modern-version interpretations in review/notes are engineering guidance, not invented GJB clauses. In particular:

- A cast does not establish representability, pointer validity, alignment, aliasing, or lifetime. Validate ranges and interfaces separately.
- `volatile` is not an atomicity or synchronization mechanism. Preserve proper thread synchronization and document any necessary tailoring of legacy wording.
- Do not impose blanket bans on exceptions, RTTI, templates, STL, dynamic allocation, or multiple inheritance without a verified rule or project requirement. Do not enable runtime features without authorization.
- Resolve `nullptr`, `=default`, `=delete`, move semantics, `override`, smart pointers, modules, and modern containers against the selected edition and project interpretation. Do not automatically certify or reject a modern equivalent. Preserve RAII lifetimes rather than hoisting objects mechanically or deleting owned storage twice.
- Where main text and an example differ, the entry identifies the discrepancy. Retain the source locator and unresolved question in a finding; do not invent a stricter ban to hide ambiguity.

## Contents and verified inventory

| Rule family | Required | Advisory | Total |
|---|---:|---:|---:|
| Shared C/C++ (Chapter 5) | 124 | 41 | 165 |
| C++ specific (Chapter 6) | 28 | 11 | 39 |
| Total | 152 | 52 | 204 |

The inventory matches Appendix A, printed pp. 142-148 / PDF pp. 146-152; every entry was checked against the corresponding main-text rule, not only the index.

- [5.1 Declarations and definitions](#section-5-1)
- [5.2 Program layout](#section-5-2)
- [5.3 Pointers](#section-5-3)
- [5.4 Conditional branches](#section-5-4)
- [5.5 Jumps](#section-5-5)
- [5.6 Operations and bounds](#section-5-6)
- [5.7 Function calls and interfaces](#section-5-7)
- [5.8 Statements and literals](#section-5-8)
- [5.9 Loops](#section-5-9)
- [5.10 Type conversions](#section-5-10)
- [5.11 Initialization](#section-5-11)
- [5.12 Comparisons](#section-5-12)
- [5.13 Variable use and names](#section-5-13)
- [6.1 Classes and inheritance](#section-6-1)
- [6.2 Constructors](#section-6-2)
- [6.3 Destructors](#section-6-3)
- [6.4 Virtual functions](#section-6-4)
- [6.5 Type conversions](#section-6-5)
- [6.6 Memory release](#section-6-6)
- [6.7 Function definition and use](#section-6-7)
- [6.8 Exception handling](#section-6-8)
- [6.9 Other C++ provisions](#section-6-9)
- [Evaluation method](#evaluation-method)
- [Validation requirements](#validation-requirements)
- [Source record](#source-record)

<a id="section-5-1"></a>

## 5.1 Declarations and definitions

### R-1-1-1 - Preserve keyword meanings

**Required | C/C++ (where applicable) | GJB 8114-2013, clause 5.1.1.1 | Printed pp. 1 / PDF pp. 5.**

**Requirement:** Do not use macros to change keywords or basic-type meanings.

**Review:** Inspect macro names against language keywords.

**Conditions and notes:** Shared C/C++; a typedef is not keyword substitution.

**Violation fragment:**

```c
#define int short
```

**Correction fragment:**

```c
typedef short Sample;
```

### R-1-1-2 - Do not disguise keywords as macros

**Required | C/C++ (where applicable) | GJB 8114-2013, clause 5.1.1.2 | Printed pp. 2 / PDF pp. 6.**

**Requirement:** Do not define other identifiers as keywords or basic types through macros.

**Review:** Inspect replacement tokens, not just macro names.

**Conditions and notes:** Shared C/C++; distinguish a type alias from a macro alias.

**Violation fragment:**

```c
#define WORD unsigned int
```

**Correction fragment:**

```c
typedef unsigned int Word;
```

### R-1-1-3 - Preserve typedef names

**Required | C/C++ (where applicable) | GJB 8114-2013, clause 5.1.1.3 | Printed pp. 2 / PDF pp. 6.**

**Requirement:** Do not redefine an existing typedef name to mean another type.

**Review:** Check nested scopes and included declarations.

**Conditions and notes:** Shared C/C++; do not rely on legal shadowing to evade this rule.

**Violation fragment:**

```c
typedef int Count; void f(void) { typedef float Count; }
```

**Correction fragment:**

```c
typedef int Count; typedef float Ratio;
```

### R-1-1-4 - Preserve standard identifiers

**Required | C/C++ (where applicable) | GJB 8114-2013, clause 5.1.1.4 | Printed pp. 3 / PDF pp. 7.**

**Requirement:** Do not redefine C/C++ keywords; the source also treats standard identifiers such as FILE and cout as protected names.

**Review:** Compare declarations with language and library identifiers in scope.

**Conditions and notes:** Shared C/C++; the source's examples exceed the strict lexical definition of keyword. Preserve that distinction in findings.

**Violation fragment:**

```c
unsigned int FILE = 1U;
```

**Correction fragment:**

```c
unsigned int file_count = 1U;
```

### R-1-1-5 - Avoid repeated macro definitions

**Required | C/C++ (where applicable) | GJB 8114-2013, clause 5.1.1.5 | Printed pp. 3-4 / PDF pp. 7-8.**

**Requirement:** Do not redefine an active macro.

**Review:** Inspect all preprocessor configurations.

**Conditions and notes:** Shared C/C++; definitions in alternative conditional-compilation branches and redefinition after undef are explicit exceptions.

**Violation fragment:**

```c
#define LIMIT 4
#define LIMIT 8
```

**Correction fragment:**

```c
#define LIMIT 4
#undef LIMIT
#define LIMIT 8
```

### R-1-1-6 - Pair local macro directives

**Required | C/C++ (where applicable) | GJB 8114-2013, clause 5.1.1.6 | Printed pp. 4-6 / PDF pp. 8-10.**

**Requirement:** Pair define and undef inside the same function.

**Review:** Track preprocessor lifetime across function boundaries.

**Conditions and notes:** Shared C/C++; macros have preprocessor scope even when textually inside a function.

**Violation fragment:**

```c
void f(void) {
#define LOCAL 2
}
void g(void) {
#undef LOCAL
}
```

**Correction fragment:**

```c
void f(void) {
#define LOCAL 2
#undef LOCAL
}
```

### R-1-1-7 - Parenthesize function-like macros

**Required | C/C++ (where applicable) | GJB 8114-2013, clause 5.1.1.7 | Printed pp. 6 / PDF pp. 10.**

**Requirement:** Parenthesize macro arguments and the resulting expression.

**Review:** Expand calls inside larger expressions.

**Conditions and notes:** Shared C/C++; parentheses do not prevent repeated evaluation of side effects.

**Violation fragment:**

```c
#define TWICE(x) x + x
```

**Correction fragment:**

```c
#define TWICE(x) ((x) + (x))
```

### R-1-1-8 - Name aggregate tags

**Required | C/C++ (where applicable) | GJB 8114-2013, clause 5.1.1.8 | Printed pp. 6-7 / PDF pp. 10-11.**

**Requirement:** Provide identifying tags when defining structures, unions, and enumerations.

**Review:** Inspect aggregate definitions including typedef forms.

**Conditions and notes:** Shared C/C++; tag names and object names serve different purposes.

**Violation fragment:**

```c
struct { int value; } sample;
```

**Correction fragment:**

```c
struct Sample { int value; } sample;
```

### R-1-1-9 - Name nested structure members

**Required | C/C++ (where applicable) | GJB 8114-2013, clause 5.1.1.9 | Printed pp. 8 / PDF pp. 12.**

**Requirement:** Do not leave a nested structure without a member identifier.

**Review:** Inspect nested declarations for named accessible members.

**Conditions and notes:** Shared C/C++; the source's example has a nested tag but lacks a member name; do not reduce the check to missing tags alone.

**Violation fragment:**

```c
struct Outer { struct Inner { int x; }; };
```

**Correction fragment:**

```c
struct Outer { struct Inner { int x; } inner; };
```

### R-1-1-10 - Signed bit-field width

**Required | C/C++ (where applicable) | GJB 8114-2013, clause 5.1.1.10 | Printed pp. 8-9 / PDF pp. 12-13.**

**Requirement:** Signed integer bit-fields must have width greater than one.

**Review:** Check the declared width, including the sign bit.

**Conditions and notes:** Shared C/C++; do not misread the scanned threshold as greater than zero.

**Violation fragment:**

```c
struct Bits { signed int delta : 1; };
```

**Correction fragment:**

```c
struct Bits { signed int delta : 2; };
```

### R-1-1-11 - Explicit bit-field signedness

**Required | C/C++ (where applicable) | GJB 8114-2013, clause 5.1.1.11 | Printed pp. 9-10 / PDF pp. 13-14.**

**Requirement:** State signed or unsigned explicitly for integer bit-fields.

**Review:** Inspect underlying type declarations.

**Conditions and notes:** Shared C/C++; implementation-defined bit-field behavior still requires target validation.

**Violation fragment:**

```c
struct Bits { int mode : 2; };
```

**Correction fragment:**

```c
struct Bits { unsigned int mode : 2; };
```

### R-1-1-12 - Consistent bit-field storage

**Required | C/C++ (where applicable) | GJB 8114-2013, clause 5.1.1.12 | Printed pp. 10-11 / PDF pp. 14-15.**

**Requirement:** Use underlying bit-field types of equal length and do not let fields cross their underlying storage-unit length.

**Review:** Check target widths and cumulative field placement.

**Conditions and notes:** Shared C/C++; equal source spelling is insufficient if ABI packing differs; the original examples also constrain crossing storage boundaries.

**Violation fragment:**

```c
struct Bits { unsigned char a:2; unsigned short b:2; };
```

**Correction fragment:**

```c
struct Bits { unsigned short a:2; unsigned short b:2; };
```

### R-1-1-13 - Complete function declarations

**Required | C/C++ (where applicable) | GJB 8114-2013, clause 5.1.1.13 | Printed pp. 11-12 / PDF pp. 15-16.**

**Requirement:** Declare parameter types and parameter names in function declarations.

**Review:** Compare every public prototype with its definition.

**Conditions and notes:** Shared C/C++; unnamed parameters can be language-valid but violate this coding requirement.

**Violation fragment:**

```c
int scale(int);
```

**Correction fragment:**

```c
int scale(int value);
```

### R-1-1-14 - Consistent function interfaces

**Required | C/C++ (where applicable) | GJB 8114-2013, clause 5.1.1.14 | Printed pp. 12-14 / PDF pp. 16-18.**

**Requirement:** Keep declarations consistent with the function prototype/definition, including function type, parameter types, and parameter names.

**Review:** Compare declarations across translation units.

**Conditions and notes:** Shared C/C++; parameter names are explicitly part of the source's consistency note.

**Violation fragment:**

```c
int scale(int height); /* definition uses width */
```

**Correction fragment:**

```c
int scale(int width); /* definition also uses width */
```

### R-1-1-15 - Typed function parameters

**Required | C/C++ (where applicable) | GJB 8114-2013, clause 5.1.1.15 | Printed pp. 14-15 / PDF pp. 18-19.**

**Requirement:** Use explicit type declarations for function parameters.

**Review:** Reject implicit parameter types and obsolete definitions.

**Conditions and notes:** Shared; chiefly relevant to historical C; C++ rejects several such forms.

**Violation fragment:**

```c
int scale(value) { return value; }
```

**Correction fragment:**

```c
int scale(int value) { return value; }
```

### R-1-1-16 - Consistent extern types

**Required | C/C++ (where applicable) | GJB 8114-2013, clause 5.1.1.16 | Printed pp. 15 / PDF pp. 19.**

**Requirement:** Match an externally declared variable's type to its definition.

**Review:** Compare declarations and definitions across files.

**Conditions and notes:** Shared C/C++; successful linking does not prove matching types.

**Violation fragment:**

```c
extern short status; /* defined as int elsewhere */
```

**Correction fragment:**

```c
extern int status; /* defined as int elsewhere */
```

### R-1-1-17 - File-scope external declarations

**Required | C/C++ (where applicable) | GJB 8114-2013, clause 5.1.1.17 | Printed pp. 15-16 / PDF pp. 19-20.**

**Requirement:** Do not place external declarations inside function bodies.

**Review:** Inspect block-scope extern variable and function declarations.

**Conditions and notes:** Shared C/C++; prefer declarations in the owning header.

**Violation fragment:**

```c
void f(void) { extern int status; }
```

**Correction fragment:**

```c
extern int status; void f(void) { status = 1; }
```

### R-1-1-18 - Explicit array bounds

**Required | C/C++ (where applicable) | GJB 8114-2013, clause 5.1.1.18 | Printed pp. 16-17 / PDF pp. 20-21.**

**Requirement:** Specify explicit bounds in array definitions.

**Review:** Inspect inferred-size definitions.

**Conditions and notes:** Shared C/C++; this is stricter than the language's initializer-based size inference.

**Violation fragment:**

```c
int samples[] = {1, 2};
```

**Correction fragment:**

```c
int samples[2] = {1, 2};
```

### R-1-1-19 - Initialize the owning definition

**Required | C/C++ (where applicable) | GJB 8114-2013, clause 5.1.1.19 | Printed pp. 17 / PDF pp. 21.**

**Requirement:** Do not initialize a variable in an extern declaration.

**Review:** Separate the single initialized definition from consumers.

**Conditions and notes:** Shared C/C++; the rule's main text explicitly identifies extern.

**Violation fragment:**

```c
extern int status = 2;
```

**Correction fragment:**

```c
int status = 2; /* owner */
/* header: extern int status; */
```

### R-1-1-20 - Numeric character signedness

**Required | C/C++ (where applicable) | GJB 8114-2013, clause 5.1.1.20 | Printed pp. 17-18 / PDF pp. 21-22.**

**Requirement:** For char values used in arithmetic, explicitly state signed or unsigned.

**Review:** Trace arithmetic uses of plain char.

**Conditions and notes:** Shared C/C++; this does not prohibit ordinary textual char strings.

**Violation fragment:**

```c
char sample = 1; int next = sample + 1;
```

**Correction fragment:**

```c
unsigned char sample = 1U; int next = sample + 1;
```

### R-1-1-21 - Portable include paths

**Required | C/C++ (where applicable) | GJB 8114-2013, clause 5.1.1.21 | Printed pp. 18 / PDF pp. 22.**

**Requirement:** Do not use absolute paths in include directives.

**Review:** Inspect include tokens and build search paths.

**Conditions and notes:** Shared C/C++; configure include directories in the build.

**Violation fragment:**

```c
#include "C:/vendor/device.h"
```

**Correction fragment:**

```c
#include "vendor/device.h"
```

### R-1-1-22 - Prevent repeated header inclusion

**Required | C/C++ (where applicable) | GJB 8114-2013, clause 5.1.1.22 | Printed pp. 18-19 / PDF pp. 22-23.**

**Requirement:** Prevent a header's contents being processed repeatedly through direct or transitive includes.

**Review:** Trace the include graph and guard coverage.

**Conditions and notes:** Shared C/C++; use project-approved inclusion protection; do not confuse harmless guarded includes with duplicate definitions.

**Violation fragment:**

```c
/* device.h: unguarded struct definition */
```

**Correction fragment:**

```c
#ifndef DEVICE_H
#define DEVICE_H
struct Device { int id; };
#endif
```

### R-1-1-23 - Explicit empty parameter lists

**Required | C/C++ (where applicable) | GJB 8114-2013, clause 5.1.1.23 | Printed pp. 19-20 / PDF pp. 23-24.**

**Requirement:** Spell an empty parameter list as void.

**Review:** Check declarations and definitions separately.

**Conditions and notes:** Shared; empty parentheses have different historical C and C++ meanings, but the source prescribes explicit void.

**Violation fragment:**

```c
int reset();
```

**Correction fragment:**

```c
int reset(void);
```

### A-1-1-1 - Semantic type aliases

**Advisory | C/C++ (where applicable) | GJB 8114-2013, clause 5.1.2.1 | Printed pp. 20 / PDF pp. 24.**

**Requirement:** Prefer typedef aliases for basic variable types.

**Review:** Check that alias names match actual target representations.

**Conditions and notes:** Shared C/C++; advisory; a name containing 32 does not itself prove a 32-bit type.

**Discouraged fragment:**

```c
unsigned int tick_count;
```

**Preferred fragment:**

```c
typedef unsigned int TickCount; TickCount tick_count;
```

### A-1-1-2 - Balanced macro syntax

**Advisory | C/C++ (where applicable) | GJB 8114-2013, clause 5.1.2.2 | Printed pp. 20-21 / PDF pp. 24-25.**

**Requirement:** Avoid macros whose parentheses or braces are completed by the caller.

**Review:** Inspect each macro expansion in isolation.

**Conditions and notes:** Shared C/C++; advisory; caller must still brace the controlled body.

**Discouraged fragment:**

```c
#define IF_READY(x) if (x) {
```

**Preferred fragment:**

```c
#define IF_READY(x) if (x)
```

### A-1-1-3 - Cautious token manipulation

**Advisory | C/C++ (where applicable) | GJB 8114-2013, clause 5.1.2.3 | Printed pp. 21 / PDF pp. 25.**

**Requirement:** Use macro stringizing and token concatenation cautiously.

**Review:** Review expansions in all supported configurations.

**Conditions and notes:** Shared C/C++; advisory, not a blanket ban on # or ##.

**Discouraged fragment:**

```c
#define JOIN(a,b) a##b /* opaque generated names */
```

**Preferred fragment:**

```c
/* Prefer explicit named declarations when token generation is unnecessary. */
```

### A-1-1-4 - Group local declarations

**Advisory | C/C++ (where applicable) | GJB 8114-2013, clause 5.1.2.4 | Printed pp. 21 / PDF pp. 25.**

**Requirement:** Prefer declaring local variables together at the start of the function body.

**Review:** Review declaration placement without changing lifetime semantics.

**Conditions and notes:** Shared C/C++; advisory; modern C++ lifetime/RAII effects require deliberate tailoring rather than mechanical hoisting.

**Discouraged fragment:**

```c
void f(void) { work(); int count = 0; }
```

**Preferred fragment:**

```c
void f(void) { int count = 0; work(); }
```

### A-1-1-5 - Limit aggregate nesting

**Advisory | C/C++ (where applicable) | GJB 8114-2013, clause 5.1.2.5 | Printed pp. 21 / PDF pp. 25.**

**Requirement:** Prefer structure nesting no deeper than three levels.

**Review:** Measure nested aggregate definitions.

**Conditions and notes:** Shared C/C++; advisory; do not confuse nesting depth with number of fields.

**Discouraged fragment:**

```c
/* Four nested record levels. */
```

**Preferred fragment:**

```c
/* Flatten metadata into named records with at most three levels. */
```

### A-1-1-6 - Name constants

**Advisory | C/C++ (where applicable) | GJB 8114-2013, clause 5.1.2.6 | Printed pp. 21 / PDF pp. 25.**

**Requirement:** Prefer macros or const objects for constants.

**Review:** Inspect unexplained repeated literals.

**Conditions and notes:** Shared C/C++; advisory; choose a constant form supported by its language context.

**Discouraged fragment:**

```c
if (count > 12) { stop(); }
```

**Preferred fragment:**

```c
const int limit = 12; if (count > limit) { stop(); }
```

<a id="section-5-2"></a>

## 5.2 Program layout

### R-1-2-1 - Brace loop bodies

**Required | C/C++ (where applicable) | GJB 8114-2013, clause 5.2.1.1 | Printed pp. 21 / PDF pp. 25.**

**Requirement:** Enclose loop bodies in braces.

**Review:** Inspect for, while, and do bodies.

**Conditions and notes:** Shared C/C++; retain intentionally empty behavior with an explicit explanation.

**Violation fragment:**

```c
while (ready) poll();
```

**Correction fragment:**

```c
while (ready) { poll(); }
```

### R-1-2-2 - Brace conditional bodies

**Required | C/C++ (where applicable) | GJB 8114-2013, clause 5.2.1.2 | Printed pp. 22 / PDF pp. 26.**

**Requirement:** Enclose if, else-if, and else bodies in braces.

**Review:** Inspect every branch, including single statements.

**Conditions and notes:** Shared C/C++; an else-if chain remains permitted.

**Violation fragment:**

```c
if (ready) send(); else wait();
```

**Correction fragment:**

```c
if (ready) { send(); } else { wait(); }
```

### R-1-2-3 - Headers before executable code

**Required | C/C++ (where applicable) | GJB 8114-2013, clause 5.2.1.3 | Printed pp. 22-23 / PDF pp. 26-27.**

**Requirement:** Do not place header inclusion after executable code.

**Review:** Inspect includes inside functions and after statements.

**Conditions and notes:** Shared C/C++; do not infer that comments or harmless preprocessor guards are executable code.

**Violation fragment:**

```c
void f(void) { run();
#include "device.h"
}
```

**Correction fragment:**

```c
#include "device.h"
void f(void) { run(); }
```

### R-1-2-4 - Explicit logical precedence

**Required | C/C++ (where applicable) | GJB 8114-2013, clause 5.2.1.4 | Printed pp. 23-24 / PDF pp. 27-28.**

**Requirement:** Parenthesize mixed logical expressions whose precedence can be misunderstood.

**Review:** Inspect mixtures of &&, logical OR, and unary negation.

**Conditions and notes:** Shared C/C++; preserve intended grouping, not an arbitrary rewrite.

**Violation fragment:**

```c
if (a || b && c) { run(); }
```

**Correction fragment:**

```c
if (a || (b && c)) { run(); }
```

### R-1-2-5 - Group operands in conditions

**Required | C/C++ (where applicable) | GJB 8114-2013, clause 5.2.1.5 | Printed pp. 24-25 / PDF pp. 28-29.**

**Requirement:** Parenthesize expression operands inside logical tests.

**Review:** Inspect arithmetic/bitwise expressions combined with comparisons.

**Conditions and notes:** Shared C/C++; the original example addresses bitwise-and versus equality precedence.

**Violation fragment:**

```c
if (flags & MASK == MASK) { run(); }
```

**Correction fragment:**

```c
if ((flags & MASK) == MASK) { run(); }
```

### R-1-2-6 - No nested comments

**Required | C/C++ (where applicable) | GJB 8114-2013, clause 5.2.1.6 | Printed pp. 25 / PDF pp. 29.**

**Requirement:** Do not nest block comments.

**Review:** Inspect comment delimiters and disabled-code regions.

**Conditions and notes:** Shared C/C++; do not rely on compiler-specific nested-comment extensions.

**Violation fragment:**

```c
/* outer /* inner */ tail */
```

**Correction fragment:**

```c
/* outer */ /* separate comment */
```

### A-1-2-1 - File size

**Advisory | C/C++ (where applicable) | GJB 8114-2013, clause 5.2.2.1 | Printed pp. 25 / PDF pp. 29.**

**Requirement:** Prefer no more than 2000 statement lines per file.

**Review:** Count physical lines using the standard's definition, including comments and blanks.

**Conditions and notes:** Shared C/C++; advisory, not a compile-time error.

**Discouraged fragment:**

```c
/* One 2400-line source file. */
```

**Preferred fragment:**

```c
/* Split cohesive implementation units into files of at most 2000 lines. */
```

### A-1-2-2 - Function size

**Advisory | C/C++ (where applicable) | GJB 8114-2013, clause 5.2.2.2 | Printed pp. 25 / PDF pp. 29.**

**Requirement:** Prefer no more than 200 statement lines per function.

**Review:** Count physical lines within function extent.

**Conditions and notes:** Shared C/C++; advisory; preserve state and error-handling behavior when extracting helpers.

**Discouraged fragment:**

```c
/* A 300-line control function. */
```

**Preferred fragment:**

```c
/* Extract cohesive helpers and reduce the function to at most 200 lines. */
```

### A-1-2-3 - C comment portability

**Advisory | C/C++ (where applicable) | GJB 8114-2013, clause 5.2.2.3 | Printed pp. 25 / PDF pp. 29.**

**Requirement:** For C, prefer traditional block comments and use line comments cautiously.

**Review:** Check the project's C version and supported compilers.

**Conditions and notes:** C-specific advisory; this is not a blanket prohibition on C++ comments or C99 line comments.

**Discouraged fragment:**

```c
// comment in a C90-only build
```

**Preferred fragment:**

```c
/* portable C comment */
```

<a id="section-5-3"></a>

## 5.3 Pointers

### R-1-3-1 - Limit pointer indirection

**Required | C/C++ (where applicable) | GJB 8114-2013, clause 5.3.1.1 | Printed pp. 25-26 / PDF pp. 29-30.**

**Requirement:** Do not exceed two pointer-indirection levels.

**Review:** Expand typedefs before counting levels.

**Conditions and notes:** Shared C/C++; redesign interfaces rather than hiding depth in typedefs.

**Violation fragment:**

```c
int ***table;
```

**Correction fragment:**

```c
struct Table { int **rows; };
```

### R-1-3-2 - Explicit function addresses

**Required | C/C++ (where applicable) | GJB 8114-2013, clause 5.3.1.2 | Printed pp. 26-27 / PDF pp. 30-31.**

**Requirement:** Use & explicitly when taking or referring to a function's address.

**Review:** Inspect callback initializers and address comparisons.

**Conditions and notes:** Shared C/C++; ordinary function calls do not require &.

**Violation fragment:**

```c
int (*callback)(int) = handler;
```

**Correction fragment:**

```c
int (*callback)(int) = &handler;
```

### R-1-3-3 - Do not rebind pointer parameters

**Required | C/C++ (where applicable) | GJB 8114-2013, clause 5.3.1.3 | Printed pp. 27-28 / PDF pp. 31-32.**

**Requirement:** Do not assign a new address to a pointer parameter itself.

**Review:** Distinguish rebinding p from writing through *p.

**Conditions and notes:** Shared C/C++; the source explicitly permits a pointer-to-pointer output pattern; use an object with sufficient lifetime.

**Violation fragment:**

```c
void set(int *p) { p = &stored; }
```

**Correction fragment:**

```c
void set(int **out) { *out = &stored; }
```

### R-1-3-4 - No returning local addresses

**Required | C/C++ (where applicable) | GJB 8114-2013, clause 5.3.1.4 | Printed pp. 28 / PDF pp. 32.**

**Requirement:** Do not return addresses of automatic local objects.

**Review:** Trace returned pointers to object lifetime.

**Conditions and notes:** Shared C/C++; static, caller-owned, or allocated storage has different lifetime and ownership requirements.

**Violation fragment:**

```c
int *get(void) { int value = 1; return &value; }
```

**Correction fragment:**

```c
int get(void) { int value = 1; return value; }
```

### R-1-3-5 - Valid storage before use or release

**Required | C/C++ (where applicable) | GJB 8114-2013, clause 5.3.1.5 | Printed pp. 28-29 / PDF pp. 32-33.**

**Requirement:** Do not use invalid/unallocated storage or release storage twice.

**Review:** Trace allocation success, ownership, and release state on every path.

**Conditions and notes:** Shared C/C++; free(NULL) is language-defined as harmless; do not repeat the source example's overly broad invalid-pointer wording as a language claim.

**Violation fragment:**

```c
free(p); free(p);
```

**Correction fragment:**

```c
free(p); p = NULL; /* no second release */
```

### R-1-3-6 - Clear released pointers

**Required | C/C++ (where applicable) | GJB 8114-2013, clause 5.3.1.6 | Printed pp. 29-30 / PDF pp. 33-34.**

**Requirement:** Set pointer variables to NULL after releasing their storage.

**Review:** Inspect every release path and remaining aliases.

**Conditions and notes:** Shared C/C++; this does not repair dangling aliases or authorize release of non-owned memory.

**Violation fragment:**

```c
free(p);
```

**Correction fragment:**

```c
free(p); p = NULL;
```

### R-1-3-7 - Initialize deferred allocation pointers

**Required | C/C++ (where applicable) | GJB 8114-2013, clause 5.3.1.7 | Printed pp. 30-31 / PDF pp. 34-35.**

**Requirement:** Initialize a dynamic-allocation pointer to NULL when storage is not allocated at its declaration.

**Review:** Inspect declarations before the first assignment.

**Conditions and notes:** Shared C/C++; a declaration directly initialized from an allocator is a different case.

**Violation fragment:**

```c
int *buffer;
```

**Correction fragment:**

```c
int *buffer = NULL;
```

### R-1-3-8 - Check allocation results

**Required | C/C++ (where applicable) | GJB 8114-2013, clause 5.3.1.8 | Printed pp. 31-32 / PDF pp. 35-36.**

**Requirement:** Test a dynamically allocated pointer against NULL before its first use.

**Review:** Verify failure paths and dominance of the check.

**Conditions and notes:** Shared; for throwing C++ new, account for its actual allocation-failure mechanism rather than inventing NULL behavior.

**Violation fragment:**

```c
int *p = malloc(sizeof *p); *p = 3;
```

**Correction fragment:**

```c
int *p = malloc(sizeof *p); if (p != NULL) { *p = 3; }
```

### R-1-3-9 - Named null pointer

**Required | C/C++ (where applicable) | GJB 8114-2013, clause 5.3.1.9 | Printed pp. 32-33 / PDF pp. 36-37.**

**Requirement:** Use NULL rather than integer zero for null-pointer expressions.

**Review:** Inspect pointer initializers and comparisons.

**Conditions and notes:** Shared legacy rule; handle nullptr under explicit modern-C++ tailoring, without automatically certifying or rejecting it.

**Violation fragment:**

```c
int *p = 0;
```

**Correction fragment:**

```c
int *p = NULL;
```

### R-1-3-10 - Close owned files

**Required | C/C++ (where applicable) | GJB 8114-2013, clause 5.3.1.10 | Printed pp. 33-34 / PDF pp. 37-38.**

**Requirement:** Do not exit while leaving an owned file stream unclosed.

**Review:** Trace every successful open to close across normal/error exits.

**Conditions and notes:** Shared C/C++; do not close a borrowed stream or standard stream without ownership authority.

**Violation fragment:**

```c
FILE *f = fopen(path, "r"); if (f != NULL) { return 0; }
```

**Correction fragment:**

```c
FILE *f = fopen(path, "r"); if (f == NULL) { return -1; } fclose(f); return 0;
```

### A-1-3-1 - Cautious callbacks

**Advisory | C/C++ (where applicable) | GJB 8114-2013, clause 5.3.2.1 | Printed pp. 34 / PDF pp. 38.**

**Requirement:** Use function pointers cautiously.

**Review:** Review callback type, target lifetime, and allowed destinations.

**Conditions and notes:** Shared C/C++; advisory, not a ban on callbacks.

**Discouraged fragment:**

```c
/* An unchecked writable callback selected from external data. */
```

**Preferred fragment:**

```c
/* Validate the callback selection against a fixed supported table. */
```

### A-1-3-2 - Cautious untyped pointers

**Advisory | C/C++ (where applicable) | GJB 8114-2013, clause 5.3.2.2 | Printed pp. 34 / PDF pp. 38.**

**Requirement:** Use void pointers cautiously.

**Review:** Check type recovery, alignment, ownership, and extent.

**Conditions and notes:** Shared C/C++; advisory; generic allocator and ABI interfaces may need void pointers.

**Discouraged fragment:**

```c
void *payload; /* no type or size contract */
```

**Preferred fragment:**

```c
struct Payload { int value; }; /* typed interface where possible */
```

### A-1-3-3 - Cautious pointer arithmetic

**Advisory | C/C++ (where applicable) | GJB 8114-2013, clause 5.3.2.3 | Printed pp. 34 / PDF pp. 38.**

**Requirement:** Use pointer arithmetic cautiously.

**Review:** Prove the arithmetic remains within the same object or permitted one-past position.

**Conditions and notes:** Shared C/C++; advisory; array notation alone does not prove safety.

**Discouraged fragment:**

```c
p += untrusted_offset;
```

**Preferred fragment:**

```c
if (offset < count) { use(array[offset]); }
```

<a id="section-5-4"></a>

## 5.4 Conditional branches

### R-1-4-1 - Complete conditional chains

**Required | C/C++ (where applicable) | GJB 8114-2013, clause 5.4.1.1 | Printed pp. 34-35 / PDF pp. 38-39.**

**Requirement:** Provide a final else in an if/else-if chain.

**Review:** Inspect chain endings and defined fallback behavior.

**Conditions and notes:** Shared C/C++; this does not require else for every standalone if.

**Violation fragment:**

```c
if (mode == 1) { start(); } else if (mode == 2) { stop(); }
```

**Correction fragment:**

```c
if (mode == 1) { start(); } else if (mode == 2) { stop(); } else { reject(); }
```

### R-1-4-2 - Explain empty branches

**Required | C/C++ (where applicable) | GJB 8114-2013, clause 5.4.1.2 | Printed pp. 35-37 / PDF pp. 39-41.**

**Requirement:** Represent an intentionally empty conditional branch using a separate semicolon statement with the explanatory comment prescribed by the source.

**Review:** Inspect empty braces, bare semicolons, and comment-only branches.

**Conditions and notes:** Shared C/C++; the note explicitly uses /* no deal with */ and excludes this annotated semicolon from the empty-statement rule.

**Violation fragment:**

```c
if (ready) { }
```

**Correction fragment:**

```c
if (ready) {
    ; /* no deal with */
}
```

### R-1-4-3 - No empty switch

**Required | C/C++ (where applicable) | GJB 8114-2013, clause 5.4.1.3 | Printed pp. 37-38 / PDF pp. 41-42.**

**Requirement:** Do not use a switch with no branches.

**Review:** Inspect switch bodies.

**Conditions and notes:** Shared C/C++; retain any necessary selector evaluation explicitly when removing code.

**Violation fragment:**

```c
switch (mode) { }
```

**Correction fragment:**

```c
/* Remove the empty switch or implement the actual branches. */
```

### R-1-4-4 - No Boolean switch

**Required | C/C++ (where applicable) | GJB 8114-2013, clause 5.4.1.4 | Printed pp. 38 / PDF pp. 42.**

**Requirement:** Do not switch on a Boolean value or logical test.

**Review:** Inspect the selector's semantic type.

**Conditions and notes:** Shared C/C++; the original also covers comparison expressions in C.

**Violation fragment:**

```c
switch (ready) { case true: run(); break; default: break; }
```

**Correction fragment:**

```c
if (ready) { run(); } else { wait(); }
```

### R-1-4-5 - No default-only switch

**Required | C/C++ (where applicable) | GJB 8114-2013, clause 5.4.1.5 | Printed pp. 38 / PDF pp. 42.**

**Requirement:** Do not use a switch containing only default.

**Review:** Check that actual cases exist.

**Conditions and notes:** Shared C/C++; evaluate side effects before removing an unnecessary selector.

**Violation fragment:**

```c
switch (mode) { default: reset(); break; }
```

**Correction fragment:**

```c
reset(); /* preserve selector evaluation if it has required effects */
```

### R-1-4-6 - Switch coverage

**Required | C/C++ (where applicable) | GJB 8114-2013, clause 5.4.1.6 | Printed pp. 38-40 / PDF pp. 42-44.**

**Requirement:** Include default unless all enumerators of an enumeration selector are explicitly covered.

**Review:** Compare case labels with the enum definition and non-enum value range.

**Conditions and notes:** Shared C/C++; exhaustive enum coverage is an explicit exception, not a general waiver for integer selectors.

**Violation fragment:**

```c
switch (mode) { case 1: run(); break; }
```

**Correction fragment:**

```c
switch (mode) { case 1: run(); break; default: reject(); break; }
```

### R-1-4-7 - Terminate or explain shared cases

**Required | C/C++ (where applicable) | GJB 8114-2013, clause 5.4.1.7 | Printed pp. 40-42 / PDF pp. 44-46.**

**Requirement:** End case/default branches with break or return, and explicitly annotate shared cases.

**Review:** Inspect all branch paths, including nested breaks.

**Conditions and notes:** Shared C/C++; the prescribed shared-case comment is /* shared */. A break reachable only on one path does not terminate all paths.

**Violation fragment:**

```c
case 1: work(); case 2: stop(); break;
```

**Correction fragment:**

```c
case 1: /* shared */
case 2: stop(); break;
```

### R-1-4-8 - Same-level case labels

**Required | C/C++ (where applicable) | GJB 8114-2013, clause 5.4.1.8 | Printed pp. 42 / PDF pp. 46.**

**Requirement:** Keep all switch branches at the same scope level.

**Review:** Inspect labels nested inside if/loop blocks.

**Conditions and notes:** Shared C/C++; preserve actual dispatch behavior when restructuring.

**Violation fragment:**

```c
case 1: if (ready) { case 2: run(); break; }
```

**Correction fragment:**

```c
case 1: if (ready) { run(); } break;
case 2: run(); break;
```

### A-1-4-1 - Limit branch nesting

**Advisory | C/C++ (where applicable) | GJB 8114-2013, clause 5.4.2 | Printed pp. 42 / PDF pp. 46.**

**Requirement:** Avoid excessive conditional nesting; prefer at most seven levels.

**Review:** Measure nested branch depth.

**Conditions and notes:** Shared C/C++; advisory; do not convert this threshold into a required-rule violation.

**Discouraged fragment:**

```c
/* Eight nested conditionals. */
```

**Preferred fragment:**

```c
/* Extract cohesive decisions or use early exits while preserving behavior. */
```

<a id="section-5-5"></a>

## 5.5 Jumps

### R-1-5-1 - Restrict goto direction and scope

**Required | C/C++ (where applicable) | GJB 8114-2013, clause 5.5.1.1 | Printed pp. 42-43 / PDF pp. 46-47.**

**Requirement:** Do not jump into a compound statement from outside or jump upward using goto.

**Review:** Compare source/target positions and lexical scopes.

**Conditions and notes:** Shared C/C++; a forward jump out to cleanup is not universally prohibited by this required rule.

**Violation fragment:**

```c
again: poll(); if (busy) { goto again; }
```

**Correction fragment:**

```c
while (busy) { poll(); }
```

### R-1-5-2 - No nonlocal jumps

**Required | C/C++ (where applicable) | GJB 8114-2013, clause 5.5.1.2 | Printed pp. 43-44 / PDF pp. 47-48.**

**Requirement:** Do not use setjmp or longjmp.

**Review:** Inspect direct calls, wrappers, and macros.

**Conditions and notes:** Shared C/C++; do not silently introduce C++ exceptions where the project disables them.

**Violation fragment:**

```c
if (setjmp(env) != 0) { fail(); }
```

**Correction fragment:**

```c
/* Return an explicit status and handle it at the caller. */
```

### A-1-5-1 - Cautious goto

**Advisory | C/C++ (where applicable) | GJB 8114-2013, clause 5.5.2 | Printed pp. 44 / PDF pp. 48.**

**Requirement:** Use goto cautiously.

**Review:** Review structured alternatives and cleanup correctness.

**Conditions and notes:** Shared C/C++; advisory; do not misstate this as a blanket ban.

**Discouraged fragment:**

```c
/* Multiple forward jumps obscure ownership and cleanup. */
```

**Preferred fragment:**

```c
/* Prefer structured cleanup or a single justified forward cleanup path. */
```

<a id="section-5-6"></a>

## 5.6 Operations and bounds

### R-1-6-1 - No floating constants assigned to integers

**Required | C/C++ (where applicable) | GJB 8114-2013, clause 5.6.1.1 | Printed pp. 44 / PDF pp. 48.**

**Requirement:** Do not assign a floating-point constant to an integer variable.

**Review:** Inspect initializers and assignments.

**Conditions and notes:** Shared C/C++; choose the intended integer meaning instead of merely hiding the constant behind a cast.

**Violation fragment:**

```c
int retries = 2.5;
```

**Correction fragment:**

```c
int retries = 2;
```

### R-1-6-2 - Representable integer values

**Required | C/C++ (where applicable) | GJB 8114-2013, clause 5.6.1.2 | Printed pp. 44-45 / PDF pp. 48-49.**

**Requirement:** Do not assign an out-of-range integer value to an integer variable.

**Review:** Use actual target type limits.

**Conditions and notes:** Shared C/C++; check target widths rather than assuming all char types are eight bits.

**Violation fragment:**

```c
unsigned char code = 300; /* 8-bit char target */
```

**Correction fragment:**

```c
unsigned short code = 300;
```

### R-1-6-3 - No assignment in logical expressions

**Required | C/C++ (where applicable) | GJB 8114-2013, clause 5.6.1.3 | Printed pp. 45 / PDF pp. 49.**

**Requirement:** Do not use assignment expressions as logical conditions.

**Review:** Inspect conditions including nested expressions.

**Conditions and notes:** Shared C/C++; adding parentheses does not remove this rule violation.

**Violation fragment:**

```c
if (status = 1) { run(); }
```

**Correction fragment:**

```c
status = 1; if (status == 1) { run(); }
```

### R-1-6-4 - Logical rather than bitwise Boolean operations

**Required | C/C++ (where applicable) | GJB 8114-2013, clause 5.6.1.4 | Printed pp. 45-46 / PDF pp. 49-50.**

**Requirement:** Do not apply bitwise operators to logical expressions.

**Review:** Inspect bitwise combinations of comparisons.

**Conditions and notes:** Shared C/C++; changing to short-circuit evaluation requires checking side effects.

**Violation fragment:**

```c
if ((x == 1) & (y == 2)) { run(); }
```

**Correction fragment:**

```c
if ((x == 1) && (y == 2)) { run(); }
```

### R-1-6-5 - Separate increment side effects

**Required | C/C++ (where applicable) | GJB 8114-2013, clause 5.6.1.5 | Printed pp. 46-47 / PDF pp. 50-51.**

**Requirement:** Do not embed ++ or -- in arithmetic expressions or function-call arguments.

**Review:** Inspect both prefix and postfix forms.

**Conditions and notes:** Shared C/C++; standalone updates and ordinary loop updates are different cases.

**Violation fragment:**

```c
send(index++);
```

**Correction fragment:**

```c
send(index); index++;
```

### R-1-6-6 - Valid shift counts

**Required | C/C++ (where applicable) | GJB 8114-2013, clause 5.6.1.6 | Printed pp. 47 / PDF pp. 51.**

**Requirement:** Do not shift beyond the variable's length.

**Review:** Check effective operand width and every possible shift count.

**Conditions and notes:** Shared C/C++; engineering safety also excludes count equal to the promoted width; the source illustrates counts beyond width.

**Violation fragment:**

```c
value = 1U << 33; /* 32-bit unsigned target */
```

**Correction fragment:**

```c
value = 1U << 3;
```

### R-1-6-7 - Nonnegative shift counts

**Required | C/C++ (where applicable) | GJB 8114-2013, clause 5.6.1.7 | Printed pp. 47-48 / PDF pp. 51-52.**

**Requirement:** Do not use a negative shift count.

**Review:** Trace signed counts and converted external inputs.

**Conditions and notes:** Shared C/C++; masking or converting a negative count is not a substitute for input validation.

**Violation fragment:**

```c
value = value << -1;
```

**Correction fragment:**

```c
value = value << 1;
```

### R-1-6-8 - Array bounds

**Required | C/C++ (where applicable) | GJB 8114-2013, clause 5.6.1.8 | Printed pp. 48 / PDF pp. 52.**

**Requirement:** Do not access outside array bounds; range-check complicated indices when safety cannot be established.

**Review:** Check lower and upper bounds on every path.

**Conditions and notes:** Shared C/C++; length n permits indices 0 through n-1, not n.

**Violation fragment:**

```c
int a[4]; a[4] = 0;
```

**Correction fragment:**

```c
int a[4]; a[3] = 0;
```

### R-1-6-9 - Nonnegative integer indices

**Required | C/C++ (where applicable) | GJB 8114-2013, clause 5.6.1.9 | Printed pp. 49 / PDF pp. 53.**

**Requirement:** Use nonnegative integer array indices.

**Review:** Inspect signed index ranges before conversion.

**Conditions and notes:** Shared C/C++; upper bounds remain necessary even with an unsigned index.

**Violation fragment:**

```c
int a[3]; int i = -1; a[i] = 0;
```

**Correction fragment:**

```c
int a[3]; int i = 1; a[i] = 0;
```

### R-1-6-10 - No logical negation of constants

**Required | C/C++ (where applicable) | GJB 8114-2013, clause 5.6.1.10 | Printed pp. 49 / PDF pp. 53.**

**Requirement:** Do not apply logical negation directly to constant values.

**Review:** Look for ! immediately applied to literals or constant values.

**Conditions and notes:** Shared C/C++; distinguish logical ! from the inequality operator != and from bitwise complement.

**Violation fragment:**

```c
if (state == !1) { run(); }
```

**Correction fragment:**

```c
if (state != 1) { run(); }
```

### R-1-6-11 - Preserve enum typing

**Required | C/C++ (where applicable) | GJB 8114-2013, clause 5.6.1.11 | Printed pp. 49-50 / PDF pp. 53-54.**

**Requirement:** Do not use an enum value as the value of a non-enum variable.

**Review:** Track enum-to-integer assignments.

**Conditions and notes:** Shared C/C++; verify external serialization interfaces separately rather than silently changing ABI.

**Violation fragment:**

```c
unsigned int mode = ACTIVE;
```

**Correction fragment:**

```c
enum Mode mode = ACTIVE;
```

### R-1-6-12 - Nonzero divisors

**Required | C/C++ (where applicable) | GJB 8114-2013, clause 5.6.1.12 | Printed pp. 50 / PDF pp. 54.**

**Requirement:** Do not divide or take remainder by zero.

**Review:** Prove the denominator nonzero before evaluation.

**Conditions and notes:** Shared C/C++; define an appropriate floating-denominator policy from requirements, not an invented universal epsilon.

**Violation fragment:**

```c
result = count / divisor; /* divisor can be zero */
```

**Correction fragment:**

```c
if (divisor != 0) { result = count / divisor; } else { reject(); }
```

### R-1-6-13 - No assignment inside sizeof

**Required | C/C++ (where applicable) | GJB 8114-2013, clause 5.6.1.13 | Printed pp. 50-51 / PDF pp. 54-55.**

**Requirement:** Do not put assignment expressions inside sizeof.

**Review:** Inspect sizeof operands, including macro expansions.

**Conditions and notes:** Shared C/C++; account for C variable-length type evaluation separately.

**Violation fragment:**

```c
size_t size = sizeof(value = other);
```

**Correction fragment:**

```c
value = other; size_t size = sizeof(value);
```

### R-1-6-14 - Buffer read bounds

**Required | C/C++ (where applicable) | GJB 8114-2013, clause 5.6.1.14 | Printed pp. 51 / PDF pp. 55.**

**Requirement:** Keep buffer reads within source storage.

**Review:** Check byte counts against the source extent.

**Conditions and notes:** Shared C/C++; arrays here are schematic; initialize source data before copying it in a complete program.

**Violation fragment:**

```c
int src[2]; int dst[4]; memcpy(dst, src, sizeof dst);
```

**Correction fragment:**

```c
int src[2]; int dst[4]; memcpy(dst, src, sizeof src);
```

### R-1-6-15 - Buffer write bounds

**Required | C/C++ (where applicable) | GJB 8114-2013, clause 5.6.1.15 | Printed pp. 51 / PDF pp. 55.**

**Requirement:** Keep buffer writes within destination storage.

**Review:** Check both source size and destination capacity.

**Conditions and notes:** Shared C/C++; truncation is only acceptable when explicitly permitted by the interface.

**Violation fragment:**

```c
int src[4]; int dst[2]; memcpy(dst, src, sizeof src);
```

**Correction fragment:**

```c
int src[4]; int dst[2]; memcpy(dst, src, sizeof dst);
```

### R-1-6-16 - No use after release

**Required | C/C++ (where applicable) | GJB 8114-2013, clause 5.6.1.16 | Printed pp. 52 / PDF pp. 56.**

**Requirement:** Do not access released storage.

**Review:** Trace aliases and object lifetime, not just NULL assignments.

**Conditions and notes:** Shared C/C++; assumes valid owned storage and initialized content before the read.

**Violation fragment:**

```c
free(p); value = *p;
```

**Correction fragment:**

```c
value = *p; free(p); p = NULL;
```

### R-1-6-17 - Free allocation bases

**Required | C/C++ (where applicable) | GJB 8114-2013, clause 5.6.1.17 | Printed pp. 52-53 / PDF pp. 56-57.**

**Requirement:** Pass the original malloc/calloc allocation address to free.

**Review:** Track pointer offsets and ownership transfers.

**Conditions and notes:** Shared C allocation interfaces; apply the same ownership reasoning to other allocators under their own contracts.

**Violation fragment:**

```c
int *base = malloc(8 * sizeof *base); free(base + 1);
```

**Correction fragment:**

```c
int *base = malloc(8 * sizeof *base); free(base); base = NULL;
```

### R-1-6-18 - No gets

**Required | C/C++ (where applicable) | GJB 8114-2013, clause 5.6.1.18 | Printed pp. 53-54 / PDF pp. 57-58.**

**Requirement:** Do not use gets; use bounded fgets instead.

**Review:** Search wrappers and check the supplied capacity.

**Conditions and notes:** Shared C library use; manage newline/truncation policy explicitly.

**Violation fragment:**

```c
gets(line);
```

**Correction fragment:**

```c
if (fgets(line, sizeof line, stdin) == NULL) { reject(); }
```

### R-1-6-19 - String destination capacity

**Required | C/C++ (where applicable) | GJB 8114-2013, clause 5.6.1.19 | Printed pp. 54-55 / PDF pp. 58-59.**

**Requirement:** Do not overflow destination storage in string assignment/copy/append operations.

**Review:** Include existing prefix length and the final NUL in capacity calculations.

**Conditions and notes:** Shared C/C++; safe use for this rule does not erase advisory preferences for bounded functions.

**Violation fragment:**

```c
char dst[3]; strcpy(dst, "abcd");
```

**Correction fragment:**

```c
char dst[5]; strcpy(dst, "abcd");
```

### A-1-6-1 - Cautious signed bit operations

**Advisory | C/C++ (where applicable) | GJB 8114-2013, clause 5.6.2.1 | Printed pp. 55 / PDF pp. 59.**

**Requirement:** Use bitwise operations on signed integers cautiously.

**Review:** Inspect promotions, sign propagation, and target representation.

**Conditions and notes:** Shared C/C++; advisory, not a ban on every signed bit operation.

**Discouraged fragment:**

```c
int flags = -1; flags >>= 1;
```

**Preferred fragment:**

```c
unsigned int flags = 1U; flags >>= 1;
```

### A-1-6-2 - Cautious integer division

**Advisory | C/C++ (where applicable) | GJB 8114-2013, clause 5.6.2.2 | Printed pp. 55 / PDF pp. 59.**

**Requirement:** Use division of integer quantities/variables cautiously.

**Review:** Check truncation, range, and zero-denominator assumptions.

**Conditions and notes:** Shared C/C++; advisory; the source wording concerns integer division, not prohibition of normal / operations.

**Discouraged fragment:**

```c
double ratio = 3 / 2;
```

**Preferred fragment:**

```c
double ratio = 3.0 / 2.0;
```

### A-1-6-3 - Prompt dynamic-storage release

**Advisory | C/C++ (where applicable) | GJB 8114-2013, clause 5.6.2.3 | Printed pp. 55 / PDF pp. 59.**

**Requirement:** Release dynamically allocated storage promptly when no longer needed.

**Review:** Inspect all success/failure paths and ownership transfers.

**Conditions and notes:** Shared C/C++; advisory; borrowed storage must not be released by the borrower.

**Discouraged fragment:**

```c
/* Buffer remains allocated after its last use. */
```

**Preferred fragment:**

```c
/* Release at the end of the owning lifetime, or use approved RAII. */
```

### A-1-6-4 - Prefer bounded copy

**Advisory | C/C++ (where applicable) | GJB 8114-2013, clause 5.6.2.4 | Printed pp. 55 / PDF pp. 59.**

**Requirement:** Avoid strcpy and prefer strncpy.

**Review:** Check source length, destination capacity, and explicit termination.

**Conditions and notes:** Shared C/C++; advisory; example assumes a real nonempty array and an approved truncation policy, not a decayed pointer.

**Discouraged fragment:**

```c
strcpy(dst, src); /* unbounded source */
```

**Preferred fragment:**

```c
strncpy(dst, src, sizeof dst - 1); dst[sizeof dst - 1] = '\0';
```

### A-1-6-5 - Prefer bounded append

**Advisory | C/C++ (where applicable) | GJB 8114-2013, clause 5.6.2.5 | Printed pp. 55 / PDF pp. 59.**

**Requirement:** Avoid strcat and prefer strncat.

**Review:** Calculate remaining capacity excluding the terminating NUL.

**Conditions and notes:** Shared C/C++; advisory; first prove dst is terminated and used is less than its real nonzero capacity.

**Discouraged fragment:**

```c
strcat(dst, src); /* unchecked capacity */
```

**Preferred fragment:**

```c
size_t used = strlen(dst); strncat(dst, src, sizeof dst - used - 1);
```

### A-1-6-6 - Cautious comma expressions

**Advisory | C/C++ (where applicable) | GJB 8114-2013, clause 5.6.2.6 | Printed pp. 55 / PDF pp. 59.**

**Requirement:** Use the comma operator cautiously.

**Review:** Distinguish sequencing expressions from declarator and argument separators.

**Conditions and notes:** Shared C/C++; advisory; preserve sequencing and result value.

**Discouraged fragment:**

```c
result = (left = 1, right = 2);
```

**Preferred fragment:**

```c
left = 1; right = 2; result = right;
```

<a id="section-5-7"></a>

## 5.7 Function calls and interfaces

### R-1-7-1 - Preserve library functions

**Required | C/C++ (where applicable) | GJB 8114-2013, clause 5.7.1.1 | Printed pp. 55-56 / PDF pp. 59-60.**

**Requirement:** Do not replace or override standard-library functions with application implementations.

**Review:** Check names, linkage, and symbol exports.

**Conditions and notes:** Shared C/C++; do not confuse an unrelated class member with replacement of a standard symbol.

**Violation fragment:**

```c
int printf(int value) { return value; }
```

**Correction fragment:**

```c
int report_value(int value) { return value; }
```

### R-1-7-2 - Match argument types

**Required | C/C++ (where applicable) | GJB 8114-2013, clause 5.7.1.2 | Printed pp. 56-57 / PDF pp. 60-61.**

**Requirement:** Actual arguments must match formal parameter types.

**Review:** Resolve the called overload/prototype and implicit conversions.

**Conditions and notes:** Shared C/C++; the source expressly excludes C++ base-class parameters accepting derived-class arguments. Explicit narrowing still needs range validation.

**Violation fragment:**

```c
void send(short value); int value = 1; send(value);
```

**Correction fragment:**

```c
void send(short value); short value = 1; send(value);
```

### R-1-7-3 - Match argument counts

**Required | C/C++ (where applicable) | GJB 8114-2013, clause 5.7.1.3 | Printed pp. 57 / PDF pp. 61.**

**Requirement:** Keep actual and formal argument counts consistent.

**Review:** Inspect resolved call signatures.

**Conditions and notes:** Shared; account for project-approved C++ default arguments rather than inventing an arity defect.

**Violation fragment:**

```c
int add(int left, int right); add(1, 2, 3);
```

**Correction fragment:**

```c
int add(int left, int right); add(1, 2);
```

### R-1-7-4 - No old-style definitions

**Required | C/C++ (where applicable) | GJB 8114-2013, clause 5.7.1.4 | Printed pp. 57-58 / PDF pp. 61-62.**

**Requirement:** Do not use K&R-style function parameter definitions.

**Review:** Inspect parameter declarations between the declarator and body.

**Conditions and notes:** Shared; historical C pattern, rejected by C++.

**Violation fragment:**

```c
int identity(value) int value; { return value; }
```

**Correction fragment:**

```c
int identity(int value) { return value; }
```

### R-1-7-5 - Consistent parameter types

**Required | C/C++ (where applicable) | GJB 8114-2013, clause 5.7.1.5 | Printed pp. 58 / PDF pp. 62.**

**Requirement:** Match parameter types between declarations and definitions.

**Review:** Compare every prototype with its implementation.

**Conditions and notes:** Shared C/C++; cross-file checks may be needed.

**Violation fragment:**

```c
int f(float value); /* definition: int f(int value) */
```

**Correction fragment:**

```c
int f(int value); /* definition: int f(int value) */
```

### R-1-7-6 - Consistent return declarations

**Required | C/C++ (where applicable) | GJB 8114-2013, clause 5.7.1.6 | Printed pp. 58-59 / PDF pp. 62-63.**

**Requirement:** Match return types between declarations and definitions.

**Review:** Compare all visible signatures.

**Conditions and notes:** Shared C/C++; linker acceptance is not evidence of type consistency.

**Violation fragment:**

```c
unsigned int read_status(void); /* definition returns int */
```

**Correction fragment:**

```c
int read_status(void); /* definition also returns int */
```

### R-1-7-7 - Return on value-producing paths

**Required | C/C++ (where applicable) | GJB 8114-2013, clause 5.7.1.7 | Printed pp. 59-60 / PDF pp. 63-64.**

**Requirement:** Functions with a result must return through return statements.

**Review:** Inspect all reachable exits.

**Conditions and notes:** Shared C/C++; do not add meaningless success returns to paths that should signal failure.

**Violation fragment:**

```c
int choose(int mode) { if (mode == 0) { return 1; } }
```

**Correction fragment:**

```c
int choose(int mode) { if (mode == 0) { return 1; } else { return 0; } }
```

### R-1-7-8 - Void returns have no value

**Required | C/C++ (where applicable) | GJB 8114-2013, clause 5.7.1.8 | Printed pp. 60 / PDF pp. 64.**

**Requirement:** Do not return a value from a void function.

**Review:** Inspect return expressions.

**Conditions and notes:** Shared C/C++; distinguish returning a void expression where the language permits it from this legacy coding requirement.

**Violation fragment:**

```c
void reset(void) { return 1; }
```

**Correction fragment:**

```c
void reset(void) { return; }
```

### R-1-7-9 - Nonvoid returns carry values

**Required | C/C++ (where applicable) | GJB 8114-2013, clause 5.7.1.9 | Printed pp. 60-61 / PDF pp. 64-65.**

**Requirement:** A return statement in a nonvoid function must carry its result.

**Review:** Inspect bare returns.

**Conditions and notes:** Shared C/C++; separate from missing returns at the end of a path.

**Violation fragment:**

```c
int status(void) { return; }
```

**Correction fragment:**

```c
int status(void) { return 0; }
```

### R-1-7-10 - Match returned value types

**Required | C/C++ (where applicable) | GJB 8114-2013, clause 5.7.1.10 | Printed pp. 61 / PDF pp. 65.**

**Requirement:** Match the returned expression's type to the function's declared return type.

**Review:** Inspect implicit result conversions and range.

**Conditions and notes:** Shared C/C++; interface changes require authorization; otherwise use the specified error representation.

**Violation fragment:**

```c
unsigned int status(void) { return -1; }
```

**Correction fragment:**

```c
int status(void) { return -1; }
```

### R-1-7-11 - Mark intentionally discarded results

**Required | C/C++ (where applicable) | GJB 8114-2013, clause 5.7.1.11 | Printed pp. 61-63 / PDF pp. 65-67.**

**Requirement:** If a value-returning function's result is intentionally unused, explicitly cast the call to void.

**Review:** Inspect unused return values.

**Conditions and notes:** Shared C/C++; acknowledging discard does not justify ignoring an error that requirements demand handling.

**Violation fragment:**

```c
read_status();
```

**Correction fragment:**

```c
(void)read_status();
```

### R-1-7-12 - Do not cast void calls again

**Required | C/C++ (where applicable) | GJB 8114-2013, clause 5.7.1.12 | Printed pp. 63 / PDF pp. 67.**

**Requirement:** Do not add a redundant void cast to a call already returning void.

**Review:** Resolve the actual return type.

**Conditions and notes:** Shared C/C++; do not mechanically add void casts to every call.

**Violation fragment:**

```c
(void)reset(); /* reset returns void */
```

**Correction fragment:**

```c
reset();
```

### R-1-7-13 - Use static functions

**Required | C/C++ (where applicable) | GJB 8114-2013, clause 5.7.1.13 | Printed pp. 63-64 / PDF pp. 67-68.**

**Requirement:** A static function must be used.

**Review:** Check references including valid callback registrations.

**Conditions and notes:** Shared C/C++; do not create dummy calls solely to silence the rule.

**Violation fragment:**

```c
static int unused(void) { return 0; }
```

**Correction fragment:**

```c
/* Remove an unused helper, or call it for a real required purpose. */
```

### R-1-7-14 - Sequence dependent calls

**Required | C/C++ (where applicable) | GJB 8114-2013, clause 5.7.1.14 | Printed pp. 64-65 / PDF pp. 68-69.**

**Requirement:** Do not call multiple order-dependent functions in one expression.

**Review:** Analyze shared state and unspecified evaluation order.

**Conditions and notes:** Shared C/C++; independent pure calls are not automatically order-dependent.

**Violation fragment:**

```c
int result = advance() + read_current();
```

**Correction fragment:**

```c
int next = advance(); int current = read_current(); int result = next + current;
```

### R-1-7-15 - No ellipsis parameter lists

**Required | C/C++ (where applicable) | GJB 8114-2013, clause 5.7.1.15 | Printed pp. 65 / PDF pp. 69.**

**Requirement:** Do not use ellipsis in function parameter declarations/definitions.

**Review:** Inspect user-defined variadic interfaces.

**Conditions and notes:** Shared C/C++; do not claim this clause verifies all format-string calls or automatically bans parameter packs without version analysis.

**Violation fragment:**

```c
int log_event(int code, ...);
```

**Correction fragment:**

```c
int log_event(int code, const struct Event *event);
```

### R-1-7-16 - No recursion

**Required | C/C++ (where applicable) | GJB 8114-2013, clause 5.7.1.16 | Printed pp. 65 / PDF pp. 69.**

**Requirement:** Do not use direct or indirect self-calling functions.

**Review:** Inspect the call graph, including callbacks.

**Conditions and notes:** Shared C/C++; loops need a justified termination/resource bound.

**Violation fragment:**

```c
int depth(int n) { return n ? depth(n - 1) : 0; }
```

**Correction fragment:**

```c
/* Use a bounded iterative implementation with explicit state. */
```

### A-1-7-1 - Limit parameter counts

**Advisory | C/C++ (where applicable) | GJB 8114-2013, clause 5.7.2.1 | Printed pp. 65 / PDF pp. 69.**

**Requirement:** Avoid excessive parameters; prefer no more than ten.

**Review:** Count formal parameters and assess cohesion.

**Conditions and notes:** Shared C/C++; advisory; do not merely hide an incoherent interface in a bag of pointers.

**Discouraged fragment:**

```c
/* An interface with eleven scalar arguments. */
```

**Preferred fragment:**

```c
/* Group cohesive data in an explicitly defined request object. */
```

### A-1-7-2 - Use parameters meaningfully

**Advisory | C/C++ (where applicable) | GJB 8114-2013, clause 5.7.2.2 | Printed pp. 65 / PDF pp. 69.**

**Requirement:** Avoid unused function parameters.

**Review:** Trace actual reads and required ABI constraints.

**Conditions and notes:** Shared C/C++; advisory; fixed callback/ABI signatures may require documented unused parameters.

**Discouraged fragment:**

```c
int f(int value, int ignored) { return value; }
```

**Preferred fragment:**

```c
int f(int value) { return value; }
```

### A-1-7-3 - Cautious process termination

**Advisory | C/C++ (where applicable) | GJB 8114-2013, clause 5.7.2.3 | Printed pp. 65 / PDF pp. 69.**

**Requirement:** Use abort and exit cautiously.

**Review:** Inspect cleanup, watchdog behavior, and system-level failure policy.

**Conditions and notes:** Shared C/C++; advisory; safety requirements may explicitly prescribe termination.

**Discouraged fragment:**

```c
if (bad) { exit(1); }
```

**Preferred fragment:**

```c
if (bad) { return ERROR_STATUS; }
```

### A-1-7-4 - Validate system-call results

**Advisory | C/C++ (where applicable) | GJB 8114-2013, clause 5.7.2.4 | Printed pp. 66 / PDF pp. 70.**

**Requirement:** Check validity of system-function return status after calls.

**Review:** Inspect each error-reporting contract.

**Conditions and notes:** Shared C/C++; advisory; choose the actual API's failure indicator.

**Discouraged fragment:**

```c
fclose(stream); /* error ignored */
```

**Preferred fragment:**

```c
if (fclose(stream) != 0) { report_close_error(); }
```

### A-1-7-5 - Pass array lengths

**Advisory | C/C++ (where applicable) | GJB 8114-2013, clause 5.7.2.5 | Printed pp. 66-67 / PDF pp. 70-71.**

**Requirement:** When passing arrays as pointers, also pass their lengths.

**Review:** Check units and correspondence between pointer and size.

**Conditions and notes:** Shared C/C++; advisory; sizeof on a pointer cannot recover array length.

**Discouraged fragment:**

```c
void clear(int *items);
```

**Preferred fragment:**

```c
void clear(int *items, size_t count);
```

<a id="section-5-8"></a>

## 5.8 Statements and literals

### R-1-8-1 - No unreachable statements

**Required | C/C++ (where applicable) | GJB 8114-2013, clause 5.8.1.1 | Printed pp. 67 / PDF pp. 71.**

**Requirement:** Do not leave unreachable statements.

**Review:** Inspect control flow after unconditional transfers and before switch labels.

**Conditions and notes:** Shared C/C++; do not move side effects merely to make them reachable without checking intended behavior.

**Violation fragment:**

```c
return 0; log_done();
```

**Correction fragment:**

```c
log_done(); return 0;
```

### R-1-8-2 - No unreachable branches

**Required | C/C++ (where applicable) | GJB 8114-2013, clause 5.8.1.2 | Printed pp. 67-68 / PDF pp. 71-72.**

**Requirement:** Do not retain branches that cannot be reached.

**Review:** Prove branch feasibility using types and ranges.

**Conditions and notes:** Shared C/C++; conditional compilation and documented configurations must be evaluated explicitly.

**Violation fragment:**

```c
unsigned int n = 1U; if (n < 0U) { reject(); }
```

**Correction fragment:**

```c
/* Remove the impossible test or use the correct signed domain. */
```

### R-1-8-3 - No ineffective statements

**Required | C/C++ (where applicable) | GJB 8114-2013, clause 5.8.1.3 | Printed pp. 68 / PDF pp. 72.**

**Requirement:** Do not use statements with no useful effect.

**Review:** Distinguish intended comparisons from missing assignments.

**Conditions and notes:** Shared C/C++; a deliberate result discard must still have a meaningful operation.

**Violation fragment:**

```c
count == limit;
```

**Correction fragment:**

```c
count = limit; /* only if assignment is intended */
```

### R-1-8-4 - Annotate octal literals

**Required | C/C++ (where applicable) | GJB 8114-2013, clause 5.8.1.4 | Printed pp. 68-69 / PDF pp. 72-73.**

**Requirement:** Explicitly annotate octal constants.

**Review:** Inspect leading-zero numeric literals.

**Conditions and notes:** Shared C/C++; the prescribed annotation is /* octal */; use decimal/hex instead when that is the actual intent.

**Violation fragment:**

```c
int mask = 077;
```

**Correction fragment:**

```c
int mask = 077; /* octal */
```

### R-1-8-5 - Uppercase numeric suffixes

**Required | C/C++ (where applicable) | GJB 8114-2013, clause 5.8.1.5 | Printed pp. 69 / PDF pp. 73.**

**Requirement:** Use uppercase letters in numeric type suffixes.

**Review:** Inspect U, L, F and combinations.

**Conditions and notes:** Shared C/C++; do not confuse suffix letters with hexadecimal digits or change a literal's type accidentally.

**Violation fragment:**

```c
unsigned int count = 1u;
```

**Correction fragment:**

```c
unsigned int count = 1U;
```

### A-1-8-1 - Avoid empty statements

**Advisory | C/C++ (where applicable) | GJB 8114-2013, clause 5.8.2.1 | Printed pp. 69 / PDF pp. 73.**

**Requirement:** Avoid unnecessary empty statements.

**Review:** Inspect stray semicolons after conditions/loops.

**Conditions and notes:** Shared C/C++; advisory; the explicitly annotated empty branch under R-1-4-2 is an exception.

**Discouraged fragment:**

```c
if (ready); { run(); }
```

**Preferred fragment:**

```c
if (ready) { run(); }
```

### A-1-8-2 - Avoid redundant variables

**Advisory | C/C++ (where applicable) | GJB 8114-2013, clause 5.8.2.2 | Printed pp. 69 / PDF pp. 73.**

**Requirement:** Avoid useless redundant variables.

**Review:** Check whether the variable provides a required value/lifetime.

**Conditions and notes:** Shared C/C++; advisory; avoid deleting RAII guards just because their names are not referenced.

**Discouraged fragment:**

```c
int unused = 0;
```

**Preferred fragment:**

```c
/* Remove the unused object when it has no required construction or volatile effects. */
```

### A-1-8-3 - Avoid redundant functions

**Advisory | C/C++ (where applicable) | GJB 8114-2013, clause 5.8.2.3 | Printed pp. 69 / PDF pp. 73.**

**Requirement:** Avoid unnecessary duplicate or unused functions.

**Review:** Review actual callers and semantic duplication.

**Conditions and notes:** Shared C/C++; advisory; externally callable APIs need whole-program evidence before removal.

**Discouraged fragment:**

```c
/* Two unused helpers implement identical conversion logic. */
```

**Preferred fragment:**

```c
/* Retain one required, tested implementation and remove unnecessary copies. */
```

### A-1-8-4 - Use numeric type suffixes

**Advisory | C/C++ (where applicable) | GJB 8114-2013, clause 5.8.2.4 | Printed pp. 69 / PDF pp. 73.**

**Requirement:** Prefer explicit numeric type suffixes.

**Review:** Inspect literals in typed arithmetic.

**Conditions and notes:** Shared C/C++; advisory; when used, suffix capitalization is separately required by R-1-8-5.

**Discouraged fragment:**

```c
unsigned int limit = 8;
```

**Preferred fragment:**

```c
unsigned int limit = 8U;
```

<a id="section-5-9"></a>

## 5.9 Loops

### R-1-9-1 - Local for-loop controls

**Required | C/C++ (where applicable) | GJB 8114-2013, clause 5.9.1.1 | Printed pp. 69-70 / PDF pp. 73-74.**

**Requirement:** Use local variables to control for loops.

**Review:** Inspect loop variables and external visibility.

**Conditions and notes:** Shared C/C++; locality reduces interference; no requirement to force a C99 declaration in a C90 build.

**Violation fragment:**

```c
for (global_index = 0; global_index < 4; ++global_index) { work(); }
```

**Correction fragment:**

```c
int index; for (index = 0; index < 4; ++index) { work(); }
```

### R-1-9-2 - Integer loop controls

**Required | C/C++ (where applicable) | GJB 8114-2013, clause 5.9.1.2 | Printed pp. 70 / PDF pp. 74.**

**Requirement:** Use integer variables as for-loop controls.

**Review:** Inspect induction-variable types.

**Conditions and notes:** Shared C/C++; examples use modern declaration placement only when the selected language supports it.

**Violation fragment:**

```c
for (float t = 0.0F; t < 1.0F; t += 0.1F) { work(); }
```

**Correction fragment:**

```c
for (int step = 0; step < 10; ++step) { work(); }
```

### R-1-9-3 - Do not modify loop controls in the body

**Required | C/C++ (where applicable) | GJB 8114-2013, clause 5.9.1.3 | Printed pp. 70 / PDF pp. 74.**

**Requirement:** Do not alter the for-loop control variable inside its body.

**Review:** Include indirect writes through calls or aliases.

**Conditions and notes:** Shared C/C++; the note expects a condition-controlled maximum iteration count; use a separate variable for variable-step work.

**Violation fragment:**

```c
for (i = 0; i < limit; ++i) { i += step; }
```

**Correction fragment:**

```c
for (i = 0; i < limit; ++i) { int position = i + step; use(position); }
```

### R-1-9-4 - Canonical unbounded loop

**Required | C/C++ (where applicable) | GJB 8114-2013, clause 5.9.1.4 | Printed pp. 70-71 / PDF pp. 74-75.**

**Requirement:** Use while(1) for an unbounded loop, rather than for(;;) or other forms.

**Review:** Inspect intended indefinitely running loops.

**Conditions and notes:** Shared C/C++; this is a coding convention, not evidence of termination or responsiveness.

**Violation fragment:**

```c
for (;;) { poll(); }
```

**Correction fragment:**

```c
while (1) { poll(); }
```

### A-1-9-1 - Cautious unbounded loops

**Advisory | C/C++ (where applicable) | GJB 8114-2013, clause 5.9.2.1 | Printed pp. 71 / PDF pp. 75.**

**Requirement:** Use unbounded loops cautiously.

**Review:** Review intentional task lifetime, exits, blocking, watchdog, and scheduler behavior.

**Conditions and notes:** Shared C/C++; advisory; embedded dispatcher loops are not automatically forbidden.

**Discouraged fragment:**

```c
while (1) { /* unbounded busy wait */ }
```

**Preferred fragment:**

```c
/* Use the required event wait or bounded polling policy inside the intentional task loop. */
```

### A-1-9-2 - Cautious multiple breaks

**Advisory | C/C++ (where applicable) | GJB 8114-2013, clause 5.9.2.2 | Printed pp. 71 / PDF pp. 75.**

**Requirement:** Use multiple break exits in one loop cautiously.

**Review:** Review all exits and cleanup paths.

**Conditions and notes:** Shared C/C++; advisory, not a universal single-exit requirement.

**Discouraged fragment:**

```c
/* Several scattered exits obscure which resources remain held. */
```

**Preferred fragment:**

```c
/* Consolidate related exit decisions where that improves correctness. */
```

### A-1-9-3 - Cautious multiple continues

**Advisory | C/C++ (where applicable) | GJB 8114-2013, clause 5.9.2.3 | Printed pp. 71 / PDF pp. 75.**

**Requirement:** Use multiple continue paths in one loop cautiously.

**Review:** Check updates, resource handling, and skipped work.

**Conditions and notes:** Shared C/C++; advisory; preserve algorithmic intent.

**Discouraged fragment:**

```c
/* Several continue statements skip required accounting. */
```

**Preferred fragment:**

```c
/* Make accounting unconditional or explicitly handle it before every continue. */
```

<a id="section-5-10"></a>

## 5.10 Type conversions

### R-1-10-1 - Explicit floating-to-integer conversion

**Required | C/C++ (where applicable) | GJB 8114-2013, clause 5.10.1.1 | Printed pp. 71-72 / PDF pp. 75-76.**

**Requirement:** Explicitly convert a floating variable assigned to an integer variable.

**Review:** Check cast presence, finite/range preconditions, and rounding intent.

**Conditions and notes:** Shared C/C++; a cast makes conversion explicit but does not prove it safe.

**Violation fragment:**

```c
int count = measured; /* measured is float */
```

**Correction fragment:**

```c
int count = (int)measured; /* after finite/range validation */
```

### R-1-10-2 - Explicit integer narrowing

**Required | C/C++ (where applicable) | GJB 8114-2013, clause 5.10.1.2 | Printed pp. 72-73 / PDF pp. 76-77.**

**Requirement:** Explicitly convert a longer integer variable assigned to a shorter integer variable.

**Review:** Compare effective target types and limits.

**Conditions and notes:** Shared C/C++; source type names alone do not establish actual widths on every ABI.

**Violation fragment:**

```c
short code = wide; /* wide is long */
```

**Correction fragment:**

```c
short code = (short)wide; /* after range validation */
```

### R-1-10-3 - Explicit double narrowing

**Required | C/C++ (where applicable) | GJB 8114-2013, clause 5.10.1.3 | Printed pp. 73 / PDF pp. 77.**

**Requirement:** Explicitly convert double variables assigned to float variables.

**Review:** Inspect assignments and precision/range loss.

**Conditions and notes:** Shared C/C++; select an approved C++ cast spelling when applying the C++ advisory rule.

**Violation fragment:**

```c
float result = precise; /* precise is double */
```

**Correction fragment:**

```c
float result = (float)precise; /* after approved loss analysis */
```

### R-1-10-4 - Pointer assignment types

**Required | C/C++ (where applicable) | GJB 8114-2013, clause 5.10.1.4 | Printed pp. 73-74 / PDF pp. 77-78.**

**Requirement:** Match the assignment expression's pointer type to the receiving pointer variable.

**Review:** Resolve the complete converted expression type.

**Conditions and notes:** Shared C/C++; the source also illustrates a cast to the receiving pointer type, but that alone does not justify alignment, aliasing, or extent safety.

**Violation fragment:**

```c
unsigned int *p = &short_value;
```

**Correction fragment:**

```c
unsigned short *p = &short_value;
```

### R-1-10-5 - Explicit pointer/integer conversion

**Required | C/C++ (where applicable) | GJB 8114-2013, clause 5.10.1.5 | Printed pp. 74 / PDF pp. 78.**

**Requirement:** Use an explicit conversion when assigning pointer values to non-pointer variables or vice versa.

**Review:** Inspect ABI width, representation, and validity.

**Conditions and notes:** Shared C/C++; example requires an available uintptr_t and approved representation. An explicit cast is not authorization to dereference an arbitrary integer address.

**Violation fragment:**

```c
address = pointer;
```

**Correction fragment:**

```c
uintptr_t address = (uintptr_t)pointer;
```

### R-1-10-6 - No ineffective casts

**Required | C/C++ (where applicable) | GJB 8114-2013, clause 5.10.1.6 | Printed pp. 74-75 / PDF pp. 78-79.**

**Requirement:** Do not use casts with no substantive purpose.

**Review:** Inspect source/result types and actual conversion scope.

**Conditions and notes:** Shared C/C++; do not remove required boundary conversions or casts used for a documented overload/ABI purpose without analysis.

**Violation fragment:**

```c
unsigned int copy = (unsigned int)source; /* source is already unsigned int */
```

**Correction fragment:**

```c
unsigned int copy = source;
```

### A-1-10-1 - Specify rounding

**Advisory | C/C++ (where applicable) | GJB 8114-2013, clause 5.10.2.1 | Printed pp. 75 / PDF pp. 79.**

**Requirement:** Consider whether floating-to-integer conversion needs rounding.

**Review:** Check requirements for positive/negative and halfway cases.

**Conditions and notes:** Shared C/C++; advisory; do not apply the source's simple rounding macro blindly to NaNs or out-of-range values.

**Discouraged fragment:**

```c
int count = (int)measured; /* nearest required */
```

**Preferred fragment:**

```c
/* Apply the specified rounding policy, validate range, then convert. */
```

### A-1-10-2 - Cautious double-to-float

**Advisory | C/C++ (where applicable) | GJB 8114-2013, clause 5.10.2.2 | Printed pp. 75 / PDF pp. 79.**

**Requirement:** Use double-to-float conversions cautiously.

**Review:** Check numerical error budget, extremes, and subnormals.

**Conditions and notes:** Shared C/C++; advisory; explicitness and numerical adequacy are separate.

**Discouraged fragment:**

```c
float result = (float)precise; /* loss unassessed */
```

**Preferred fragment:**

```c
/* Retain double or document and test acceptable narrowing. */
```

### A-1-10-3 - Cautious integer narrowing

**Advisory | C/C++ (where applicable) | GJB 8114-2013, clause 5.10.2.3 | Printed pp. 75 / PDF pp. 79.**

**Requirement:** Use long-to-short integer conversions cautiously.

**Review:** Prove representability before conversion.

**Conditions and notes:** Shared C/C++; advisory; choose limits for the actual signedness.

**Discouraged fragment:**

```c
short result = (short)wide; /* unchecked */
```

**Preferred fragment:**

```c
if ((wide >= SHRT_MIN) && (wide <= SHRT_MAX)) { result = (short)wide; }
```

### A-1-10-4 - Cautious pointer/integer assignments

**Advisory | C/C++ (where applicable) | GJB 8114-2013, clause 5.10.2.4 | Printed pp. 75 / PDF pp. 79.**

**Requirement:** Use pointer-to-nonpointer and reverse assignments cautiously.

**Review:** Review architecture-specific representation and approved hardware interfaces.

**Conditions and notes:** Shared C/C++; advisory; do not invent portability guarantees.

**Discouraged fragment:**

```c
/* Unvalidated numeric input is cast to a pointer and dereferenced. */
```

**Preferred fragment:**

```c
/* Use a validated target-specific address abstraction or a typed object reference. */
```

<a id="section-5-11"></a>

## 5.11 Initialization

### R-1-11-1 - Initialize before use

**Required | C/C++ (where applicable) | GJB 8114-2013, clause 5.11.1.1 | Printed pp. 75-76 / PDF pp. 79-80.**

**Requirement:** Do not use variables before assignment.

**Review:** Perform path-sensitive initialization analysis.

**Conditions and notes:** Shared C/C++; a write on one conditional path is insufficient.

**Violation fragment:**

```c
int count; return count;
```

**Correction fragment:**

```c
int count = 0; return count;
```

### R-1-11-2 - Explicit static initialization

**Required | C/C++ (where applicable) | GJB 8114-2013, clause 5.11.1.2 | Printed pp. 76 / PDF pp. 80.**

**Requirement:** Do not implicitly depend on system default values for variable initialization.

**Review:** Inspect file-scope and static definitions.

**Conditions and notes:** Shared C/C++; distinguish language-guaranteed zero initialization from this stricter explicit-initialization coding rule.

**Violation fragment:**

```c
static int state;
```

**Correction fragment:**

```c
static int state = 0;
```

### R-1-11-3 - Match aggregate initialization structure

**Required | C/C++ (where applicable) | GJB 8114-2013, clause 5.11.1.3 | Printed pp. 76-77 / PDF pp. 80-81.**

**Requirement:** Match nested initialization braces to the structure definition.

**Review:** Compare initializer nesting and member order.

**Conditions and notes:** Shared C/C++; language-permitted brace elision can still violate this coding requirement.

**Violation fragment:**

```c
struct Pair { int x; int y; }; struct Box { int tag; struct Pair point; }; struct Box b = {1, 2, 3};
```

**Correction fragment:**

```c
struct Pair { int x; int y; }; struct Box { int tag; struct Pair point; }; struct Box b = {1, {2, 3}};
```

### R-1-11-4 - Consistent enum initializers

**Required | C/C++ (where applicable) | GJB 8114-2013, clause 5.11.1.4 | Printed pp. 77-78 / PDF pp. 81-82.**

**Requirement:** Initialize only the first enumerator explicitly, or initialize every enumerator explicitly.

**Review:** Inspect complete enum definitions.

**Conditions and notes:** Shared C/C++; the note permits first-only initialization; do not demand explicit values for every enum member unconditionally.

**Violation fragment:**

```c
enum Mode { IDLE, RUN = 4, STOP };
```

**Correction fragment:**

```c
enum Mode { IDLE = 3, RUN = 4, STOP = 5 };
```

### A-1-11-1 - Initialize at declaration

**Advisory | C/C++ (where applicable) | GJB 8114-2013, clause 5.11.2.1 | Printed pp. 78 / PDF pp. 82.**

**Requirement:** Prefer initializing variables when declared.

**Review:** Inspect unnecessary intervals with indeterminate state.

**Conditions and notes:** Shared C/C++; advisory; this does not replace required path-safe initialization before use.

**Discouraged fragment:**

```c
int count; count = 0;
```

**Preferred fragment:**

```c
int count = 0;
```

### A-1-11-2 - Coordinated global initialization

**Advisory | C/C++ (where applicable) | GJB 8114-2013, clause 5.11.2.2 | Printed pp. 78 / PDF pp. 82.**

**Requirement:** Prefer initializing global variables in a consistently designed initialization module.

**Review:** Review order, dependencies, and readiness before use.

**Conditions and notes:** Shared C/C++; advisory; do not erase required definition-time initializers or break C++ initialization semantics.

**Discouraged fragment:**

```c
/* Independent startup fragments initialize mutually dependent globals in unknown order. */
```

**Preferred fragment:**

```c
/* Use a documented initialization sequence with explicit dependency and failure handling. */
```

<a id="section-5-12"></a>

## 5.12 Comparisons

### R-1-12-1 - No Boolean ordering

**Required | C/C++ (where applicable) | GJB 8114-2013, clause 5.12.1.1 | Printed pp. 78-79 / PDF pp. 82-83.**

**Requirement:** Do not order logical values using greater-than or less-than.

**Review:** Resolve Boolean-valued variables even when typedefed to an integer.

**Conditions and notes:** Shared C/C++; preserve the actual truth condition rather than arbitrarily replacing > with &&.

**Violation fragment:**

```c
if (ready > enabled) { run(); }
```

**Correction fragment:**

```c
if (ready && !enabled) { run(); }
```

### R-1-12-2 - No pointer ordering

**Required | C/C++ (where applicable) | GJB 8114-2013, clause 5.12.1.2 | Printed pp. 79-80 / PDF pp. 83-84.**

**Requirement:** Do not compare pointers using greater-than or less-than.

**Review:** Inspect comparison operand types.

**Conditions and notes:** Shared C/C++; this is stricter than some language-permitted same-array ordering; do not misstate the language itself.

**Violation fragment:**

```c
if (left > right) { choose(); } /* pointers */
```

**Correction fragment:**

```c
if (*left > *right) { choose(); } /* when comparing valid pointed-to values is intended */
```

### R-1-12-3 - No exact floating equality

**Required | C/C++ (where applicable) | GJB 8114-2013, clause 5.12.1.3 | Printed pp. 80-81 / PDF pp. 84-85.**

**Requirement:** Do not compare floating values for exact equality or inequality; compare differences against specified precision.

**Review:** Check both == and !=, magnitude scales, NaNs, and infinities.

**Conditions and notes:** Shared C/C++; the source prescribes a given precision; derive tolerance from requirements, not a universal epsilon.

**Violation fragment:**

```c
if (actual == target) { accept(); }
```

**Correction fragment:**

```c
if (fabs(actual - target) < tolerance) { accept(); }
```

### R-1-12-4 - Unsigned comparisons with zero

**Required | C/C++ (where applicable) | GJB 8114-2013, clause 5.12.1.4 | Printed pp. 81-82 / PDF pp. 85-86.**

**Requirement:** Do not use unsigned >=0 or <0 comparisons.

**Review:** Check unsigned operand types and intended zero/nonzero logic.

**Conditions and notes:** Shared C/C++; the source also flags <=0 in an example, although that can meaningfully test zero. Record this discrepancy; prefer an explicit ==0 test for zero intent.

**Violation fragment:**

```c
if (count >= 0U) { work(); }
```

**Correction fragment:**

```c
if (count > 0U) { work(); } /* when positive is intended */
```

### R-1-12-5 - No direct mixed-sign comparison

**Required | C/C++ (where applicable) | GJB 8114-2013, clause 5.12.1.5 | Printed pp. 82 / PDF pp. 86.**

**Requirement:** Do not directly compare signed and unsigned values.

**Review:** Prove range before choosing a common comparison domain.

**Conditions and notes:** Shared C/C++; the source illustrates a cast, but unchecked unsigned-to-signed conversion can itself lose information.

**Violation fragment:**

```c
if (signed_count < unsigned_limit) { run(); }
```

**Correction fragment:**

```c
/* Check signed_count for negativity, then compare validated nonnegative values in a common representable type. */
```

### A-1-12-1 - Constant-first equality

**Advisory | C/C++ (where applicable) | GJB 8114-2013, clause 5.12.2 | Printed pp. 82 / PDF pp. 86.**

**Requirement:** Prefer placing a constant on the left of equality comparisons.

**Review:** Inspect comparisons with constants.

**Conditions and notes:** Shared C/C++; advisory; do not rewrite relational operators without reversing the operator correctly.

**Discouraged fragment:**

```c
if (mode == 2) { run(); }
```

**Preferred fragment:**

```c
if (2 == mode) { run(); }
```

<a id="section-5-13"></a>

## 5.13 Variable use and names

### R-1-13-1 - No local/global name collision

**Required | C/C++ (where applicable) | GJB 8114-2013, clause 5.13.1.1 | Printed pp. 83 / PDF pp. 87.**

**Requirement:** Do not give a local variable the same name as a global variable.

**Review:** Resolve scopes across visible declarations.

**Conditions and notes:** Shared C/C++; legal shadowing can still violate the rule.

**Violation fragment:**

```c
int state = 0; void f(void) { int state = 1; }
```

**Correction fragment:**

```c
int state = 0; void f(void) { int next_state = 1; }
```

### R-1-13-2 - No parameter/global name collision

**Required | C/C++ (where applicable) | GJB 8114-2013, clause 5.13.1.2 | Printed pp. 83 / PDF pp. 87.**

**Requirement:** Do not give a formal parameter the same name as a global variable.

**Review:** Compare interface names against globals.

**Conditions and notes:** Shared C/C++; update matching prototype names consistently.

**Violation fragment:**

```c
int state = 0; int f(int state) { return state; }
```

**Correction fragment:**

```c
int state = 0; int f(int requested_state) { return requested_state; }
```

### R-1-13-3 - Distinct variable/function names

**Required | C/C++ (where applicable) | GJB 8114-2013, clause 5.13.1.3 | Printed pp. 83 / PDF pp. 87.**

**Requirement:** Do not name a variable after a function.

**Review:** Inspect all identifiers and shadowing.

**Conditions and notes:** Shared C/C++; do not silently rename external ABI symbols.

**Violation fragment:**

```c
void reset(void); void f(void) { int reset = 0; }
```

**Correction fragment:**

```c
void reset(void); void f(void) { int reset_count = 0; }
```

### R-1-13-4 - Distinct variable/tag names

**Required | C/C++ (where applicable) | GJB 8114-2013, clause 5.13.1.4 | Printed pp. 84 / PDF pp. 88.**

**Requirement:** Do not reuse a type/aggregate identifying tag as a variable name.

**Review:** Compare object names with struct/union/enum tags.

**Conditions and notes:** Shared C/C++; the source examples clarify the broad word identifier as aggregate tag naming.

**Violation fragment:**

```c
struct Packet { int id; }; struct Packet Packet;
```

**Correction fragment:**

```c
struct Packet { int id; }; struct Packet packet;
```

### R-1-13-5 - Distinct variable/enumerator names

**Required | C/C++ (where applicable) | GJB 8114-2013, clause 5.13.1.5 | Printed pp. 84-85 / PDF pp. 88-89.**

**Requirement:** Do not reuse an enumerator name as a variable name.

**Review:** Resolve enumerator visibility and inner scopes.

**Conditions and notes:** Shared C/C++; scoped-enum differences require language-aware applicability.

**Violation fragment:**

```c
enum Mode { IDLE = 0, RUN }; void f(void) { int RUN = 1; }
```

**Correction fragment:**

```c
enum Mode { IDLE = 0, RUN }; void f(void) { int run_count = 1; }
```

### R-1-13-6 - Distinct variable/typedef names

**Required | C/C++ (where applicable) | GJB 8114-2013, clause 5.13.1.6 | Printed pp. 85 / PDF pp. 89.**

**Requirement:** Do not reuse a typedef name as a variable name.

**Review:** Expand aliases and inspect nested scopes.

**Conditions and notes:** Shared C/C++; keep naming distinct even where the language permits hiding.

**Violation fragment:**

```c
typedef int Count; void f(void) { int Count = 0; }
```

**Correction fragment:**

```c
typedef int Count; void f(void) { Count count = 0; }
```

### R-1-13-7 - No inner-block variable shadowing

**Required | C/C++ (where applicable) | GJB 8114-2013, clause 5.13.1.7 | Printed pp. 85-86 / PDF pp. 89-90.**

**Requirement:** Do not redefine an existing variable name inside an inner block.

**Review:** Resolve scopes through nested control structures.

**Conditions and notes:** Shared C/C++; avoid changing which object an existing reference resolves to.

**Violation fragment:**

```c
int count = 1; if (ready) { int count = 0; }
```

**Correction fragment:**

```c
int count = 1; if (ready) { int pending_count = 0; }
```

### R-1-13-8 - Case-distinguishable names

**Required | C/C++ (where applicable) | GJB 8114-2013, clause 5.13.1.8 | Printed pp. 86 / PDF pp. 90.**

**Requirement:** Do not rely solely on letter case to distinguish variable names.

**Review:** Compare names case-insensitively.

**Conditions and notes:** Shared C/C++; this differs from the language's case-sensitive symbol lookup.

**Violation fragment:**

```c
int Speed = 0; int speed = 1;
```

**Correction fragment:**

```c
int current_speed = 0; int target_speed = 1;
```

### R-1-13-9 - Distinguish l from 1

**Required | C/C++ (where applicable) | GJB 8114-2013, clause 5.13.1.9 | Printed pp. 86 / PDF pp. 90.**

**Requirement:** Do not distinguish variable names only by lowercase l versus digit 1.

**Review:** Inspect visually confusable identifier pairs.

**Conditions and notes:** Shared C/C++; font choice alone does not satisfy distinct naming.

**Violation fragment:**

```c
int pathl = 0; int path1 = 1;
```

**Correction fragment:**

```c
int primary_path = 0; int backup_path = 1;
```

### R-1-13-10 - Distinguish O from 0

**Required | C/C++ (where applicable) | GJB 8114-2013, clause 5.13.1.10 | Printed pp. 86 / PDF pp. 90.**

**Requirement:** Do not distinguish variable names only by uppercase O versus digit 0.

**Review:** Inspect visually confusable identifier pairs.

**Conditions and notes:** Shared C/C++; preserve external names only through explicit compatibility handling.

**Violation fragment:**

```c
int codeO = 0; int code0 = 1;
```

**Correction fragment:**

```c
int old_code = 0; int new_code = 1;
```

### R-1-13-11 - No single-character l or O variables

**Required | C/C++ (where applicable) | GJB 8114-2013, clause 5.13.1.11 | Printed pp. 86 / PDF pp. 90.**

**Requirement:** Do not use lowercase l or uppercase O alone as a variable name.

**Review:** Inspect single-letter identifiers.

**Conditions and notes:** Shared C/C++; this does not ban every single-character variable.

**Violation fragment:**

```c
int l = 1; int O = 0;
```

**Correction fragment:**

```c
int length = 1; int offset = 0;
```

### R-1-13-12 - Externally modified objects

**Required | C/C++ (where applicable) | GJB 8114-2013, clause 5.13.1.12 | Printed pp. 86 / PDF pp. 90.**

**Requirement:** Use volatile declarations for variables that can change outside the program's ordinary execution.

**Review:** Identify memory-mapped registers, dual-port storage, and externally modified state.

**Conditions and notes:** Shared C/C++; source examples include thread-shared variables, but volatile does not provide atomicity, synchronization, or data-race safety. Preserve atomics/locks and resolve tailoring explicitly.

**Violation fragment:**

```c
unsigned int *status_register;
```

**Correction fragment:**

```c
volatile unsigned int *status_register;
```

### R-1-13-13 - Read volatile state once per expression

**Required | C/C++ (where applicable) | GJB 8114-2013, clause 5.13.1.13 | Printed pp. 86-87 / PDF pp. 90-91.**

**Requirement:** Do not operate on multiple occurrences of the same volatile variable in one expression.

**Review:** Count accesses after macro expansion.

**Conditions and notes:** Shared C/C++; snapshotting is appropriate only when the hardware/protocol permits that access pattern.

**Violation fragment:**

```c
unsigned int result = flag + flag; /* flag is volatile */
```

**Correction fragment:**

```c
unsigned int snapshot = flag; unsigned int result = snapshot + snapshot;
```

### R-1-13-14 - NULL is not numeric zero

**Required | C/C++ (where applicable) | GJB 8114-2013, clause 5.13.1.14 | Printed pp. 87 / PDF pp. 91.**

**Requirement:** Do not use NULL as an integer zero value.

**Review:** Resolve the expected operand/parameter type.

**Conditions and notes:** Shared C/C++; keep null-pointer and numeric-zero intent separate.

**Violation fragment:**

```c
int retries = NULL;
```

**Correction fragment:**

```c
int retries = 0;
```

### R-1-13-15 - Unsigned negative assignments

**Required | C/C++ (where applicable) | GJB 8114-2013, clause 5.13.1.15 | Printed pp. 88 / PDF pp. 92.**

**Requirement:** Do not assign a negative value to an unsigned variable implicitly.

**Review:** Inspect negative literals/expressions and intentional modular representations.

**Conditions and notes:** Shared C/C++; the source labels the explicit cast as compliant despite stronger headline wording. Record that boundary; reject negative domain input when modular encoding is not intended.

**Violation fragment:**

```c
unsigned short value = -2;
```

**Correction fragment:**

```c
unsigned short value = (unsigned short)(-2); /* only for specified modular encoding */
```

### R-1-13-16 - Terminate strings

**Required | C/C++ (where applicable) | GJB 8114-2013, clause 5.13.1.16 | Printed pp. 88-89 / PDF pp. 92-93.**

**Requirement:** Arrays used as strings must end with a NUL character.

**Review:** Check construction, copying, append operations, and consumers.

**Conditions and notes:** Shared C/C++; binary buffers are not automatically strings.

**Violation fragment:**

```c
char text[2] = {'O', 'K'}; puts(text);
```

**Correction fragment:**

```c
char text[3] = {'O', 'K', '\0'}; puts(text);
```

### A-1-13-1 - Type-prefixed names

**Advisory | C/C++ (where applicable) | GJB 8114-2013, clause 5.13.2.1 | Printed pp. 89 / PDF pp. 93.**

**Requirement:** Prefer variable names containing a type prefix.

**Review:** Compare the prefix with actual declarations and project naming conventions.

**Conditions and notes:** Shared C/C++; advisory. The source's illustrative width/range table is not a target ABI guarantee; document actual platform ranges.

**Discouraged fragment:**

```c
unsigned int retries = 0U;
```

**Preferred fragment:**

```c
unsigned int uiRetries = 0U;
```

### A-1-13-2 - Cautious register variables

**Advisory | C/C++ (where applicable) | GJB 8114-2013, clause 5.13.2.2 | Printed pp. 89 / PDF pp. 93.**

**Requirement:** Use register storage-class variables cautiously.

**Review:** Inspect language version and any address-taking or ABI assumptions.

**Conditions and notes:** Shared legacy advisory; register does not specify a particular hardware register, and modern C++ may reject it.

**Discouraged fragment:**

```c
register int index; /* relied on for hardware placement */
```

**Preferred fragment:**

```c
int index; /* let the compiler allocate registers */
```

<a id="section-6-1"></a>

## 6.1 Classes and inheritance

### R-2-1-1 - Define ownership-aware copying

**Required | C++ | GJB 8114-2013, clause 6.1.1.1 | Printed pp. 90-91 / PDF pp. 94-95.**

**Requirement:** A class with dynamically allocated members must define a copy constructor and overload assignment.

**Review:** Inspect owned allocations and both copy operations; test independent ownership and self-assignment.

**Conditions and notes:** C++ owning classes. Deleted copying or modern ownership wrappers require an explicit project interpretation or tailoring; do not silently equate them to the literal requirement.

**Violation fragment:**

```cpp
class Owner { int *p; /* implicit shallow copying */ };
```

**Correction fragment:**

```cpp
class Owner {
public:
    Owner(void) : p(new int(0)) {}
    Owner(const Owner &other) : p(new int(*other.p)) {}
    Owner &operator=(const Owner &other) {
        if (this != &other) { *p = *other.p; }
        return *this;
    }
    ~Owner(void) { delete p; p = NULL; }
private:
    int *p;
};
```

### R-2-1-2 - Check virtual-base downcasts

**Required | C++ | GJB 8114-2013, clause 6.1.1.2 | Printed pp. 91-93 / PDF pp. 95-97.**

**Requirement:** Use dynamic_cast for conversions from a virtual-base pointer to a derived pointer; the examples also cover references.

**Review:** Verify polymorphic source, target lifetime, pointer failure checks, and reference failure handling.

**Conditions and notes:** C++ virtual-base downcasts. Record RTTI or exception-policy conflicts; never replace checked downcasts with unchecked casts to satisfy a disabled-runtime configuration.

**Violation fragment:**

```cpp
Derived *p = (Derived *)base;
```

**Correction fragment:**

```cpp
Derived *p = dynamic_cast<Derived *>(base);
if (p != NULL) { p->operate(); }
```

### R-2-1-3 - Share diamond bases explicitly

**Required | C++ | GJB 8114-2013, clause 6.1.1.3 | Printed pp. 93-96 / PDF pp. 97-100.**

**Requirement:** Use virtual inheritance for the common base in a diamond hierarchy.

**Review:** Trace every path to the repeated base and initialization by the most-derived class.

**Conditions and notes:** C++ diamond inheritance; this is not a general prohibition of multiple inheritance.

**Violation fragment:**

```cpp
struct Left : Root {};
struct Right : Root {};
struct Leaf : Left, Right {};
```

**Correction fragment:**

```cpp
struct Left : virtual Root {};
struct Right : virtual Root {};
struct Leaf : Left, Right {};
```

### R-2-1-4 - Restrict abstract-base assignment

**Required | C++ | GJB 8114-2013, clause 6.1.1.4 | Printed pp. 96-99 / PDF pp. 100-103.**

**Requirement:** Declare the copy-assignment operator of an abstract class protected or private.

**Review:** Check accessibility of assignment through base references and partial-object copying.

**Conditions and notes:** C++ abstract classes. The example concerns assignment, not a blanket access restriction on all copying operations.

**Violation fragment:**

```cpp
public: Base &operator=(const Base &other);
```

**Correction fragment:**

```cpp
protected: Base &operator=(const Base &other);
```

### A-2-1-1 - Use virtual bases cautiously

**Advisory | C++ | GJB 8114-2013, clause 6.1.2.1 | Printed pp. 99 / PDF pp. 103.**

**Requirement:** Exercise caution when deriving from virtual bases.

**Review:** Review layout, construction responsibility, ambiguity, timing, and maintenance costs.

**Conditions and notes:** C++ advisory; virtual inheritance is not prohibited.

**Discouraged scenario:** introduce virtual inheritance without analyzing shared-base ownership.

**Preferred scenario:** document the shared-base need and construction and layout implications.

### A-2-1-2 - Use inline functions cautiously

**Advisory | C++ | GJB 8114-2013, clause 6.1.2.2 | Printed pp. 99 / PDF pp. 103.**

**Requirement:** Exercise caution in using inline functions.

**Review:** Review code size and timing using actual compiler output where relevant.

**Conditions and notes:** C++ advisory; inline syntax does not guarantee machine-code inlining.

**Discouraged scenario:** inline a large routine solely on an assumed speed benefit.

**Preferred scenario:** keep a normal function unless measured results justify inlining.

<a id="section-6-2"></a>

## 6.2 Constructors

### R-2-2-1 - Keep globals out of constructors

**Required | C++ | GJB 8114-2013, clause 6.2.1.1 | Printed pp. 99-100 / PDF pp. 103-104.**

**Requirement:** Do not use global variables inside constructors.

**Review:** Trace direct and helper-mediated global accesses and initialization-order dependencies.

**Conditions and notes:** C++ constructors. Passing a global value as an explicit argument is the source's accepted pattern; this does not prove startup order safe.

**Violation fragment:**

```cpp
Device::Device(void) : value(global_value) {}
```

**Correction fragment:**

```cpp
Device::Device(int initial) : value(initial) {}
```

### R-2-2-2 - Define a default constructor explicitly

**Required | C++ | GJB 8114-2013, clause 6.2.1.2 | Printed pp. 100-102 / PDF pp. 104-106.**

**Requirement:** Explicitly define the class default constructor.

**Review:** Check the deliberate no-argument initial state and all member initialization.

**Conditions and notes:** C++. For intentionally non-default-constructible classes or modern =default, record the project interpretation instead of inventing a meaningless constructor.

**Violation fragment:**

```cpp
class Counter { int value; };
```

**Correction fragment:**

```cpp
class Counter { public: Counter(void) : value(0) {} private: int value; };
```

### R-2-2-3 - Make converting constructors explicit

**Required | C++ | GJB 8114-2013, clause 6.2.1.3 | Printed pp. 102-104 / PDF pp. 106-108.**

**Requirement:** Use explicit on single-argument constructors.

**Review:** Inspect implicit conversion paths in calls and assignments.

**Conditions and notes:** C++ converting constructors. Do not automatically apply this example to special copy constructors without considering their language semantics and the project interpretation.

**Violation fragment:**

```cpp
Sample(int value);
```

**Correction fragment:**

```cpp
explicit Sample(int value);
```

### R-2-2-4 - Initialize every member in every constructor

**Required | C++ | GJB 8114-2013, clause 6.2.1.4 | Printed pp. 104-105 / PDF pp. 108-109.**

**Requirement:** Each constructor must initialize every member variable.

**Review:** Inspect all constructor paths and member states before use.

**Conditions and notes:** C++. Initializer lists are a useful implementation choice; the original also demonstrates assignments. Modern default member initializers need a documented version-aware interpretation.

**Violation fragment:**

```cpp
Sample::Sample(void) { first = 0; /* second omitted */ }
```

**Correction fragment:**

```cpp
Sample::Sample(void) : first(0), second(0) {}
```

### R-2-2-5 - Name direct-base construction

**Required | C++ | GJB 8114-2013, clause 6.2.1.5 | Printed pp. 105-106 / PDF pp. 109-110.**

**Requirement:** A derived constructor must explicitly specify direct-base construction in its initializer list.

**Review:** Check all direct bases in every derived constructor.

**Conditions and notes:** C++; retain the intended base arguments rather than relying silently on implicit default construction.

**Violation fragment:**

```cpp
Derived::Derived(void) : member(0) {}
```

**Correction fragment:**

```cpp
Derived::Derived(void) : Base(), member(0) {}
```

<a id="section-6-3"></a>

## 6.3 Destructors

### R-2-3-1 - Use virtual destructors in polymorphic classes

**Required | C++ | GJB 8114-2013, clause 6.3.1.1 | Printed pp. 106-109 / PDF pp. 110-113.**

**Requirement:** A class with virtual member functions must have a virtual destructor.

**Review:** Inspect the hierarchy and deletion through base pointers.

**Conditions and notes:** C++ polymorphic classes; the source marks both base and derived destructor declarations explicitly virtual.

**Violation fragment:**

```cpp
class Base { public: virtual void run(void); ~Base(void); };
```

**Correction fragment:**

```cpp
class Base { public: virtual void run(void); virtual ~Base(void); };
```

### R-2-3-2 - Contain destructor exceptions

**Required | C++ | GJB 8114-2013, clause 6.3.1.2 | Printed pp. 109-110 / PDF pp. 113-114.**

**Requirement:** A destructor must not allow an exception to escape without handling it itself.

**Review:** Trace every potentially throwing call and cleanup path.

**Conditions and notes:** C++; the failure-recording path must itself not throw. Merely adding noexcept can terminate execution and does not establish local handling.

**Violation fragment:**

```cpp
Sample::~Sample(void) { close_checked(); }
```

**Correction fragment:**

```cpp
Sample::~Sample(void) { try { close_checked(); } catch (...) { record_cleanup_failure(); } }
```

<a id="section-6-4"></a>

## 6.4 Virtual functions

### R-2-4-1 - Preserve virtual default arguments

**Required | C++ | GJB 8114-2013, clause 6.4.1.1 | Printed pp. 110-113 / PDF pp. 114-117.**

**Requirement:** Do not change a base virtual function's default argument in an overriding declaration.

**Review:** Compare default arguments across the hierarchy and calls through different static types.

**Conditions and notes:** C++; the source also accepts omitting the derived default and supplying an explicit argument for derived calls.

**Violation fragment:**

```cpp
virtual int read(int mode = 2); // base uses 0
```

**Correction fragment:**

```cpp
virtual int read(int mode = 0); // same as base
```

### R-2-4-2 - State virtual on overrides

**Required | C++ | GJB 8114-2013, clause 6.4.1.2 | Printed pp. 113-115 / PDF pp. 117-119.**

**Requirement:** An overriding declaration must explicitly include virtual.

**Review:** Compare overridden signatures and declaration specifiers.

**Conditions and notes:** C++. Modern override is additional useful checking; do not silently claim that override alone satisfies the literal virtual requirement.

**Violation fragment:**

```cpp
int read(int mode); // overrides a virtual base member
```

**Correction fragment:**

```cpp
virtual int read(int mode);
```

### R-2-4-3 - Do not make a concrete virtual pure again

**Required | C++ | GJB 8114-2013, clause 6.4.1.3 | Printed pp. 115-116 / PDF pp. 119-120.**

**Requirement:** Do not override a non-pure virtual function with a pure virtual function.

**Review:** Trace the immediate and earlier hierarchy declarations.

**Conditions and notes:** C++; the source example has an abstract root, concrete intermediate, then prohibited re-abstraction.

**Violation fragment:**

```cpp
struct Derived : Base { virtual void run(void) = 0; }; // Base::run is concrete
```

**Correction fragment:**

```cpp
struct Derived : Base { virtual void run(void); };
```

<a id="section-6-5"></a>

## 6.5 Type conversions

### R-2-5-1 - Avoid unrelated object-pointer casts

**Required | C++ | GJB 8114-2013, clause 6.5.1.1 | Printed pp. 116-117 / PDF pp. 120-121.**

**Requirement:** Do not force an unrelated pointer type into an object-pointer type.

**Review:** Check casts against actual object types, inheritance, and lifetimes.

**Conditions and notes:** C++. Similar field layout does not make unrelated types interchangeable.

**Violation fragment:**

```cpp
Device *p = reinterpret_cast<Device *>(packet);
```

**Correction fragment:**

```cpp
Device *p = &device;
```

### R-2-5-2 - Preserve const and volatile

**Required | C++ | GJB 8114-2013, clause 6.5.1.2 | Printed pp. 117-118 / PDF pp. 121-122.**

**Requirement:** Do not remove const or volatile in pointer or reference conversions.

**Review:** Inspect named casts, C-style casts, and helper APIs for qualifier loss.

**Conditions and notes:** C++; this rule prohibits qualifier removal even where the language could permit a cast.

**Violation fragment:**

```cpp
int *p = const_cast<int *>(source);
```

**Correction fragment:**

```cpp
const int *p = source;
```

### A-2-5-1 - Prefer named C++ casts

**Advisory | C++ | GJB 8114-2013, clause 6.5.2 | Printed pp. 118 / PDF pp. 122.**

**Requirement:** Prefer C++ cast operators over C-style casts.

**Review:** Check the intended conversion category; a named cast does not make an unsafe conversion acceptable.

**Conditions and notes:** C++ advisory; preserve range checks and the required conversion restrictions.

**Discouraged fragment:**

```cpp
int result = (int)value;
```

**Preferred fragment:**

```cpp
int result = static_cast<int>(value);
```

<a id="section-6-6"></a>

## 6.6 Memory release

### R-2-6-1 - Release new allocations

**Required | C++ | GJB 8114-2013, clause 6.6.1.1 | Printed pp. 118-119 / PDF pp. 122-123.**

**Requirement:** Release memory allocated with new using delete after use.

**Review:** Trace ownership across normal exits, transfers, and exceptions.

**Conditions and notes:** C++; the rule does not ban dynamic allocation. Approved RAII can implement the release; allocation-failure handling follows the actual throwing or nothrow form.

**Violation fragment:**

```cpp
int *p = new int(3); /* owning pointer lost at exit */
```

**Correction fragment:**

```cpp
int *p = new int(3); use(*p); delete p; p = NULL;
```

### R-2-6-2 - Match array allocation and deletion

**Required | C++ | GJB 8114-2013, clause 6.6.1.2 | Printed pp. 119-120 / PDF pp. 123-124.**

**Requirement:** Use delete[] for memory allocated with new[].

**Review:** Pair allocator and deallocator forms across ownership transfers.

**Conditions and notes:** C++ arrays; scalar delete is not a substitute even for trivially destructible elements.

**Violation fragment:**

```cpp
int *p = new int[4];
delete p;
```

**Correction fragment:**

```cpp
int *p = new int[4];
delete[] p;
p = NULL;
```

### R-2-6-3 - Preserve the allocation address

**Required | C++ | GJB 8114-2013, clause 6.6.1.3 | Printed pp. 120-122 / PDF pp. 124-126.**

**Requirement:** The pointer used for delete must designate the original new allocation address.

**Review:** Track pointer arithmetic, aliases, and the owning base address.

**Conditions and notes:** C++. Do not mistake this array example for a ban on valid language-defined deletion through a suitable polymorphic base pointer.

**Violation fragment:**

```cpp
int *p = new int[4];
++p;
delete[] p;
```

**Correction fragment:**

```cpp
int *owner = new int[4];
int *cursor = owner + 1;
(void)cursor;
delete[] owner;
owner = NULL;
```

<a id="section-6-7"></a>

## 6.7 Function definition and use

### R-2-7-1 - Pass fixed-size arrays by reference

**Required | C++ | GJB 8114-2013, clause 6.7.1.1 | Printed pp. 122-123 / PDF pp. 126-127.**

**Requirement:** Pass fixed-length array variables to functions by reference.

**Review:** Inspect array parameter adjustment and preservation of the required extent.

**Conditions and notes:** C++ fixed-size arrays; variable-length buffers and modern container interfaces need their own explicit project interpretation.

**Violation fragment:**

```cpp
void update(int values[4]);
```

**Correction fragment:**

```cpp
void update(int (&values)[4]);
```

### R-2-7-2 - Preserve const in member results

**Required | C++ | GJB 8114-2013, clause 6.7.1.2 | Printed pp. 123-126 / PDF pp. 127-130.**

**Requirement:** A const member function must not return a non-const pointer or reference.

**Review:** Inspect return types and indirect mutation of owned storage.

**Conditions and notes:** C++; source examples concern exposing class-owned arrays. Do not infer that const on the pointer itself protects the pointed-to object.

**Violation fragment:**

```cpp
int *data(void) const;
```

**Correction fragment:**

```cpp
const int *data(void) const;
```

### R-2-7-3 - Do not expose mutable non-resource state

**Required | C++ | GJB 8114-2013, clause 6.7.1.3 | Printed pp. 126-129 / PDF pp. 130-133.**

**Requirement:** Do not return member results that allow external modification of non-resource object data.

**Review:** Trace references and pointers that bypass class invariants.

**Conditions and notes:** C++; the source qualifies this as non-resource data. Do not invent a universal ban on all resource-access interfaces; review their ownership and invariant contracts.

**Violation fragment:**

```cpp
int &count(void) { return count_; }
```

**Correction fragment:**

```cpp
int count(void) { return count_; }
```

### A-2-7-1 - Define member bodies outside the class

**Advisory | C++ | GJB 8114-2013, clause 6.7.2.1 | Printed pp. 129-130 / PDF pp. 133-134.**

**Requirement:** Avoid defining member-function implementation bodies inside the class definition.

**Review:** Review declaration and implementation placement.

**Conditions and notes:** C++ advisory; template visibility requirements still apply.

**Discouraged fragment:**

```cpp
class Device { public: void run(void) { operate(); } };
```

**Preferred fragment:**

```cpp
class Device { public: void run(void); };
void Device::run(void) { operate(); }
```

### A-2-7-2 - Make input referents const

**Advisory | C++ | GJB 8114-2013, clause 6.7.2.2 | Printed pp. 130 / PDF pp. 134.**

**Requirement:** Use const for pointer or reference parameters whose referents are not modified.

**Review:** Inspect writes and callees before applying const.

**Conditions and notes:** C++ advisory; top-level const on a pointer alone does not protect its referent.

**Discouraged fragment:**

```cpp
void inspect(Packet &packet);
```

**Preferred fragment:**

```cpp
void inspect(const Packet &packet);
```

<a id="section-6-8"></a>

## 6.8 Exception handling

### R-2-8-1 - Catch derived exceptions first

**Required | C++ | GJB 8114-2013, clause 6.8.1.1 | Printed pp. 130-133 / PDF pp. 134-137.**

**Requirement:** Order related exception handlers from derived classes to base classes.

**Review:** Compare handler types, inheritance, and handler reachability.

**Conditions and notes:** C++ exceptions; unrelated exception types have no derived-to-base ordering requirement.

**Violation fragment:**

```cpp
catch (const BaseError &e) { handle(e); }
catch (const DetailError &e) { handle(e); }
```

**Correction fragment:**

```cpp
catch (const DetailError &e) { handle(e); }
catch (const BaseError &e) { handle(e); }
```

### R-2-8-2 - Match every specified throw

**Required | C++ | GJB 8114-2013, clause 6.8.1.2 | Printed pp. 133-134 / PDF pp. 137-138.**

**Requirement:** Every explicitly specified throw must have a matching catch.

**Review:** Trace thrown types through calls, propagation, and enclosing handlers.

**Conditions and notes:** C++; a matching catch need not be in the throwing function itself. This is not a blanket ban on exceptions.

**Violation fragment:**

```cpp
try { throw ErrorB(); } catch (const ErrorA &e) { handle(e); }
```

**Correction fragment:**

```cpp
try { throw ErrorB(); } catch (const ErrorA &e) { handle(e); } catch (const ErrorB &e) { handle(e); }
```

### R-2-8-3 - Catch thrown objects by reference

**Required | C++ | GJB 8114-2013, clause 6.8.1.3 | Printed pp. 134-136 / PDF pp. 138-140.**

**Requirement:** Catch thrown exception objects using references.

**Review:** Inspect throw operands and handler declarations for copying or pointer lifetime hazards.

**Conditions and notes:** C++; source examples replace throwing a local object's address with throwing the object and catching by reference. Pointer exceptions are additionally cautioned by A-2-8-2.

**Violation fragment:**

```cpp
try { throw error; } catch (Error e) { handle(e); }
```

**Correction fragment:**

```cpp
try { throw error; } catch (const Error &e) { handle(e); }
```

### R-2-8-4 - Put catch-all last

**Required | C++ | GJB 8114-2013, clause 6.8.1.4 | Printed pp. 136-137 / PDF pp. 140-141.**

**Requirement:** Place the default catch handler after all typed handlers.

**Review:** Inspect every handler sequence.

**Conditions and notes:** C++; this ordering rule does not itself require adding a catch-all.

**Violation fragment:**

```cpp
try { work(); } catch (...) { recover(); } catch (const Error &e) { handle(e); }
```

**Correction fragment:**

```cpp
try { work(); } catch (const Error &e) { handle(e); } catch (...) { recover(); }
```

### R-2-8-5 - Do not throw untyped NULL

**Required | C++ | GJB 8114-2013, clause 6.8.1.5 | Printed pp. 138 / PDF pp. 142.**

**Requirement:** Do not explicitly throw NULL directly.

**Review:** Inspect throw expressions and their actual types.

**Conditions and notes:** C++; the original accepts a typed null pointer variable or explicit typed null cast. The object example avoids pointer-lifetime ambiguity; do not misstate the rule as banning every null-valued exception.

**Violation fragment:**

```cpp
throw NULL;
```

**Correction fragment:**

```cpp
throw Error();
```

### A-2-8-1 - Consider a final catch-all

**Advisory | C++ | GJB 8114-2013, clause 6.8.2.1 | Printed pp. 139 / PDF pp. 143.**

**Requirement:** Use a default catch after the specified typed handlers to prevent overlooked exceptions.

**Review:** Review recovery, logging, propagation, and safety-state policy.

**Conditions and notes:** C++ advisory; do not silently swallow failures or add catch-all handlers indiscriminately to every function.

**Discouraged scenario:** unexpected exception types bypass an intended containment boundary.

**Preferred scenario:** a final catch-all implements the approved containment or rethrow policy.

### A-2-8-2 - Use pointer exceptions cautiously

**Advisory | C++ | GJB 8114-2013, clause 6.8.2.2 | Printed pp. 139 / PDF pp. 143.**

**Requirement:** Exercise caution when throwing and catching pointer types.

**Review:** Analyze lifetime, ownership, and whether the handler must release storage.

**Conditions and notes:** C++ advisory; the source highlights uncertainty about releasing dynamically allocated exception pointers.

**Discouraged scenario:** throw a pointer to an automatic object whose lifetime ends during unwinding.

**Preferred scenario:** throw a value object and catch a const reference with defined lifetime.

<a id="section-6-9"></a>

## 6.9 Other C++ provisions

### R-2-9-1 - Keep template material together

**Required | C++ | GJB 8114-2013, clause 6.9.1 | Printed pp. 139 / PDF pp. 143.**

**Requirement:** Template declaration, definition, and implementation must be in the same file.

**Review:** Check the physical source file containing each template's material.

**Conditions and notes:** C++; modern modules, explicit-instantiation strategies, or split included implementation files need a documented project deviation or interpretation.

**Violation fragment:**

```cpp
/* buffer.h */ template<typename T> T twice(T value);
/* buffer.cpp */ template<typename T> T twice(T value) { return value + value; }
```

**Correction fragment:**

```cpp
/* buffer.h: declaration and implementation together */
template<typename T> T twice(T value) { return value + value; }
```

### A-2-9-1 - Use typename for template type parameters

**Advisory | C++ | GJB 8114-2013, clause 6.9.2.1 | Printed pp. 139 / PDF pp. 143.**

**Requirement:** Prefer typename when declaring type parameters in a template parameter list.

**Review:** Inspect type-parameter spellings without altering non-type or template-template parameter semantics.

**Conditions and notes:** C++ advisory; it is not a ban on class declarations.

**Discouraged fragment:**

```cpp
template<class T> class Buffer;
```

**Preferred fragment:**

```cpp
template<typename T> class Buffer;
```

### A-2-9-2 - Place const first where possible

**Advisory | C++ | GJB 8114-2013, clause 6.9.2.2 | Printed pp. 139-140 / PDF pp. 143-144.**

**Requirement:** Prefer const at the beginning of the type declaration, except for constant-pointer qualification.

**Review:** Check spelling while preserving which entity is const.

**Conditions and notes:** C++ advisory. int *const p fixes the pointer and must not be rewritten as const int *p, which changes meaning.

**Discouraged fragment:**

```cpp
int const value = 1;
```

**Preferred fragment:**

```cpp
const int value = 1;
```

### A-2-9-3 - Avoid overloading logical and comma operators

**Advisory | C++ | GJB 8114-2013, clause 6.9.2.3 | Printed pp. 140 / PDF pp. 144.**

**Requirement:** Avoid overloading &&, ||, and comma.

**Review:** Inspect overload declarations and unexpected evaluation or sequencing semantics.

**Conditions and notes:** C++ advisory; a function alternative does not provide built-in short-circuiting, so callers must express that behavior explicitly if required.

**Discouraged fragment:**

```cpp
bool operator&&(const Flag &left, const Flag &right);
```

**Preferred fragment:**

```cpp
bool both_set(const Flag &left, const Flag &right);
```

### A-2-9-4 - Prefer standard C++ header names

**Advisory | C++ | GJB 8114-2013, clause 6.9.2.4 | Printed pp. 140 / PDF pp. 144.**

**Requirement:** Avoid .h-suffixed C++ headers; the example replaces iostream.h with iostream.

**Review:** Distinguish obsolete C++ library headers from project, vendor, and C interoperability headers.

**Conditions and notes:** C++ advisory. The wording is broad but the example targets obsolete standard-library spelling; record the scope interpretation rather than renaming every project .h header without agreement.

**Discouraged fragment:**

```cpp
#include <iostream.h>
```

**Preferred fragment:**

```cpp
#include <iostream>
```

<a id="evaluation-method"></a>

## Evaluation method

Source: Chapter 7, printed pp. 140-141 / PDF pp. 144-145; informative Appendix B, printed pp. 149-152 / PDF pp. 153-156. Do not confuse rule coverage with the numeric violation rate.

Before using a coding-rule checker for this evaluation, Chapter 7 requires validation that it does not miss the violations in the standard's violating examples, does not falsely report the compliant parts of its compliant examples, and has a report confirming its detection capability against the standard. This skill and general compiler warnings have not undergone that checker qualification. Rule extraction, manual example review, and a skill-structure check do not replace it.

For an established, completely checked software scope:

1. Count total statement lines `N`. Chapter 3 defines a statement line as one physical newline-delimited line, including code, comments, and blank lines. Establish file set, revision, configurations, and counting treatment explicitly; do not substitute logical statements or executable-only lines.
2. Count violated required rules `M`, not the number of all diagnostics and not the number of checked rules. Keep advisory departures separate.
3. For each violated required rule `i`, count its violating statement lines `L_i`; retain file/line evidence and consolidate repeated diagnostics for the same rule and physical line.
4. Compute `L = sum(L_i)` and `P = (L / N) * 1000` in **per mille**, written `P per mille`. The rule-wise sum is not the union of physical lines across all rules: one line violating two different required rules contributes to both rule counts. Do not use `M` as the numerator or clamp the result to 1000. Report N, M, each L_i, L, units, precision, and limitations. For N=0, report undefined rather than divide by zero.

Chapter 7's suggested grades are:

| Grade | P in per mille | English rendering |
|---|---|---|
| 1 | P <= 3 | Very good |
| 2 | 3 < P <= 20 | Good |
| 3 | 20 < P <= 40 | Fairly good |
| 4 | 40 < P <= 60 | Fairly poor |
| 5 | 60 < P <= 100 | Poor |
| 6 | P > 100 | Very poor |

Industries/projects may adjust grade intervals for their specific circumstances. Appendix B demonstrates a **different project-specific table**: upper thresholds 2, 15, 30, 50, 80 per mille, with grade 6 above 80. Do not mix those intervals with Chapter 7's suggested intervals.

Appendix B's arithmetic examples, using its own table, are A: N=9075, M=21, L=155, P=17.08 per mille, grade 3; B: N=7354, reported M=25, L=277, P=37.67 per mille, grade 4; C: N=10315, M=25, L=596, P=57.78 per mille, grade 5. The displayed line-count columns sum to the stated L values. **Source discrepancy:** Table B.3 lists R-1-6-3 twice (rows 9 and 12, each eight lines), so its 25 table rows contain only 24 distinct rule IDs. The underlying line sets are absent: it is not possible to establish whether these are separate occurrences, duplicated data, or a mislabeled rule. Preserve the published arithmetic as an illustration, identify the M discrepancy, and do not infer that real assessments may count one rule twice in M or duplicate identical rule/line evidence.

Compute a grade only when the required checked scope, applicable-rule inventory, validated checking capability, confirmed findings, and necessary line data are complete. For focused/partial/manual reviews lacking those prerequisites, report findings and coverage gaps without a conformity score or an extrapolated grade. If presenting arithmetic alone for supplied data, label it as arithmetic under assumptions, not a verified conformity evaluation. Even a low violation rate is not a safety or certification claim.

<a id="validation-requirements"></a>

## Validation requirements

For each use, distinguish language/compiler checks, runtime tests, static-analysis output, and manual GJB interpretation. Do not execute intentionally unsafe counterexamples. Where compilation is possible, build complete test harnesses with the actual language edition, headers, definitions, ABI assumptions, and required target options; a fragment is not a standalone translation unit. Test boundary/failure cases as well as ordinary inputs. Avoid changing product code merely to make an example compile.

When updating this file, check all 204 unique IDs and the 124/28/41/11 family counts against Appendix A, then review every changed rule against the main text, including notes, level, language, exceptions, clause, and page. Check each example's correspondence to its rule and separate source requirements from engineering additions. Preserve section links and source-file identity. Run the available skill-creator structure validator and verify the installed file matches the reviewed staged content. Keep this installation to SKILL.md only; do not create permanent auxiliary references, UI metadata, or reports. Retain the original PDF and remove only task-created temporary artifacts after successful installation.

Behavioral acceptance scenarios:

- An aerospace C array indexed at its extent produces R-1-6-8 with its actual location and impact; a cast alone does not repair it. Floating-to-integer assignment invokes R-1-10-1 and separate representability/rounding checks. A correctly bounded example must not receive a fabricated bounds finding.
- A new[]/delete mismatch invokes R-2-6-2; freeing an interior array pointer invokes R-2-6-3. Shared release and alias rules still apply.
- A polymorphic class with a nonvirtual destructor invokes R-2-3-1. An escaping destructor exception invokes R-2-3-2; related catches in base-before-derived order invoke R-2-8-1. Do not misreport exceptions themselves as prohibited.
- Split template material invokes R-2-9-1 with the physical-file interpretation recorded; typename is advisory under A-2-9-1. Do not invent a ban on templates or RTTI.
- A switch covering every enum member may use R-1-4-6's explicit default exception. A properly annotated empty conditional branch under R-1-4-2 must not be rejected mechanically under A-1-8-1.
- A user specifying GJB 5369-2005 keeps that baseline. Its absent text yields a precise missing-evidence notice and suspended 5369-specific conclusions, never invented 8114-to-5369 numbering. An unavailable source clause is pending, not assumed compliant.
- Ordinary C++, Verilog, and FPGA RTL prompts do not automatically activate this skill. An explicit invocation activates it while retaining language applicability; no C++ rule is applied to Verilog as if it were C++.
- A partial review reports coverage and findings without Chapter 7 grading. Complete supplied counts can support transparent arithmetic, subject to the qualification and scope limitations above.

Preparation validation for this edition: all source pages, main-text rule entries, Appendix A inventory, and Appendix B examples were visually read; OCR served only as a navigation aid. The 204 IDs and four family counts were checked mechanically. The examples and the behavioral scenarios above were reviewed manually. No C/C++ compiler was available on the inspected command path, so this preparation does not claim compiled or runtime-tested examples, independent agent testing, or qualified checker coverage.

<a id="source-record"></a>

## Source record and evidence limits

- Standard: GJB 8114-2013, *Safe subset of C/C++ language programming* (English rendering of the title). Cover records issue 2013-07-10, implementation 2013-10-01, approved by the PLA General Armaments Department. The scan's colophon states first edition and first printing in October 2013. This records the scanned edition, not independently confirmed present-day legal/official status.
- [Retained local source PDF](D:/NCE/giithub/qx/.report_work/gjb8114-alternate.pdf): 157 physical pages, 14,405,650 bytes, SHA-256 `82498AAF0C7E2675334D6DAB590F17CFBC1423DAD7B4C921516B47A1D657D139`. Main printed pages 1-152 map to physical pages 5-156; the colophon is physical page 157. Cover, foreword, contents, Chapters 1-7, and informative appendices were visually inspected.
- Acquisition: [third-party source listing](https://www.kqqw.com/qtbz/226633.html) and its linked download. Content was checked against this scan; authenticity was not confirmed by an official standards publisher. If a project needs an authoritative controlled copy, record that evidence gap and compare the relevant clauses against the supplied authorized copy. Do not invent discrepancies or suspend unrelated verified work.
- A separate three-page Antpedia preview contains cover/contents only and was not used as proof of rule bodies. No GJB 5369-2005 full text was available. Replacement relationships remain open evidence questions.
- This file is an independently written English paraphrase with original examples, not a reproduction of the entire Chinese standard. The scan controls in case of translation ambiguity. Any newly discovered conflict must retain the exact locator and disputed interpretation until resolved.
