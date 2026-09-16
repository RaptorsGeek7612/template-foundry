# Changelog

All notable changes to this project are documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/).

## [Unreleased]

## [0.1.6] - 2026-09-16

### Added

- A full worked Sepolia deployment example (with expected `forge script` output and `cast` interaction) in `examples/README.md`, linked from the README's Sepolia section.

## [0.1.5] - 2026-09-16

### Added

- Automated tagging and releasing: a `release` job in CI now creates a git tag and GitHub release automatically whenever a push to `master` changes `CHANGELOG.md` and introduces a new version section that isn't tagged yet. It waits for the `test` job to pass first, and pulls the release notes straight from that version's CHANGELOG section. Bumping the version is still a manual, deliberate edit — only the tag/release mechanics are automated.

## [0.1.4] - 2026-09-16

### Added

- GitHub issue templates (bug report, feature request).
- `SECURITY.md`.
- License badge in the README.
- A `Coverage` step in CI (`forge coverage`).
- GitHub repo topics (`foundry`, `solidity`, `ethereum`, `web3`, `voting`, `template`, `smart-contracts`) for discoverability.
- Branch protection on `master`: the CI check must pass before merging; force-pushes and branch deletion are blocked.
- `examples/` directory with a README of usage walkthroughs (deployment script, `cast` interaction, tests as documentation).

### Changed

- CI now only triggers on `master` (dropped the unused `main` branch trigger, kept for parity with the sibling Hardhat template).

## [0.1.3] - 2026-09-16

### Added

- `.gitattributes` (normalize line endings to LF, mark `foundry.lock` as generated).

## [0.1.2] - 2026-09-16

### Added

- Cross-links to the sibling Hardhat template in the README description.

## [0.1.1] - 2026-09-16

### Added

- "Latest release" badge/link in the README.

## [0.1.0] - 2026-09-16

### Added

- Initial pure Foundry template: `src/Voting.sol` (whitelisted on-chain voting workflow, `Ownable`-gated, mirrors the equivalent Hardhat template's contract).
- `test/Voting.t.sol` — 18 Foundry tests (unit, revert, event, and one fuzz test) covering the full workflow and access control.
- `script/Voting.s.sol` — deployment script (local/Anvil or Sepolia).
- `forge-std` and `openzeppelin-contracts` (v5.7.0) as git submodules, pinned via `foundry.lock`.
- GitHub Actions CI (`forge fmt --check`, build, test) with a status badge in the README.
- MIT `LICENSE` file.
- `CONTRIBUTING.md` and a pull request template.
