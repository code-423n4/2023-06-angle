# Angle Protocol - Invitational audit details

- Total Prize Pool: $52,500 USDC
  - HM awards: $27,000 USDC
  - Analysis awards: $1,500 USDC
  - QA awards: $750 USD
  - Gas awards: $750 USDC
  - Judge awards: $8,000 USDC
  - Scout awards: $500 USDC
  - Mitigation Review: $14,000 USDC (_Opportunity goes to top 3 certified wardens based on placement in this audit._)
- Join [C4 Discord](https://discord.gg/code4rena) to register
- Submit findings [using the C4 form](https://code4rena.com/contests/2023-06-angle-protocol/submit)
- [Read our guidelines for more details](https://docs.code4rena.com/roles/wardens)
- Starts June 28, 2023 20:00 UTC
- Ends July 07, 2023 20:00 UTC

## Documentation

- [Overview of the Transmuter system](https://github.com/AngleProtocol/angle-transmuter/tree/9707ee4ed3d221e02dcfcd2ebaa4b4d38d280936/README.md)
- [Transmuter Whitepaper](https://docs.angle.money/overview/whitepapers)
- [Angle Documentation](https://docs.angle.money)
- [Angle Developers Documentation](https://developers.angle.money)
- [Merkl documentation](https://docs.angle.money/side-products/merkl)
- [Merkl overview](https://github.com/AngleProtocol/merkl-contracts/blob/1825925daef8b22d9d6c0a2bc7aab3309342e786/README.md)

## Automated Findings / Publicly Known Issues

- Lack of support for ERC165
- At initialization, fees need to be < 100% for 100% exposure because the first exposures will be ~100%
- If at some point there are 0 funds in the system it’ll break as `amountToNextBreakPoint` will be 0
- In the burn, if there is one asset which is making 99% of the basket, and another one 1%: if the one making 1% depegs, it still impacts the burn for the asset that makes the majority of the funds
- The whitelist function for burns and redemptions are somehow breaking the fairness of the system as whitelisted actors will redeem more value
- Requirements on negative fees and on setters can be bypassed by taking multiple actions (set negative fees and then decrease fees) but this is acceptable as remains within governance powers.
- When negative fees are set the guardian could create arbitrage loops than could potentially enable funds stealing. This is a known issue and negative fees have to be set carefully and for reduced period of time.

Trust assumptions of the system can also be checked [here](https://github.com/AngleProtocol/angle-transmuter/tree/9707ee4ed3d221e02dcfcd2ebaa4b4d38d280936/README.md).

## Scope

| Contracts (24)                                                                                                                                                                                                              | SLOC (2276) | Purpose                                                         | Libraries used |
| --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------- | --------------------------------------------------------------- | -------------- |
| [transmuter/contracts/savings/BaseSavings.sol](https://github.com/AngleProtocol/angle-transmuter/tree/9707ee4ed3d221e02dcfcd2ebaa4b4d38d280936/contracts/savings/BaseSavings.sol)                                           | 10          |                                                                 | openzeppelin   |
| [transmuter/contracts/savings/Savings.sol](https://github.com/AngleProtocol/angle-transmuter/tree/9707ee4ed3d221e02dcfcd2ebaa4b4d38d280936/contracts/savings/Savings.sol)                                                   | 95          |                                                                 |                |
| [transmuter/contracts/savings/SavingsVest.sol](https://github.com/AngleProtocol/angle-transmuter/tree/9707ee4ed3d221e02dcfcd2ebaa4b4d38d280936/contracts/savings/SavingsVest.sol)                                           | 105         | ERC4626 to distribute yield to agEUR holders                    |                |
| [transmuter/contracts/transmuter/facets/AccessControlModifiers.sol](https://github.com/AngleProtocol/angle-transmuter/tree/9707ee4ed3d221e02dcfcd2ebaa4b4d38d280936/contracts/transmuter/facets/AccessControlModifiers.sol) | 13          |                                                                 |                |
| [transmuter/contracts/transmuter/facets/DiamondCut.sol](https://github.com/AngleProtocol/angle-transmuter/tree/9707ee4ed3d221e02dcfcd2ebaa4b4d38d280936/contracts/transmuter/facets/DiamondCut.sol)-                        | 10          | See ERC-2535.                                                   |                |
| [transmuter/contracts/transmuter/facets/DiamondLoupe.sol](https://github.com/AngleProtocol/angle-transmuter/tree/9707ee4ed3d221e02dcfcd2ebaa4b4d38d280936/contracts/transmuter/facets/DiamondLoupe.sol)                     | 92          | See ERC-2535.                                                   |                |
| [transmuter/contracts/transmuter/facets/Getters.sol](https://github.com/AngleProtocol/angle-transmuter/tree/9707ee4ed3d221e02dcfcd2ebaa4b4d38d280936/contracts/transmuter/facets/Getters.sol)                               | 105         | View functions ot fetch the storage of the Transmuter           |                |
| [transmuter/contracts/transmuter/facets/Redeemer.sol](https://github.com/AngleProtocol/angle-transmuter/tree/9707ee4ed3d221e02dcfcd2ebaa4b4d38d280936/contracts/transmuter/facets/Redeemer.sol)                             | 113         | Redeeming functionalities                                       |                |
| [transmuter/contracts/transmuter/facets/RewardHandler.sol](https://github.com/AngleProtocol/angle-transmuter/tree/9707ee4ed3d221e02dcfcd2ebaa4b4d38d280936/contracts/transmuter/facets/RewardHandler.sol)                   | 45          |                                                                 | openzeppelin   |
| [transmuter/contracts/transmuter/facets/SettersGovernor.sol](https://github.com/AngleProtocol/angle-transmuter/tree/9707ee4ed3d221e02dcfcd2ebaa4b4d38d280936/contracts/transmuter/facets/SettersGovernor.sol)               | 120         | Admin functions of the Transmuter - Governor Role               | openzeppelin   |
| [transmuter/contracts/transmuter/facets/SettersGuardian.sol](https://github.com/AngleProtocol/angle-transmuter/tree/9707ee4ed3d221e02dcfcd2ebaa4b4d38d280936/contracts/transmuter/facets/SettersGuardian.sol)               | 19          | Admin functions of the Transmuter - Guardian Role               | openzeppelin   |
| [transmuter/contracts/transmuter/facets/Swapper.sol](https://github.com/AngleProtocol/angle-transmuter/tree/9707ee4ed3d221e02dcfcd2ebaa4b4d38d280936/contracts/transmuter/facets/Swapper.sol)                               | 345         | User facing swap functions                                      | openzeppelin   |
| [transmuter/contracts/transmuter/libraries/LibDiamond.sol](https://github.com/AngleProtocol/angle-transmuter/tree/9707ee4ed3d221e02dcfcd2ebaa4b4d38d280936/contracts/transmuter/libraries/LibDiamond.sol)                   | 122         | See ERC-2535.                                                   |                |
| [transmuter/contracts/transmuter/libraries/LibHelpers.sol](https://github.com/AngleProtocol/angle-transmuter/tree/9707ee4ed3d221e02dcfcd2ebaa4b4d38d280936/contracts/transmuter/libraries/LibHelpers.sol)                   | 45          |                                                                 |                |
| [transmuter/contracts/transmuter/libraries/LibManager.sol](https://github.com/AngleProtocol/angle-transmuter/tree/9707ee4ed3d221e02dcfcd2ebaa4b4d38d280936/contracts/transmuter/libraries/LibManager.sol)                   | 29          |                                                                 |                |
| [transmuter/contracts/transmuter/libraries/LibOracle.sol](https://github.com/AngleProtocol/angle-transmuter/tree/9707ee4ed3d221e02dcfcd2ebaa4b4d38d280936/contracts/transmuter/libraries/LibOracle.sol)                     | 98          |                                                                 |                |
| [transmuter/contracts/transmuter/libraries/LibSetters.sol](https://github.com/AngleProtocol/angle-transmuter/tree/9707ee4ed3d221e02dcfcd2ebaa4b4d38d280936/contracts/transmuter/libraries/LibSetters.sol)                   | 201         |                                                                 |                |
| [transmuter/contracts/transmuter/libraries/LibStorage.sol](https://github.com/AngleProtocol/angle-transmuter/tree/9707ee4ed3d221e02dcfcd2ebaa4b4d38d280936/contracts/transmuter/libraries/LibStorage.sol)                   | 17          |                                                                 |                |
| [transmuter/contracts/transmuter/libraries/LibWhitelist.sol](https://github.com/AngleProtocol/angle-transmuter/tree/9707ee4ed3d221e02dcfcd2ebaa4b4d38d280936/contracts/transmuter/libraries/LibWhitelist.sol)               | 19          |                                                                 |                |
| [transmuter/contracts/transmuter/libraries/LibGetters.sol](https://github.com/AngleProtocol/angle-transmuter/tree/9707ee4ed3d221e02dcfcd2ebaa4b4d38d280936/contracts/transmuter/libraries/LibGetters.sol)                   | 56          |                                                                 |                |
| [transmuter/contracts/transmuter/DiamondProxy.sol](https://github.com/AngleProtocol/angle-transmuter/tree/9707ee4ed3d221e02dcfcd2ebaa4b4d38d280936/contracts/transmuter/DiamondProxy.sol)                                   | 31          | See ERC-2535. Base Transmuter contract                          |                |
| [transmuter/contracts/transmuter/Storage.sol](https://github.com/AngleProtocol/angle-transmuter/tree/9707ee4ed3d221e02dcfcd2ebaa4b4d38d280936/contracts/transmuter/Storage.sol)                                             | 101         | Structs of the Transmuter storage                               |                |
| [merkl/contracts/DistributionCreator.sol](https://github.com/AngleProtocol/merkl-contracts/blob/1825925daef8b22d9d6c0a2bc7aab3309342e786/contracts/DistributionCreator.sol)                                                 | 301         | Contract to initiate a distribution of rewards to UniswapV3 LPs | openzeppelin   |
| [merkl/contracts/Distributor.sol](https://github.com/AngleProtocol/merkl-contracts/blob/1825925daef8b22d9d6c0a2bc7aab3309342e786/contracts/Distributor.sol)                                                                 | 184         | Contract to distribute incentives via Merkl tree airdrops       | openzeppelin   |

## Out of scope

All files not listed above are out of scope for this audit. It includes:

| Contracts                                                                                                                                                                 | Purpose                                                                |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------- |
| [transmuter/transmuter/configs/\*\*.sol](https://github.com/AngleProtocol/angle-transmuter/tree/9707ee4ed3d221e02dcfcd2ebaa4b4d38d280936/contracts/transmuter/configs)    | Configuration file to create mock and prod deployments (not finalized) |
| [transmuter/transmuter/Layout.sol](https://github.com/AngleProtocol/angle-transmuter/tree/9707ee4ed3d221e02dcfcd2ebaa4b4d38d280936/contracts/transmuter/Layout.sol)       | Contract to check the storage layout is well understood                |
| [transmuter/interfaces/\*\*.sol](https://github.com/AngleProtocol/angle-transmuter/tree/9707ee4ed3d221e02dcfcd2ebaa4b4d38d280936/contracts/interfaces)                    |                                                                        |
| [transmuter/utils/\*\*.sol](https://github.com/AngleProtocol/angle-transmuter/tree/9707ee4ed3d221e02dcfcd2ebaa4b4d38d280936/contracts/utils)                              |                                                                        |
| [merkl/contracts/](https://github.com/AngleProtocol/merkl-contracts/blob/1825925daef8b22d9d6c0a2bc7aab3309342e786/contracts/): all files aside from the 2 listed in scope |                                                                        |

## Scoping Details

```
- If you have a public code repo, please share it here:
- How many contracts are in scope?:   24
- Total SLoC for these contracts?:  2276
- How many external imports are there?: 2
- How many separate interfaces and struct definitions are there for the contracts within scope?:  15
- Does most of your code generally use composition or inheritance?:   Composition
- How many external calls?:   3
- What is the overall line coverage percentage provided by your tests?:  100
- Is there a need to understand a separate part of the codebase / get context in order to audit this part of the protocol?:   False
- Please describe required context:
- Does it use an oracle?:  Chainlink
- Does the token conform to the ERC20 standard?:  True
- Are there any novel or unique curve logic or mathematical models?: https://github.com/AngleProtocol/angle-docs/blob/main/whitepapers/Transmuter.pdf
- Does it use a timelock function?:
- Is it an NFT?:
- Does it have an AMM?:   True
- Is it a fork of a popular project?:   False
- Does it use rollups?:
- Is it multi-chain?:
- Does it use a side-chain?: False
```

## Tests

First, clone the repo recursively:

```bash
# Clone using SSH
git clone git@github.com:code-423n4/2023-06-angle.git --recursive
# Or clone using HTTPS
git clone https://github.com/code-423n4/2023-06-angle --recursive
# Or update submodules if the cloning was done without recursive
git submodule update --init --recursive
```

Then, execute the following (eventually replacing with your custom Arbitrum endpoint):

```
cd 2023-06-angle/transmuter
yarn
forge i
yarn test
cd ../merkl
echo ETH_NODE_URI_ARBITRUM=https://1rpc.io/arb > .env
yarn
forge i
yarn hardhat:test
```

## Slither

Slither can be run using `yarn slither` in the transmuter repository. We've already gone through the slither report.
