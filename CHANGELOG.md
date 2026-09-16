# Changelog

All notable changes to this project are documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/).

## [Unreleased]

## [0.1.0] - 2026-09-16

### Added

- Initial pure Foundry template: `src/Voting.sol` (whitelisted on-chain voting workflow, `Ownable`-gated, mirrors the equivalent Hardhat template's contract).
- `test/Voting.t.sol` — 18 Foundry tests (unit, revert, event, and one fuzz test) covering the full workflow and access control.
- `script/Voting.s.sol` — deployment script (local/Anvil or Sepolia).
- `forge-std` and `openzeppelin-contracts` (v5.7.0) as git submodules, pinned via `foundry.lock`.
- GitHub Actions CI (`forge fmt --check`, build, test) with a status badge in the README.
- MIT `LICENSE` file.
- `CONTRIBUTING.md` and a pull request template.
