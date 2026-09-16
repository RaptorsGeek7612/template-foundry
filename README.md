# Voting (Foundry)

[![CI](https://github.com/RaptorsGeek7612/template-foundry/actions/workflows/ci.yml/badge.svg)](https://github.com/RaptorsGeek7612/template-foundry/actions/workflows/ci.yml)
[![Latest release](https://img.shields.io/github/v/release/RaptorsGeek7612/template-foundry)](https://github.com/RaptorsGeek7612/template-foundry/releases/latest)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

A whitelisted on-chain voting system built with Foundry and OpenZeppelin's `Ownable`. This is the Foundry counterpart of a pair of framework-pure starter templates implementing the same `Voting` contract:

- Hardhat — https://github.com/RaptorsGeek7612/template-hardhat
- Foundry (this repo) — https://github.com/RaptorsGeek7612/template-foundry

The `Voting` contract drives voters through a fixed workflow:

1. `RegisteringVoters` — the owner whitelists voter addresses.
2. `ProposalsRegistrationStarted` — whitelisted voters submit proposals.
3. `ProposalsRegistrationEnded`
4. `VotingSessionStarted` — whitelisted voters cast one vote each.
5. `VotingSessionEnded`
6. `VotesTallied` — the owner tallies votes; the most-voted proposal wins.

Only the owner can advance the workflow and register voters; only registered voters can submit proposals, vote, or read voter/proposal data.

## Project layout

```
src/               Voting.sol
test/              Foundry unit + fuzz tests (Voting.t.sol)
script/            Deployment script (Voting.s.sol)
lib/               Dependencies as git submodules (forge-std, openzeppelin-contracts)
examples/          Walkthroughs and usage examples (see examples/README.md)
foundry.toml
```

## Setup

```shell
git clone --recurse-submodules <this-repo>
# or, if already cloned without --recurse-submodules:
git submodule update --init --recursive

forge install   # only needed if lib/ is empty
cp .env.example .env   # fill in values to deploy to Sepolia
```

## Usage

### Build

```shell
forge build
```

### Test

Runs the full Solidity test suite, including the fuzz test:

```shell
forge test
forge test -vvv          # verbose traces on failure
forge test --match-test testFuzz_AddProposalIncrementsProposalCount
```

### Format & static checks

```shell
forge fmt --check
```

### Local deployment (Anvil)

```shell
anvil                                                        # in one terminal
forge script script/Voting.s.sol --rpc-url http://127.0.0.1:8545 \
  --private-key 0xac0974bec39a17e36ba4a6b4d238ff944bacb478cbed5efcae784d7bf4f2ff80 \
  --broadcast
```

(That private key is Anvil's well-known default test account #0 — never reuse it for anything real.)

### Deploying to Sepolia

Foundry does not read `.env` automatically — export it first:

```shell
set -a && source .env && set +a

forge script script/Voting.s.sol \
  --rpc-url sepolia \
  --private-key $PRIVATE_KEY \
  --broadcast \
  --verify
```

Prefer not to keep a raw private key in `.env`? Use Foundry's encrypted keystore instead:

```shell
cast wallet import deployer --interactive
forge script script/Voting.s.sol --rpc-url sepolia --account deployer --broadcast --verify
```

See [examples/README.md](examples/README.md#to-sepolia) for a full worked example, including expected output.

### Interacting with a deployed contract

```shell
cast send <VOTING_ADDRESS> "addVoter(address)" <VOTER_ADDRESS> --rpc-url sepolia --account deployer
cast call <VOTING_ADDRESS> "workflowStatus()(uint8)" --rpc-url sepolia
```

## Docs

- Foundry Book — https://book.getfoundry.sh/
- OpenZeppelin Contracts — https://docs.openzeppelin.com/contracts/5.x/

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md).

## License

MIT — see [LICENSE](LICENSE).
