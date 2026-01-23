---
name: Ninox Scripting
description: Expert knowledge for scripting in Ninox databases, preventing hallucinations and enforcing project rules.
---

# Ninox Scripting Skill

This skill MUST be used whenever the user asks to write, debug, or explain Ninox scripts (NX).

## ⚠️ CRITICAL RULES

You must strictly follow the project's RAG rules to avoid "hallucinations" (inventing functions that don't exist).

1.  **ALWAYS** read `rules/function-whitelist.md` before writing code. If a function is not in that list, **DO NOT USE IT** unless you verify it in the official docs yourself.
2.  **ALWAYS** read `rules/forbidden-patterns.md` to avoid common mistakes (like using JS Array methods `map`, `filter`, etc. which do NOT exist in Ninox).
3.  **CONTEXT QUERIES**: If field names, table names, or relations are unclear, **ASK** instead of guessing. See `rules/context-queries.md`.
4.  **CONSULT ALL RULES**: Review all relevant documents in the `rules/` directory before writing code. See Resources section below for all available rule documents.

## Resources

*   [Function Whitelist](rules/function-whitelist.md)
*   [Forbidden Patterns](rules/forbidden-patterns.md)
*   [Common Mistakes](rules/common-mistakes.md)
*   [Context Queries](rules/context-queries.md) - When to ask instead of guessing
*   [Relations and Loops](rules/relations-and-loops.md) - Correct usage of relations and for-loops
*   [Performance Rules](rules/performance-rules.md)
*   [Undocumented Features](rules/undocumented-features.md)
*   [Style Guide](rules/style-guide.md)
