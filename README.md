# .github
Organization-wide GitHub community health files and templates for QOAX repositories

## Commit messages

Commits follow [Conventional Commits](https://www.conventionalcommits.org/en/v1.0.0/). A shared `commit-msg` hook checks the message before the commit is written, and the same check runs in CI on every pull request.

Git hooks are local configuration, so a fresh clone has nothing enabled. Turn it on once per clone:

```sh
sh scripts/setup-hooks.sh
```

The script is safe to run again. It only points `core.hooksPath` at `.githooks`. The hook in that folder, `.githooks/commit-msg`, is a tracked copy of the [qoax-githooks](https://github.com/qoax-community/qoax-githooks) hook.

Two things worth knowing:

- On macOS the hook needs bash 4+, which means `brew install bash`. Without it the commit is written unchecked with a warning, and only CI catches a bad message.
- The CI check pins a release of qoax-githooks by commit sha. It compares `.githooks/commit-msg` with the hook of that release. Dependabot opens a pull request to move the pin. If the release changes the hook, a sync commit in that pull request updates the copy. After the merge, `git pull` gives you the new hook. For details, see [Versions](https://github.com/qoax-community/qoax-githooks#versions) in the qoax-githooks README.

`git commit --no-verify` skips the hook. The pull request check is not optional.
