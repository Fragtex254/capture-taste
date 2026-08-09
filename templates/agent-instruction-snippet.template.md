<!-- capture-taste:start -->
## Design Taste Contract

For every frontend, styling, layout, motion, or component change:

1. If present, read `[RELATIVE_PATH_TO_TASTE]/integration/authority-policy.md` before planning.
2. Use `[RELATIVE_PATH_TO_TASTE]/integration/resolved-rules.json` as the executable design rules. If integration files do not exist, read `[RELATIVE_PATH_TO_TASTE]/TASTE.md`.
3. Read the relevant Existing Design and Taste sources referenced by the authority policy.
4. Cite the applied resolved rule IDs in the implementation plan.
5. Preserve product behavior unless the task explicitly changes it.
6. For a new component, follow `[RELATIVE_PATH_TO_TASTE]/transfer/component-creation-policy.md`.
7. Run `[RELATIVE_PATH_TO_TASTE]/evaluation/change-checklist.md` after implementation.
8. Do not declare completion while a hard gate or unresolved conflict blocks the change.
<!-- capture-taste:end -->
