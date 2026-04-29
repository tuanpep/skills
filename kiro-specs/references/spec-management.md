# Spec management (caveman)

## Update cascade
- If `requirements.md` changes -> update affected `design.md` -> update affected `tasks.md`.
- If `design.md` changes -> recheck req feasibility -> update affected `tasks.md`.
- If checking progress -> compare code vs acceptance -> mark done `[x]`.

Read current file before overwrite. Protect user edits.

## Multi-spec
- One folder per feature/bug under `.kiro/specs/`
- Specs independent. Coordinate only shared modules/contracts.
- Load specific spec context with `#spec [name]`.
