# AGENTS.md

Baseline operating rules for coding agents across all repositories.
Keep this file short and enforceable. Project-specific rules live in each repo's `AGENTS.md` and override this file when more specific.

## 1. Scope and authority

- This file is the default rulebook for all repos.
- If a repo has its own rules, follow the repo rules first and note any conflict.
- Do not change the project's stack (language/framework/build/package manager) unless explicitly asked.

## 2. Core operating rules

- Discover the repo before changing code: read `README`, `CONTRIBUTING`, and any docs or CI configs.
- Prefer the repo's existing tools and scripts; do not add new linters, formatters, or test frameworks without asking.
- Keep diffs small and focused. Avoid drive-by refactors.
- No secrets in commits. If a secret is found, stop and report it.
- Maintain consistent code style and patterns used in the repo.
- Update repo docs when behavior changes.
- If `pnpm-lock.yaml` exists, use `pnpm` and a frozen lockfile in CI.

## 3. Workflow (simple, repeatable)

1. Intake: restate goal, constraints, and success criteria.
2. Discovery: identify stack, run commands, tests, and linting.
3. Plan: list steps and files likely to change.
4. Implement: minimal changes first; isolate mechanical edits.
5. Verify: run existing checks or document why they were not run.
6. Report: summarize changes and verification results.

## 4. Git workflow (beginner-friendly)

- Default model: `main` + short-lived `feature/*` branches.
- Do not commit directly to `main`.
- Branch naming: `feature/<short-kebab-summary>` (e.g., `feature/add-login-form`).
- Commit messages should be clear and specific. Use conventional commits if the repo already uses them.
- PRs are recommended. If working solo without PRs, do a quick self-review before merging.

## 5. Verification rules (strict but practical)

- For behavior changes or bug fixes, add or update tests when feasible.
- Always run the repo's existing checks, matching CI when possible (including e2e if CI runs it).
- If a required check cannot be run, state why and provide manual verification steps.
- Verification reporting is mandatory in the final response and PR/MR body.

Example reporting:

```markdown
## Verification
- ✅ `pnpm test`
- ✅ `pnpm lint`
- ⚠️ Not run: `pnpm build` (not configured in repo)

## Manual checks
- ✅ Started dev server and verified `/health` returns 200
```

## 6. Project modes

Each repo's `AGENTS.md` can define a `Mode` to adjust behavior. Examples:

- `MVP` mode: prioritize speed and core functionality.
- `Harden` mode: prioritize tests, error handling, and safety.
- `Refactor` mode: prioritize structure and maintainability.

If a repo defines a mode, follow it.

## 7. Stop conditions

Stop and ask the user if any of these occur:

- The request conflicts with repo rules.
- The change risks data loss or breaking changes without a rollback plan.
- A security issue is discovered that requires coordinated response.
- Required verification cannot be run and risk is unclear.

## 8. Quick discovery commands (optional)

```sh
ls
rg --files -g "README*" -g "CONTRIBUTING*"
rg --files -g "*.yml" -g ".github/workflows/*"
rg -n "\"(test|lint|build|typecheck)\"" package.json
```
