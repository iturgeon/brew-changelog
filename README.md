# brew-changelog

A Homebrew external command that shows changelogs between your currently installed package versions and the latest available versions.

```
brew changelog [formula ...]
```

![Example output showing aws-vault changelog between versions](https://github.com/user-attachments/assets/placeholder)

## Features

- Shows all outdated packages by default, or check specific formulas by name
- Fetches GitHub release notes for each version between what you have and what you'd get
- Falls back to querying npm or PyPI registries to find the GitHub repo when the formula doesn't link to it directly (handles monorepos too)
- Handles monorepo-style release tags (e.g. `pkg@1.2.0`)
- Set `GITHUB_TOKEN` to avoid GitHub API rate limits when checking many packages

## Requirements

- [Homebrew](https://brew.sh)
- [jq](https://jqlang.org) (`brew install jq`)
- Python 3 (included with macOS)

## Installation

### Via Homebrew (recommended)

```sh
brew install iturgeon/tap/brew-changelog
```

> Tap not yet published - use the manual method below.

### Manual

Download and place `brew-changelog` anywhere on your `PATH`. The standard Homebrew bin directory works well:

```sh
curl -fsSL https://raw.githubusercontent.com/iturgeon/brew-changelog/main/brew-changelog \
  -o "$(brew --prefix)/bin/brew-changelog"
chmod +x "$(brew --prefix)/bin/brew-changelog"
```

Homebrew automatically recognizes any `brew-*` executable on your PATH as an external command, so `brew changelog` will work immediately.

## Usage

```sh
# Show changelogs for all outdated packages
brew changelog

# Check one or more specific packages
brew changelog curl git

# Avoid GitHub API rate limits (60 req/hr unauthenticated, 5000 with a token)
GITHUB_TOKEN=ghp_... brew changelog
```

## How it works

1. Runs `brew outdated --json=v2` to find packages with newer versions available
2. For each package, reads the formula's source URL and homepage to find a GitHub repository
3. If neither URL points to GitHub, queries the npm or PyPI registry to locate it
4. Fetches GitHub releases and displays only the entries between your installed version and the latest

Packages that have no GitHub releases and no registry fallback will show their homepage URL instead.

## License

MIT
