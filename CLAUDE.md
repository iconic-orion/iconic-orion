# Branching workflow

- `main` — production-ready. Only merge here via PR once changes are tested and ready to ship.
- `prototype` — experimental / in-progress work. Day-to-day development happens here (or on feature branches off `prototype`).

## Flow

1. Branch off `prototype` for new work: `git checkout -b feature/x prototype`
2. Open PRs into `prototype` for iteration.
3. When `prototype` reaches a stable, shippable state, open a PR from `prototype` → `main`.

## Branch protection (set in GitHub UI)

On `main`:
- Require pull request before merging
- Require status checks to pass
- Disallow direct pushes
