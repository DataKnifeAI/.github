# DataKnifeAI repository settings

Recommended **common pattern** for first-party (non-fork) repositories in the [DataKnifeAI](https://github.com/DataKnifeAI) organization.

Aligned with the org mission: keep work **maintainable**, **automated**, and **stable**, and prefer setups that stay operable without one-off heroics. See [`ORG_BRANDING.md`](ORG_BRANDING.md) for identity and principles.

Related: agent skills / Cloud Agent workspace baseline — [`PROJECT_SETUP.md`](https://github.com/DataKnifeAI/.github/pull/5) (PR; path `docs/PROJECT_SETUP.md` after merge).

This document describes the **target** state. Existing repos may drift; prefer fixing settings intentionally (new repos first, then high-traffic product repos) rather than bulk-changing everything at once.

## Scope

| Kind | Apply this pattern? |
|------|---------------------|
| First-party product / infra / tooling repos | Yes |
| Org meta repo (`.github`) | Yes (docs live in-repo; keep the surface small) |
| Private repos on free GitHub plans | Apply what the plan allows; classic branch protection / rulesets may be unavailable |
| Forks of upstream projects | Partial — see [Forks](#forks) |

Org-level rulesets (if enabled later) should encode the same defaults so new repos inherit them. As of the last review, org rulesets were not readable without `admin:org` scope; do not assume they are configured.

## New repository defaults

Use these when creating a repo (UI or `gh repo create` / `gh repo edit`).

| Setting | Recommended | Notes |
|---------|-------------|--------|
| Default branch | `main` | Already universal across first-party repos |
| Issues | **On** | Track work in the owning repo unless there is a deliberate hub |
| Projects | On (optional) | Harmless default; use org/user projects if preferred |
| Wiki | **Off** | Prefer Markdown in the repo (`README` / `docs/`) so docs version with code |
| Downloads | Off | Legacy “Downloads” tab; unused |
| Squash merge | **On** (preferred path) | Keeps `main` readable; matches linear-history protection |
| Merge commit | On or off | Optional; squash is the default contributor path |
| Rebase merge | On or off | Optional |
| Delete branch on merge | **On** | Avoids stale head branches |
| Auto-merge | Optional | Useful once required checks exist; not required |
| Allow force push / branch deletion on default | **Off** | Enforced via protection / rulesets |

Example:

```bash
gh repo edit DataKnifeAI/<repo> \
  --default-branch main \
  --enable-issues \
  --enable-projects \
  --enable-squash-merge \
  --delete-branch-on-merge \
  --allow-update-branch
# Disable wiki when the API/UI allows (GitHub has no universal --disable-wiki flag on all gh versions).
```

## Default branch protection / rulesets

Protect `main` (the default branch) on every **public** first-party repo that accepts contributions or automation.

### Classic branch protection (common today)

Target shape:

| Rule | Recommended |
|------|-------------|
| Require a pull request before merging | **Yes** |
| Required approving reviews | **1** when more than one active maintainer; **0** is acceptable for solo-maintainer repos if a PR is still required |
| Dismiss stale reviews | **Yes** |
| Require review from Code Owners | Only if a `CODEOWNERS` file exists and is kept accurate |
| Require conversation resolution | **Yes** |
| Require linear history | **Yes** (pairs with squash-or-rebase) |
| Require status checks to pass | **Yes when CI exists** — name the checks that gate quality (see [github-workflows](#relation-to-github-workflows)) |
| Require branches to be up to date | **Yes** (`strict`) when checks are configured |
| Do not allow force pushes | **Yes** (deny) |
| Do not allow deletions | **Yes** (deny) |
| Include administrators | **Yes** (`enforce_admins`) so the same path applies to everyone |

Empty required-check lists with “strict” up-to-date only are a weak gate. Prefer either real check names or omitting required checks until CI is wired.

### Rulesets (optional overlay)

Repository rulesets are fine for additive policy (for example Copilot code review on the default branch, block force-push / deletion). Prefer **one clear story**: either classic protection plus a small ruleset overlay, or a single ruleset that encodes the same intent. Avoid duplicating conflicting review requirements.

## Dependabot and security basics

| Control | Recommended |
|---------|-------------|
| Dependabot version updates | Enable `.github/dependabot.yml` for ecosystems the repo actually uses (`gomod`, `pip`, `npm`, `docker`, `github-actions`, `terraform`, …) on a weekly cadence |
| Vulnerability alerts / Dependabot security updates | **On** for first-party repos |
| Secret scanning / push protection | On where GitHub enables them for the visibility/plan |
| `CODEOWNERS` | Optional; add when ownership is stable enough that review routing helps |

Do not add Dependabot ecosystems “for completeness” in repos with no lockfile or package manifest.

## Forks

Forks exist to track or contribute upstream. They intentionally differ:

- **Issues off** (typical) — avoid splitting reports away from upstream
- Default branch may remain upstream’s (`main` or `master`)
- Do **not** force org branding, org issue templates, or full product protection onto forks unless the fork is permanently diverged into a first-party product
- Merge / delete-branch settings may stay loose; treat the fork as a mirror or contribution staging area

When a fork becomes a long-lived DataKnifeAI product, graduate it: enable issues, adopt `main` if needed, and apply this document’s first-party pattern.

## Relation to `github-workflows`

Reusable CI lives in [`DataKnifeAI/github-workflows`](https://github.com/DataKnifeAI/github-workflows) (`workflow_call` workflows and composite actions).

- Caller repos should **pin a tag** (for example `@v1`), not floating `@main`, once a release line is stable.
- After a consumer wires reusable workflows, add those job/check names to **required status checks** on `main` so automation actually gates merges.
- Mirror / security reusable workflows (GitLab push, Trivy, game-server verify) are opt-in per repo; protection should only require checks that the repo runs.

Settings keep the branch **stable**; reusable workflows keep verification **automated** and consistent across consumers.

## Alignment snapshot (review notes)

Observed across org-owned non-fork repos (representative audit; not a live dashboard):

**Mostly aligned**

- Default branch `main`
- Issues and projects enabled
- All three merge strategies enabled; downloads off
- Many public repos share classic protection: PR required, dismiss stale reviews, linear history, conversation resolution, enforce admins, no force push / no branch deletion
- No `CODEOWNERS` files in sampled repos (consistent absence)

**Common drift (fix toward this doc)**

| Area | Drift |
|------|--------|
| Wiki | Off on some older product repos; still on for many others (prefer off) |
| Delete branch on merge | On for an older core set (and `.github`); **off** on many newer repos |
| Auto-merge | Enabled only on an outlier (`high-command-mcp`) |
| Branch protection | **Missing** on several newer public repos (operators / related) and on `.github` |
| Required reviews | Often **0** approvals (PR still required); scripted intent elsewhere was 1 |
| Required status checks | Strict up-to-date with **empty** check lists on protected repos |
| Rulesets | Only a few repos (High Command) have a Copilot-review ruleset |
| Dependabot config | Present on a small minority |
| Vulnerability alerts | On for many newer repos; still off on a large older set |
| Private repos | Branch protection / rulesets blocked without a paid plan feature |

Forks (separate): issues disabled; some default to `master`; not held to the first-party checklist.

## Applying changes safely

1. Set **new** repos to this pattern at creation time.
2. For existing repos, change settings in small batches; verify CI check names before requiring them.
3. Prefer documenting intent here over silent bulk edits across the org.
4. Private repos: enable whatever the plan allows; consider public + careful secrets hygiene, or a plan that includes protection, for repos that need hard gates.

```bash
# Example: align merge hygiene on one repo
gh repo edit DataKnifeAI/<repo> --enable-squash-merge --delete-branch-on-merge

# Example: enable vulnerability alerts
gh api -X PUT "repos/DataKnifeAI/<repo>/vulnerability-alerts" -H "Accept: application/vnd.github+json"
```
