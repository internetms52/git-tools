# git-unrevert-rebase

Rebase helper that detects and undoes reverts targeting your branch.

## The Problem

When a feature branch is merged into `main` and then reverted, rebasing the feature branch onto `main` will silently drop your changes.

This happens because Git uses patch equivalence to decide which commits to apply during rebase. Since the revert on `main` cancels out your feature branch changes, Git considers those commits already applied and skips them.

```
main:    C1 - C2 - M - C3 - R       (R reverts M, which contained your changes)
                   ↑
feature:          F1 - F2            (after rebase onto main, F1 and F2 disappear)
```

The standard fix is to manually revert R before rebasing, but this is easy to forget and error-prone in a team environment.

## What This Tool Does

Before rebasing, `git-unrevert-rebase` scans the upstream branch for any revert commits that target your current branch. If found, it automatically applies a revert-of-revert, then proceeds with the rebase as normal.

## Limitations

- Squash merge detection requires the squash commit message to contain a `squash-source-sha: <hash>` line pointing back to the original feature branch commit. Without this, squash-merged branches cannot be detected.

## Installation

**macOS / Linux**

```bash
mkdir -p ~/.git-tools/bin && \
curl -o ~/.git-tools/bin/git-unrevert-rebase https://raw.githubusercontent.com/internetms52/git-tools/main/git-unrevert-rebase/git-unrevert-rebase && \
chmod +x ~/.git-tools/bin/git-unrevert-rebase && \
echo 'export PATH="$HOME/.git-tools/bin:$PATH"' >> ~/.zshrc && \
source ~/.zshrc
```

**Windows (Git Bash)**

```bash
mkdir -p ~/.git-tools/bin && \
curl -o ~/.git-tools/bin/git-unrevert-rebase https://raw.githubusercontent.com/internetms52/git-tools/main/git-unrevert-rebase/git-unrevert-rebase && \
chmod +x ~/.git-tools/bin/git-unrevert-rebase && \
echo 'export PATH="$HOME/.git-tools/bin:$PATH"' >> ~/.bashrc && \
source ~/.bashrc
```

## Usage

```bash
git unrevert-rebase main
```

## License

MIT