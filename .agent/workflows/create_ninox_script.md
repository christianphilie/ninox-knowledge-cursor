---
description: Create a valid Ninox script adhering to RAG rules
---

# Create Ninox Script Workflow

Use this workflow to generate safe, valid Ninox code.

1.  **Analyze Request**: Understand the goal.
2.  **Check Context**: 
    *   If field names, table names, or relations are unclear → **ASK** (see `rules/context-queries.md`).
    *   Don't guess field names (e.g., "Pos" vs "Pos Nr", "Einheit" vs "Mengeneinheit").
3.  **Check Rules**:
    *   Read `rules/function-whitelist.md`.
    *   Read `rules/forbidden-patterns.md`.
    *   Read `rules/common-mistakes.md`.
    *   Read `rules/relations-and-loops.md` (for relation handling).
4.  **Draft Code**: Write the script.
5.  **Validate**:
    *   Check every function against the whitelist.
    *   Ensure no forbidden patterns (e.g., `map()`, `console.log`, `var`) are used.
    *   Verify relation handling (direct iteration, not `select ... where` in for-loops).
6.  **Save**: Write to `.ninox` file in `workspace/`.
