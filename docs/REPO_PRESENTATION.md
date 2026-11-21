# Repository presentation checklist

Short checklist for how a DataKnifeAI product repo presents itself on GitHub. Branding copy and naming rules live elsewhere — do not redefine org identity here.

Related: [ORG_BRANDING](./ORG_BRANDING.md), [NAMING](./NAMING.md), [PROJECT_SETUP](./PROJECT_SETUP.md), [REPO_SETTINGS](./REPO_SETTINGS.md).

## Checklist

| Item | Target |
|------|--------|
| **GitHub description** | Role + purpose, ≤ ~160 characters (same length budget as the org short description in [ORG_BRANDING](./ORG_BRANDING.md)) |
| **Topics** | Capability and stack per [NAMING](./NAMING.md) (`mcp`, `kubernetes`, `agents`, `gitops`, …) — not every dependency; upstream topics only when discovery for that integration is a primary goal |
| **README lead** | Lead with what DataKnifeAI owns / the product job; integrations are secondary |
| **Hero graphic** | `docs/assets/<repo>-hero.jpg` or `.png`, embedded as the **first** image in the README when the repo has public-facing docs |

## Notes

- Description and topics follow the “Topics and descriptions” / decision checklist in [NAMING](./NAMING.md).
- Hero path and “README leads with product job” also appear in the org Cursor rule ([`dataknifeai-common.mdc`](https://github.com/DataKnifeAI/agent-skills/blob/main/rules/dataknifeai-common.mdc)); keep product READMEs aligned when you touch them.
- Org logo / profile assets stay in this `.github` repo — product heroes are per-repo under `docs/assets/`.
