---
name: karpathy-guidelines-codex
description: Use when Codex is writing, reviewing, debugging, refactoring, or simplifying code and should bias toward compact, explicit, readable engineering choices inspired by Andrej Karpathy's coding style.
---

# Karpathy Guidelines

## Overview

Use these guidelines as a lightweight engineering style check before and during coding work. The goal is code that is easy to read, easy to debug, and hard to misunderstand.

This skill adapts the public Karpathy Guidelines skill for Codex. Preserve project conventions and user instructions first; apply these rules where they improve the local codebase.

Source inspiration: https://github.com/forrestchang/andrej-karpathy-skills

## Core Rules

1. Keep control flow simple.
   Prefer straight-line code, small functions, explicit branches, and local reasoning. Avoid clever abstractions, deep nesting, metaprogramming, or framework magic unless the existing project clearly depends on them.

2. Optimize for readability before reuse.
   Do not extract helpers just because two blocks look similar. Extract only when it gives the code a better name, isolates a real concept, or removes duplication that is already making changes risky.

3. Make state and data movement visible.
   Prefer explicit inputs, outputs, and transformations. Avoid hidden global state, mutation from distant call sites, implicit registries, and action-at-a-distance side effects.

4. Write code that is easy to inspect in a debugger.
   Use named intermediate values when they clarify intent. Avoid dense one-liners, chained transformations, or nested expressions that hide important failure points.

5. Prefer boring dependencies and local patterns.
   Use the repository's existing stack and helpers. Add new dependencies or architectural patterns only when they remove meaningful complexity.

6. Keep failure behavior concrete.
   Check edge cases where data enters the system. Return or raise clear errors. Avoid broad catches, silent fallbacks, and ambiguous defaults.

## Working Pattern

Before editing:
- Identify the smallest behavior or code path that needs to change.
- Read the surrounding code and copy its style unless it is actively causing the problem.
- If the task changes behavior, use the project's normal test workflow before implementation.

While editing:
- Make the smallest coherent change.
- Prefer explicit names over comments. Add comments only for non-obvious tradeoffs or constraints.
- Stop when the requested behavior works; do not broaden the refactor without a clear reason.

Before finishing:
- Re-read the diff as if debugging it at 2 AM.
- Remove accidental cleverness, dead paths, unnecessary abstractions, and vague names.
- Verify with the narrowest meaningful command, then broader checks when the blast radius warrants it.

## Review Checklist

Ask these questions before claiming the work is done:

| Question | If the answer is no |
| --- | --- |
| Can a reader understand the main path without jumping across many files? | Inline the path or improve the boundary. |
| Are data inputs, outputs, and mutations visible? | Make dependencies explicit. |
| Is each abstraction carrying real conceptual weight? | Delete or collapse it. |
| Would the failure mode be obvious from logs, errors, or tests? | Add concrete handling or coverage. |
| Did the change follow local conventions? | Align it unless there is a stated reason not to. |

## Common Mistakes

- Turning guidelines into a blanket ban on abstractions. Good abstractions are welcome when they make the system smaller and clearer.
- Rewriting working local style into a personal style. Consistency with the repository matters more than aesthetic preference.
- Hiding complexity behind generic helpers. If a helper name is vague, the abstraction is probably vague.
- Skipping tests because the change is "just cleanup." Refactors need verification because behavior should not move.
- Over-commenting obvious code. Prefer clear names and structure; comments should explain why, not restate what.

## Conflict Resolution

When instructions conflict, use this order:

1. User's explicit request.
2. Repository and project instructions.
3. Safety, correctness, and test requirements.
4. These guidelines.

Do not use this skill to override a user's requested architecture or a project's established patterns. Use it to make the chosen approach simpler, clearer, and easier to maintain.
