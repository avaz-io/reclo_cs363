# CI and branch protection

## CI (`.github/workflows/ci.yml`)

GitHub Actions runs on every pull request, on every push to `main`, and by hand from the Actions tab
(Run workflow). There are two jobs:

- **Lint, typecheck, test, build** runs `pnpm lint`, `pnpm typecheck`, `pnpm test` and
  `pnpm build`. It needs no database.
- **Prisma migrations** applies every migration to an empty Postgres 18. It then fails if
  `schema.prisma` has changes that no migration covers. Run `pnpm db:migrate` to add the migration.

Node comes from `.nvmrc` and pnpm from `packageManager` in `package.json`, so CI uses the same
versions as local development. A newer push to the same branch cancels the run in progress.

## Branch protection (`.github/rulesets/main.json`)

A repository ruleset for the default branch (`main`):

- Changes go in through a pull request with 1 approval. A new push dismisses earlier approvals, and
  every review thread must be resolved.
- Both CI jobs must pass, on a branch that is up to date with `main`.
- No force pushes and no deleting `main`.
- Squash and merge commits are allowed. Nobody can bypass the rules, admins included.

### Turning it on

The ruleset JSON does nothing until it is imported. It needs admin access to the repository.

1. Push the workflow first and let it run once on a pull request. GitHub only offers a status check
   in the list after it has seen it run.
2. Go to **Settings → Rules → Rulesets → New ruleset → Import a ruleset** and choose
   `.github/rulesets/main.json`.
3. Check the rules on the page that opens, then click **Create**.

Or, with the GitHub CLI:

```bash
gh api --method POST repos/avaz-io/reclo_cs363/rulesets --input .github/rulesets/main.json
```

To let admins merge in an emergency, add them under **Bypass list** in the ruleset.

On a free plan, rulesets are enforced on public repositories only. On a private repository
without GitHub Team, use **Settings → Branches → Add classic branch protection rule** for `main` with
the same settings instead.
