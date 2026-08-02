# DataKnifeAI GitLab project settings

Recommended **common pattern** for first-party projects under [dk-raas/dkai](https://gitlab.com/dk-raas/dkai).

Parallel to GitHub [REPO_SETTINGS](https://github.com/DataKnifeAI/.github) (branch protection → GitLab protected branches / MR approvals). Solo-maintainer defaults: safe and automatable, not multi-reviewer gates.

Related: [ORG_BRANDING.md](./ORG_BRANDING.md), [PROJECT_SETUP.md](./PROJECT_SETUP.md).

## Scope

| Kind | Apply? |
|------|--------|
| First-party product / infra / tooling | Yes |
| This meta project (`gitlab-profile`) | Yes (keep surface small) |
| Pull mirrors of GitHub (read-mostly) | Partial — protect `main`; avoid fighting the mirror job |
| Forks of upstream | Partial — don’t impose org branding onto upstream identity |

Group already sets a baseline (`default_branch_protection` ≈ Maintainer push/merge, force-push off). Per-project settings below sharpen that for active repos.

## New project defaults

| Setting | Recommended | Notes |
|---------|-------------|--------|
| Default branch | `main` | Match GitHub |
| Visibility | Public for first-party mirrors | Private only when needed |
| Issues | **On** (if using GitLab issues) | Many projects track on GitHub — either is fine; don’t split casually |
| Wiki | **Off** | Prefer Markdown in-repo (`README` / `docs/`) |
| Squash commits when merging | **On** (preferred) | Linear, readable `main` |
| Merge commit / fast-forward | Optional | Squash is the default contributor path |
| Delete source branch on merge | **On** | Avoids stale branches |
| Auto-merge | Optional | Useful once CI is reliable |

```bash
# Example (project path URL-encoded)
glab api -X PUT projects/dk-raas%2Fdkai%2Fdevops%2Francher-deploy \
  -f default_branch=main \
  -f issues_enabled=true \
  -f wiki_enabled=false \
  -f squash_option=default_on \
  -f remove_source_branch_after_merge=true
```

## Protected branches (solo-dev defaults)

Protect `main` on every active first-party project.

| Rule | Recommended (solo) | GitLab mapping |
|------|--------------------|----------------|
| No force push to default | **Yes** | Protected branch → Allowed to force push: No |
| No delete default branch | **Yes** | Protected branch default |
| Who can push | Maintainers (or “No one” + MR-only) | Prefer **Allowed to push: No one** + merge via MR when not a pure mirror |
| Who can merge | Maintainers | Allowed to merge: Maintainers |
| Require MR | **Yes** for human work | Code changes via MR even for solo |
| Required approvals | **0** | Do not require 1+ until a second person exists |
| Code Owner approval | **Off** | Enable only with real `CODEOWNERS` + >1 reviewer |
| Resolve discussions | Optional | “All threads must be resolved” is fine |
| Pipeline must succeed | **Only when CI is reliable** | Don’t require empty/flaky pipelines |

Pure GitHub→GitLab **pull mirrors**: keep `main` protected against casual force-push by humans; allow the mirror/service account what it needs. Don’t layer “required approvals” on automated mirror updates.

### When the group grows

| Change | Target |
|--------|--------|
| Required approvals | **1+** |
| CODEOWNERS | Add and optionally require |
| Push access | Tighten further (MR-only for everyone including maintainers if desired) |
| Group push rules / compliance | Encode shared floor for new projects |

## Group-level controls (optional later)

| Capability | When to use |
|------------|-------------|
| Group push rules | Commit message / branch name conventions org-wide |
| Group CI/CD variables | Shared non-secret defaults; secrets still least-privilege per project |
| Compliance frameworks | Only if you adopt GitLab Ultimate compliance workflows |
| Group file templates / project templates | Shared `.gitlab-ci.yml` / LICENSE / SECURITY templates — use a dedicated template project if needed |
| Instance/group runners | Prefer project or group runners you control for Harbor/k8s jobs |

Do **not** invent a parallel `github-workflows` stack on GitLab unless GitLab CI becomes a primary path. Mirrors may carry `.gitlab-ci.yml` opportunistically.

## Out of scope

- Bulk-rewriting every mirrored project overnight.
- Cursor skills / Cloud Agent baselines — see [PROJECT_SETUP.md](./PROJECT_SETUP.md) (GitHub-canonical).
