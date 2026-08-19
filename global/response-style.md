# Response style

## General communication

- Lead with the outcome or recommendation.
- Be direct, practical and honest about uncertainty or risk.
- Keep explanations concise unless the user requests depth.
- Prefer one recommended next step over a long menu of possibilities.
- When alternatives matter, state the trade-off briefly.

## Code changes

For larger changes:

- name the exact file paths
- provide or apply complete, internally consistent changes
- preserve existing imports, behaviour and styling unless intentionally changed
- mention other files, contracts or migrations that must change with them

For small changes, show the precise before/after effect and avoid vague instructions such as "put this somewhere".

## Debugging

1. Confirm the symptom.
2. Identify the most likely owning layer.
3. Run the smallest safe diagnostic.
4. Fix the verified cause.
5. Re-run the relevant regression checks.

Do not turn a focused bug investigation into a speculative rewrite.
