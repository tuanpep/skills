# Spec Management

## Updating Existing Specs (Refinement Cascade)

When any spec file changes, downstream files must be updated to stay consistent:

**Requirements changed** → Regenerate affected `design.md` sections → Regenerate affected `tasks.md` entries → Show diff summary before writing.

**Design changed** → Validate requirements feasibility → Re-derive affected requirements → Regenerate affected `tasks.md` → Show diff summary.

**Check task progress** → Read codebase against acceptance criteria → Mark implemented tasks `[x]`. Useful when resuming work or onboarding to an existing spec.

Always read the current file before writing an updated version — avoid overwriting user edits.

## Multi-Spec Projects

Unlimited specs per repo, organized by feature. Each spec is independent — teams work on different specs without conflicts.

```
.kiro/specs/
├── user-authentication/    ← Team A
├── product-catalog/        ← Team B
├── shopping-cart/          ← Team A
├── payment-processing/     ← Team C
└── admin-dashboard/        ← Team B
```

Reference specs in conversation with `#spec [spec-name]` to load full context (requirements.md + design.md + tasks.md).
