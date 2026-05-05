# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [0.1.0] - 2026-05-05

### Added

- Initial release
- `brew changelog` external command - shows changelogs for all outdated Homebrew packages
- Optional per-package mode: `brew changelog curl git` checks specific formulas
- GitHub releases fetched between installed version and latest, showing only relevant entries
- Colored, readable output with package heading and rule separator
- Fallback to npm registry to find GitHub repo when formula URLs don't point there
- Fallback to PyPI registry for Python packages
- Monorepo tag support - handles `pkg@1.2.0` style tags and skips scoped sub-package tags
- `GITHUB_TOKEN` support to raise GitHub API rate limit from 60 to 5000 req/hr
- Graceful fallbacks: shows homepage URL when no GitHub repo or releases can be found

[0.1.0]: https://github.com/iturgeon/brew-changelog/releases/tag/v0.1.0
