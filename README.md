# .github
Organization-wide GitHub community health files and templates for QOAX repositories

## Commit messages

Commits follow [Conventional Commits](https://www.conventionalcommits.org/en/v1.0.0/). A shared `commit-msg` hook checks the message before the commit is written, and the same check runs in CI on every pull request.

Git hooks are local configuration, so a fresh clone has nothing enabled. Turn it on once per clone:

```sh
sh scripts/setup-hooks.sh
```

The script is safe to run again, and it checks out the [qoax-githooks](https://github.com/qoax-community/qoax-githooks) submodule under `.githooks/shared` itself if the clone left it empty.

Two things worth knowing:

- On macOS the hook needs bash 4+, which means `brew install bash`. Without it the commit is written unchecked with a warning, and only CI catches a bad message.
- Dependabot moves the submodule pin forward as the hook changes. `git config --global submodule.recurse true` makes `git pull` follow it; otherwise you keep running the version you first cloned.

`git commit --no-verify` skips the hook. The pull request check is not optional.
