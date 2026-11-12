# Git rules
- Commit, push or open pull requests only when asked
- If on the default branch, create a branch first: `type/short-description` (`feat/`, `fix/`, `chore/`, `docs/`)
- Commit messages follow Conventional Commits: `type(scope): summary`, imperative, 72 characters or fewer; the body explains why
- One logical change per commit; don't mix refactoring with behaviour changes
- Check `git status` and the diff before committing; never commit unrelated files, build output or secrets
- Never force-push, rewrite published history or skip hooks without asking