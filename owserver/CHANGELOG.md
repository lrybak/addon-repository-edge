# Changelog since v0.9.2
- Changelog 0.9.3: add owserver error log fix 
- Merge pull request #98 from lrybak/chore/tempio-macos

Use the tempio binary for macOS in template tests 
- Merge pull request #97 from lrybak/fix/owserver-foreground-logs

Show owserver and owhttpd errors in the app log 
- Start owhttpd only when owserver is up

bashio::net.wait_for waits at most 60 seconds. After that owhttpd
started anyway, stopped with exit code 1 after 5 seconds when owserver
was not running, and the loop added lines to the log every 75 seconds.

Wait for port 4304 with no time limit. BusyBox "timeout 0" stops at
once, so use a simple loop instead of bashio::net.wait_for. 
- Use the tempio binary for macOS in template tests

tempio 2026.07.0 has release binaries for macOS (darwin_arm64 and
darwin_amd64), so template tests can use a local binary on macOS too,
not only on Linux.

- Download the tempio binary for Linux and macOS.
- Bump TEMPIO_VERSION from 2024.11.2 to 2026.07.0, the version in the
  base image.
- Start the container only when there is no local binary, so
  `pytest tests/ -m template` does not need Docker on Linux and macOS. 
- Show owserver and owhttpd errors in the app log

owserver and owhttpd ran as daemons. Their errors went to syslog,
which the container does not have, so the app log showed only
"Starting owserver...". s6 also did not supervise the daemons.

- Start both with --foreground --error_print=2 and remove the pgrep check.
- Add finish scripts: if a service stops by itself, wait 10 seconds
  before s6 starts it again, so the same error does not fill the log.
  Stop waiting when the app is stopping.
- Add tests for the error message and for s6 supervision.

Fixes #96 
- Merge pull request #94 from lrybak/fix/release-drafter-autolabeler

Fix release-drafter autolabeler and migrate config to v7 
- Make release-drafter categories exclusive 
- Fix release-drafter autolabeler and migrate config to v7 
- Changelog 0.9.3 
- Merge pull request #92 from lrybak/chore/bump-base-21.0.8

Bump addon base image to 21.0.8 
- Bump addon base image to 21.0.8 
- Merge pull request #91 from lrybak/docs/add-claude-md

Add CLAUDE.md, bump-base-image skill and chore/ branch support 
- Never merge PRs, the maintainer does the final merge 
- Add Unreleased section and missing 0.9.2 changelog entry 
- Add chore/ branch prefix to CI, lint and release-drafter 
- Add CLAUDE.md and bump-base-image skill 
- Merge pull request #90 from lrybak/dependabot/github_actions/hadolint/hadolint-action-3.5.0

ci: bump hadolint/hadolint-action from 3.4.0 to 3.5.0 
- ci: bump hadolint/hadolint-action from 3.4.0 to 3.5.0

Bumps [hadolint/hadolint-action](https://github.com/hadolint/hadolint-action) from 3.4.0 to 3.5.0.
- [Release notes](https://github.com/hadolint/hadolint-action/releases)
- [Commits](https://github.com/hadolint/hadolint-action/compare/v3.4.0...v3.5.0)

---
updated-dependencies:
- dependency-name: hadolint/hadolint-action
  dependency-version: 3.5.0
  dependency-type: direct:production
  update-type: version-update:semver-minor
...

Signed-off-by: dependabot[bot] <support@github.com> 
