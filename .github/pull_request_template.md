<!-- Title: start with the Jira key, e.g. "KAN-66: add user model". -->

## What and why

<!-- What this PR changes and why. Link the design doc if there is one. -->

## Issue

<!-- Keep one line. Use "Closes" only on the PR for the last subtask of the parent task. -->

Part of #
<!-- Closes # -->

## How to test

1.

## Checklist

- [ ] The branch is named `KAN-<number>-short-description` and every commit starts with the key.
- [ ] `pnpm lint`, `pnpm typecheck` and `pnpm test` pass locally.
- [ ] Schema changes come with a migration (`pnpm db:migrate`).
- [ ] New Zod schemas live in `packages/shared` and are used by both web and api.
- [ ] UI is built from shadcn/ui components. Screenshots are below for visible changes.
- [ ] New env variables are added to the matching `.env.example`.

## Screenshots

<!-- Before and after, for UI changes. Delete this section if there are none. -->
