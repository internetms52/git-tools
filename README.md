# git-tools

A collection of Git helper tools.

## Tools

### [git-unrevert-rebase](./git-unrevert-rebase/README.md)

Rebase helper that detects and undoes revert commits targeting your branch, preventing silent commit loss during rebase.

```bash
git unrevert-rebase main
```

## Installation

Each tool can be installed individually. See the README in each tool's directory for instructions.

For tools that use the shared install path `~/.git-tools/bin`, add this to your shell profile once:

```bash
echo 'export PATH="$HOME/.git-tools/bin:$PATH"' >> ~/.zshrc && source ~/.zshrc
```
bad