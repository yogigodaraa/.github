# Contributing

Thanks for taking a look. These are solo projects, but issues and PRs are welcome.

## Workflow

1. **Open an issue first** for anything bigger than a typo, so we can agree on the approach.
2. **Branch** off `main`: `git switch -c feat/short-description` (or `fix/…`, `docs/…`, `chore/…`).
3. **Commit small.** One concern per commit. Conventional-commit style messages
   (`feat:`, `fix:`, `docs:`, `chore:`) are preferred but not required.
4. **Open a PR** against `main` and fill in the template.
5. **CI must pass.** PRs are squash-merged, and the PR title becomes the commit message,
   so make it descriptive.

`main` is protected: no direct pushes, no force pushes.

## Before you push

- Run the project's own checks locally (see its README: usually `npm run lint && npm test`
  or `ruff check . && pytest`).
- **Never commit secrets.** Use `.env` (git-ignored) and keep `.env.example` up to date
  with placeholder values only.
- Don't commit build output, `node_modules/`, virtualenvs, `__pycache__/` or real datasets.

## Merge conflicts

If your branch conflicts with `main`:

```bash
git fetch origin
git rebase origin/main      # fix conflicts file by file, then:
git add <file> && git rebase --continue
git push --force-with-lease # only ever on your own branch
```

## Code of conduct

By participating you agree to the [Code of Conduct](CODE_OF_CONDUCT.md).
