# DataKnifeAI organization branding

Canonical **organization** identity for DataKnifeAI (GitHub org / GitLab group). This repo (`.github`) holds the public org profile README and branding assets. Individual product repos should not redefine org branding.

Repository naming (pipeline layers, descriptive vs evocative, upstream integrations): [NAMING.md](./NAMING.md).

Shared agent baselines for projects: [PROJECT_SETUP.md](./PROJECT_SETUP.md) ([agent-skills](https://github.com/DataKnifeAI/agent-skills), [agent-workspace](https://github.com/DataKnifeAI/agent-workspace)).

## Mission

Learn and solve problems by leveraging AI tools so the work stays maintainable and runs reliably through automation—preferring open software that respects freedom.

## Profile copy (paste-ready)

### Tagline / short description

Use for GitHub **Short description** (and similar short fields). Keep under ~160 characters.

```
Learn and solve problems with AI tools—built to stay maintainable through automation, and aligned with software freedom.
```

### About / mission paragraph

Use for longer About / overview fields.

```
DataKnifeAI is an organization for learning and solving problems with AI tooling.
We put AI to work in ways people can operate and evolve over time: automation carries the repeatable pieces, and we favor boring reliability over fragile cleverness.
When it fits, we prefer open software that preserves user agency.
The org hosts multiple AI-related projects across infrastructure, tooling, and experimentation—not a single product or repository.
```

### Principles

- **Maintainable** — clear structure people can operate and evolve over time
- **Automated** — repeatable workflows over one-off heroics
- **Stable** — boring reliability over fragile cleverness
- **Freedom-respecting** — prefer open and free (as in freedom) software that preserves user agency when it fits

### Name note (optional)

The name nods lightly to Titanfall’s Data Knife—a tool for getting into systems—applied here to AI development rather than game fiction. Keep any mention brief; the org identity is AI work, not game branding.

## Canonical logo assets

All files live under [`profile/assets/`](../profile/assets/).

| File | Size | Use |
|------|------|-----|
| [`dataknifeai-org-logo.png`](../profile/assets/dataknifeai-org-logo.png) | 1024×1024 (~1.2 MB) | Full-resolution source; **profile README header** |
| [`dataknifeai-org-logo-384.png`](../profile/assets/dataknifeai-org-logo-384.png) | 384×384 (~146 KB) | **Recommended** GitHub/GitLab org avatar upload (under 200 KB) |
| [`dataknifeai-org-logo-512.png`](../profile/assets/dataknifeai-org-logo-512.png) | 512×512 (~264 KB) | Larger scaled master (over 200 KB for some upload limits) |

The org profile README displays **only** the 1024×1024 asset. Keep the 384 (and 512) files in-repo for avatar uploads and other scaled uses—do not embed them in `profile/README.md`.

## Set the live profiles

### Text (description / about)

| Platform | Target | Where to paste | Status |
|----------|--------|----------------|--------|
| GitHub | Organization **DataKnifeAI** | https://github.com/organizations/DataKnifeAI/settings/profile — **Short description** = tagline above | Prefer API update when `gh` has `admin:org` (or org admin UI) |
| GitLab | Group **dk-raas/dkai** | https://gitlab.com/groups/dk-raas/dkai/-/edit — **Description** = tagline or short About paragraph | Manual (or `glab` when authenticated) |

**GitHub CLI** (requires org-admin token with permission to update the org):

```bash
gh api -X PATCH orgs/DataKnifeAI \
  -f description='Learn and solve problems with AI tools—built to stay maintainable through automation, and aligned with software freedom.'
```

**GitLab CLI** (when authenticated; group path may vary):

```bash
glab api -X PUT groups/dk-raas%2Fdkai \
  -f description='Learn and solve problems with AI tools—built to stay maintainable through automation, and aligned with software freedom.'
```

If the CLI returns 401/403, paste the tagline (and optional About paragraph) in the web UI using the links above.

### Avatar (manual)

There is no public API to upload org/group avatars via `gh` or `glab`. Upload the PNG in the web UI:

| Platform | Target | Settings |
|----------|--------|----------|
| GitHub | Organization **DataKnifeAI** | https://github.com/organizations/DataKnifeAI/settings/profile |
| GitLab | Group **dk-raas/dkai** | https://gitlab.com/groups/dk-raas/dkai/-/edit |

Upload [`profile/assets/dataknifeai-org-logo-384.png`](../profile/assets/dataknifeai-org-logo-384.png) as the organization/group avatar (not a repository avatar). Prefer this under-200 KB asset for profile upload; keep `dataknifeai-org-logo.png` as the full canonical source and `dataknifeai-org-logo-512.png` if you need a larger scaled master.

### Organization profile README (GitHub)

GitHub renders an org landing README from this public repo: edit **`profile/README.md`**. Images in that README must use absolute URLs (e.g. `raw.githubusercontent.com`).

**Maintain:**

1. Clone or PR against https://github.com/DataKnifeAI/.github
2. Update `profile/README.md` (mission/tagline should stay aligned with the Profile copy above)
3. Keep the header image pointed at `profile/assets/dataknifeai-org-logo.png` (1024×1024 only—do not switch the README to the 384 asset)
4. Open a PR into `main` — after merge, https://github.com/DataKnifeAI shows the new profile

### Group profile README (GitLab)

GitLab renders the group overview README from **`gitlab-profile/README.md`** (mirrored to project `dk-raas/dkai/gitlab-profile`). Group overview image paths can fail with relative links—use an absolute raw URL to the 1024 asset:

`https://gitlab.com/dk-raas/dkai/gitlab-profile/-/raw/main/assets/dataknifeai-org-logo.png`

Keep that header pointed at the 1024 file only (not the 384 avatar asset). Assets sync from `profile/assets/` → GitLab `assets/` via the mirror workflow.
