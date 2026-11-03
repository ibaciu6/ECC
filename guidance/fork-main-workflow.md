# Fork-main-first workflow for this repo

## Goal
Use only your fork’s `main` branch as the canonical integration branch for this repo.
Keep it up to date with upstream, then stack customizations on top of it.

## Definitions
- `origin/main` — upstream main, used only as a source of new updates.
- `fork/main` — this repo’s own main branch. This is the branch we maintain.
- `fix/*` branches — feature or fix branches that stack custom changes on top of `fork/main`.

## Default update rule
When asked to integrate upstream updates:

1. Fetch latest `origin/main` and `fork/main`.
2. If `fork/main` is behind `origin/main`, update `fork/main` from upstream first.
3. Rebase or merge the active branch onto `fork/main` so custom changes stay on top.
4. Resolve conflicts in favor of keeping both upstream changes and this repo’s custom changes.
5. Verify the result locally before pushing.
6. Push the updated branch to the fork.

Do not make `origin/main` the repo’s maintained branch. Do not replace `fork/main` with upstream history.

## Conflict guidance
- Prefer keeping upstream changes when they touch the same code for the first time and this repo has not customized that area yet.
- Preserve this repo’s custom changes where they represent intentional local behavior.
- If a conflict is unclear, stop and describe the conflicting sections rather than guessing.

## What gets pushed
- Update `fork/main` when upstream needs to be pulled in.
- Push custom branches to the fork separately.
- Keep PRs and branch pushes pointed at the fork, not assumed to land on upstream directly.

## Verification
Before calling work complete on an integration:
- Confirm ancestry: `fork/main` should contain `origin/main` after an upstream sync.
- Confirm custom branch still sits on top of `fork/main`.
- Confirm no leftover merge conflict markers.
- Run whatever quick local checks are reasonable for the changed area.

## Notes
- If a future request explicitly changes this rule, follow the newer instruction.
- If upstream and fork diverge in a way that would force a large history rewrite, say so before rewriting.
