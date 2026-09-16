# Changelog

All notable changes to this project are documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/).

## [Unreleased]

### Changed

- CI now only triggers on `master` (dropped the unused `main` branch trigger, kept for parity with the sibling Hardhat template).

### Added

- `examples/` directory with a README of usage walkthroughs (deployment script, `cast` interaction, tests as documentation).

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
