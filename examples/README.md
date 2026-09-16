# Examples

## Deploying the Voting contract

[`script/Voting.s.sol`](../script/Voting.s.sol) deploys the contract with no constructor arguments and logs its address.

### Locally (Anvil)

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

### To Sepolia

```shell
cp .env.example .env
# edit .env: set SEPOLIA_RPC_URL, PRIVATE_KEY, ETHERSCAN_API_KEY
set -a && source .env && set +a

forge script script/Voting.s.sol \
  --rpc-url sepolia \
  --private-key $PRIVATE_KEY \
  --broadcast \
  --verify
```

Expected output:

```
##### sepolia
✅  [Success] Hash: 0xabc123...def456
Contract Address: 0x1234567890abcdef1234567890abcdef12345678
Block: 6942069
Paid: 0.00123456 ETH (123456 gas * 10 gwei)

Starting contract verification...
Waiting for verification result...
Contract successfully verified

Transactions saved to: broadcast/Voting.s.sol/11155111/run-latest.json
```

Look the address up at `https://sepolia.etherscan.io/address/<the address above>` — with `--verify`, the source code is already attached — or interact with it directly:

```shell
VOTING=<the deployed address>
cast send $VOTING "addVoter(address)" $(cast wallet address --private-key $PRIVATE_KEY) --rpc-url sepolia --private-key $PRIVATE_KEY
cast call $VOTING "workflowStatus()(uint8)" --rpc-url sepolia
```

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
