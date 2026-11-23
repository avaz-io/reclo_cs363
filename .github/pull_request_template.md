From 8401026ebef4cbdc69c10d77afb87419d0353c8b Mon Sep 17 00:00:00 2001
From: avaz-io <asoibnazarov2005@gmail.com>
Date: Mon, 23 Nov 2026 16:49:31 +0500
Subject: [PATCH] Add feature, bugfix and CI pull request templates

---
 .github/PULL_REQUEST_TEMPLATE/bugfix.md  | 26 +++++++++++++++++++
 .github/PULL_REQUEST_TEMPLATE/ci.md      | 24 +++++++++++++++++
 .github/PULL_REQUEST_TEMPLATE/feature.md | 33 ++++++++++++++++++++++++
 .github/pull_request_template.md         |  3 +++
 4 files changed, 86 insertions(+)
 create mode 100644 .github/PULL_REQUEST_TEMPLATE/bugfix.md
 create mode 100644 .github/PULL_REQUEST_TEMPLATE/ci.md
 create mode 100644 .github/PULL_REQUEST_TEMPLATE/feature.md

diff --git a/.github/PULL_REQUEST_TEMPLATE/bugfix.md b/.github/PULL_REQUEST_TEMPLATE/bugfix.md
new file mode 100644
index 0000000..2c31d19
--- /dev/null
+++ b/.github/PULL_REQUEST_TEMPLATE/bugfix.md
@@ -0,0 +1,26 @@
+<!-- Title: start with the Jira key, e.g. "KAN-78: fix the language switcher label". -->
+
+## Bug
+
+<!-- What was broken and how to see it on main before this PR. -->
+
+Fixes #
+
+## Cause
+
+<!-- Why it happened. -->
+
+## Fix
+
+<!-- What this PR changes to stop it. -->
+
+## How to verify
+
+1.
+
+## Checklist
+
+- [ ] The branch is named `KAN-<number>-short-description` and every commit starts with the key.
+- [ ] A test fails without this fix and passes with it.
+- [ ] `pnpm lint`, `pnpm typecheck` and `pnpm test` pass locally.
+- [ ] The diff only touches what the bug needs, with no unrelated refactoring.
diff --git a/.github/PULL_REQUEST_TEMPLATE/ci.md b/.github/PULL_REQUEST_TEMPLATE/ci.md
new file mode 100644
index 0000000..12345d9
--- /dev/null
+++ b/.github/PULL_REQUEST_TEMPLATE/ci.md
@@ -0,0 +1,24 @@
+<!-- Title: start with the Jira key, e.g. "KAN-80: cache the Prisma engines in CI". -->
+<!-- Use this template for CI, rulesets, Docker, scripts, dependencies and repository settings. -->
+
+## What changes
+
+## Why
+
+## What the team has to do after the merge
+
+<!-- e.g. run `pnpm install`, run a migration, change a GitHub setting. Write "Nothing" if so. -->
+
+## How it was tested
+
+- [ ] The CI run on this PR is green.
+
+## Checklist
+
+- [ ] The branch is named `KAN-<number>-short-description` and every commit starts with the key.
+- [ ] Job names in `.github/workflows/ci.yml` still match the required checks in
+      `.github/rulesets/main.json`.
+- [ ] New dependencies with install scripts are approved under `allowBuilds` in
+      `pnpm-workspace.yaml`.
+- [ ] No secrets in the diff. Secrets go in GitHub Actions secrets.
+- [ ] `docs/ci.md` or the README is updated if a command or setting changed.
diff --git a/.github/PULL_REQUEST_TEMPLATE/feature.md b/.github/PULL_REQUEST_TEMPLATE/feature.md
new file mode 100644
index 0000000..5ea5ef6
--- /dev/null
+++ b/.github/PULL_REQUEST_TEMPLATE/feature.md
@@ -0,0 +1,33 @@
+<!-- Title: start with the Jira key, e.g. "KAN-66: add user model". -->
+
+## What and why
+
+<!-- The change a client, vendor or admin will notice, and why it is needed. -->
+
+Design doc: `docs/<feature>-design.md`
+
+## Issue
+
+<!-- Keep one line. Use "Closes" only on the PR for the last subtask of the parent task. -->
+
+Part of #
+
+<!-- Closes # -->
+
+## How to test
+
+1.
+
+## Checklist
+
+- [ ] The branch is named `KAN-<number>-short-description` and every commit starts with the key.
+- [ ] `pnpm lint`, `pnpm typecheck` and `pnpm test` pass locally.
+- [ ] New behaviour has tests (Vitest in web and api, Supertest for API routes).
+- [ ] Schema changes come with a migration (`pnpm db:migrate`).
+- [ ] New Zod schemas live in `packages/shared` and are used by both web and api.
+- [ ] UI is built from shadcn/ui components. New strings are in the en, uz and ru catalogs.
+- [ ] New env variables are added to the matching `.env.example`.
+
+## Screenshots
+
+<!-- Before and after for visible changes. Delete this section if there are none. -->
diff --git a/.github/pull_request_template.md b/.github/pull_request_template.md
index ab3bdc9..a427112 100644
--- a/.github/pull_request_template.md
+++ b/.github/pull_request_template.md
@@ -1,4 +1,6 @@
 <!-- Title: start with the Jira key, e.g. "KAN-66: add user model". -->
+<!-- Other templates: add `&template=feature.md`, `bugfix.md` or `ci.md` to the compare URL, or
+     pick one in `gh pr create`. They live in .github/PULL_REQUEST_TEMPLATE/. -->
 
 ## What and why
 
@@ -9,6 +11,7 @@
 <!-- Keep one line. Use "Closes" only on the PR for the last subtask of the parent task. -->
 
 Part of #
+
 <!-- Closes # -->
 
 ## How to test
-- 
2.43.0