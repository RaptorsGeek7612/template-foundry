# Examples

## Deploying the Voting contract

[`script/Voting.s.sol`](../script/Voting.s.sol) deploys the contract with no constructor arguments and logs its address.

Against a local Anvil node:

```shell
anvil                                                        # in one terminal
forge script script/Voting.s.sol --rpc-url http://127.0.0.1:8545 \
  --private-key 0xac0974bec39a17e36ba4a6b4d238ff944bacb478cbed5efcae784d7bf4f2ff80 \
  --broadcast
```

Expected output:

```
== Return ==
voting: contract Voting 0x5FbDB2315678afecb367f032d93F642f64180aa3

== Logs ==
  Voting deployed at: 0x5FbDB2315678afecb367f032d93F642f64180aa3
```

See the [Deploying to Sepolia](../README.md#deploying-to-sepolia) section of the main README for testnet usage.

## Driving the full workflow with cast

Once deployed, register voters, run proposals/voting, and read state with `cast`:

```shell
RPC=http://127.0.0.1:8545
KEY=0xac0974bec39a17e36ba4a6b4d238ff944bacb478cbed5efcae784d7bf4f2ff80
VOTING=<deployed address>

cast send $VOTING "addVoter(address)" $(cast wallet address --private-key $KEY) --rpc-url $RPC --private-key $KEY
cast send $VOTING "startProposalsRegistering()" --rpc-url $RPC --private-key $KEY
cast send $VOTING "addProposal(string)" "Plant more trees" --rpc-url $RPC --private-key $KEY
cast call $VOTING "workflowStatus()(uint8)" --rpc-url $RPC
```

## Reading the test suite as usage examples

[`test/Voting.t.sol`](../test/Voting.t.sol) doubles as executable documentation for every function's expected behavior (who can call it, in which workflow phase, and what it reverts on) — including a fuzz test for proposal registration.
