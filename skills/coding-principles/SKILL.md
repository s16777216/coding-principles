---
name: coding-principles
description: "Core software development guardrails for AI code generation and modifications. Enforces DRY, KISS, YAGNI, SoC, SOLID, Minimal Change Principle, and Bilingual Documentation rules."
---

# SYSTEM DIRECTIVE: CODE GENERATION & REFACTORING GUARDRAILS

When inspecting, generating, or modifying code, you MUST strictly adhere to the following execution constraints. 

## 1. Execution Scope & Safety Rules

### Minimal Change Principle (Blast Radius Control)
* **STRICT RULE:** You MUST ONLY modify code directly required to fulfill the user's explicit request.
* **FORBIDDEN:** Do NOT perform "incidentally" refactoring, reformatting, or style changes on surrounding code that you were not explicitly asked to touch.
* **FORBIDDEN:** Do NOT rename existing variables, functions, or classes outside the scope of the task.

### YAGNI & KISS (Scope & Complexity)
* **STRICT RULE:** Implement ONLY what is currently requested. Choose the simplest implementation that correctly solves the task.
* **FORBIDDEN:** Do NOT introduce speculative abstractions, generic interfaces, unrequested design patterns, or extra configuration layers for "future expansion."

---

## 2. Architecture & Design Integrity

### DRY (Don't Repeat Yourself)
* Before writing new logic or utility methods, you MUST search the codebase to check if an authoritative function or helper already exists.
* Reuse existing modules instead of duplicating implementation details.

### SoC & SOLID Rules
* **Single Responsibility:** Ensure each modified or created module/function serves exactly one purpose.
* **Layer Isolation:** Keep presentation logic, business rules, and data access strict separated:
  - UI components must NOT contain direct raw API/Database operations or complex data transformations.
  - Controllers/Handlers must NOT execute database queries directly; delegate to services/repositories.

---

## 3. Bilingual Documentation & Context Rules

When writing code comments, variable names, and documentation, follow the **Intent-Driven & Bilingual Context** protocol:

1. **Naming Conventions (Standardized English):**
   - All code identifiers (variables, functions, types, interfaces, classes) MUST use standard, professional English.
   - Core domain business terms MUST adhere strictly to the project's standardized domain glossary. Do NOT create literal translations.

2. **Code Comments (Local Language & Context):**
   - **Code specifies "HOW"; Comments explain "WHY" and "CONTEXT".**
   - Use the local project language (e.g., Traditional Chinese) for code comments when explaining:
     * Complex business logic, edge cases, and regulatory constraints.
     * Special exception handling or workarounds.
   - Do NOT write trivial comments that simply restate what the code does.

---

## 4. Pre-Output Verification Checklist

Before emitting final code edits or file writes, perform this internal sanity check:
1. Did I touch any code unrelated to the requested task? (If YES -> Revert those changes).
2. Did I introduce unnecessary abstractions or generic interfaces? (If YES -> Simplify).
3. Are technical identifiers in standard English and complex business comments in the team's local language? (If NO -> Correct comments/names).
