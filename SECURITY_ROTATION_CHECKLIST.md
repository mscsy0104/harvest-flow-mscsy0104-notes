# Security Rotation Checklist

Use this checklist after repository split or public exposure changes.

## 1) Rotate credentials

- Rotate any GitHub Personal Access Tokens used for CI/deploy.
- Rotate any SSH deploy keys previously used by old repositories.
- Rotate model/provider tokens if they were ever stored in `.env`.

## 2) Re-register repository secrets

Register secrets only in the repository that needs them.

- `GITHUB_TOKEN` permissions: minimum required.
- Deployment secrets: add to `harvest-flow-mscsy0104-notes` only.
- Do not duplicate secrets across `harvest-flow`, `harvest-flow-core`, and `harvest-flow-my` unless necessary.

## 3) Verify local safety

- Keep `.env` out of git.
- Keep runtime data (`data/`, qdrant, logs, sqlite) out of git.
- Run a secret-pattern scan before pushing:
  - `rg -n "(ghp_|github_pat_|AKIA|AIza|xox|BEGIN .* PRIVATE KEY)" .`

## 4) GitHub settings review

- Enable secret scanning and push protection for public repositories.
- Enable branch protection for `main`.
- Limit Actions permissions to least privilege.

