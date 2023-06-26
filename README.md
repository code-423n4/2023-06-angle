# Angle Protocol - Invitational audit details

- Total Prize Pool: $52,500 USDC (Notion: Total award pool)
  - HM awards: $26,000 USDC (Notion: HM (main) pool)
  - QA awards: $3,000 USDC (Notion: QA pool)
  - Gas awards: $1,000 USDC (Notion: Gas pool)
  - Judge awards: $8,000 USDC (Notion: Judge Fee)
  - Scout awards: $500 USDC (Notion: Scout fee - but usually $500 USDC)
  - Mitigation Review: $14,000 USDC (_Opportunity goes to top 3 certified wardens based on placement in this audit._)
- Join [C4 Discord](https://discord.gg/code4rena) to register
- Submit findings [using the C4 form](https://code4rena.com/contests/2023-06-angle-protocol/submit)
- [Read our guidelines for more details](https://docs.code4rena.com/roles/wardens)
- Starts June 26, 2023 20:00 UTC
- Ends July 06, 2023 20:00 UTC

## Documentation

- [Overview of the Transmuter system](transmuter/README.md)
- [Transmuter Whitepaper](https://docs.angle.money/overview/whitepapers)
- [Angle Documentation](https://docs.angle.money)
- [Angle Developers Documentation](https://developers.angle.money)
- [Merkl documentation](https://docs.angle.money/side-products/merkl)
- [Merkl overview](merkl/README.md)
-

## Automated Findings / Publicly Known Issues

Automated findings output for the audit can be found [here](add link to report) within 24 hours of audit opening.

_Note for C4 wardens: Anything included in the automated findings output is considered a publicly known issue and is ineligible for awards._

- Lack of support for ERC165
- At initialization, fees need to be < 100% for 100% exposure because the first exposures will be ~100%
- If at some point there are 0 funds in the system it’ll break as `amountToNextBreakPoint` will be 0
- In the burn, if there is one asset which is making 99% of the basket, and another one 1%: if the one making 1% depegs, it still impacts the burn for the asset that makes the majority of the funds
- The whitelist function for burns and redemptions are somehow breaking the fairness of the system as whitelisted actors will redeem more value

Trust assumptions of the system can also be checked [here](transmuter/README.md).

## Scope

| Contracts (24)                                                                                                                                                                                                              | SLOC (2276) | Purpose                                                         | Libraries used |
| --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------- | --------------------------------------------------------------- | -------------- |
| [transmuter/contracts/savings/BaseSavings.sol](https://github.com/AngleProtocol/angle-transmuter/tree/040f9beeb394fe85f3e647bfcccd58acea575b0e/contracts/savings/BaseSavings.sol)                                           | 10          |                                                                 |                |
| [transmuter/contracts/savings/Savings.sol](https://github.com/AngleProtocol/angle-transmuter/tree/040f9beeb394fe85f3e647bfcccd58acea575b0e/contracts/savings/Savings.sol)                                                   | 95          |                                                                 |                |
| [transmuter/contracts/savings/SavingsVest.sol](https://github.com/AngleProtocol/angle-transmuter/tree/040f9beeb394fe85f3e647bfcccd58acea575b0e/contracts/savings/SavingsVest.sol)                                           | 105         | ERC4626 to distribute yield to agEUR holders                    |                |
| [transmuter/contracts/transmuter/facets/AccessControlModifiers.sol](https://github.com/AngleProtocol/angle-transmuter/tree/040f9beeb394fe85f3e647bfcccd58acea575b0e/contracts/transmuter/facets/AccessControlModifiers.sol) | 13          |                                                                 |                |
| [transmuter/contracts/transmuter/facets/DiamondCut.sol](https://github.com/AngleProtocol/angle-transmuter/tree/040f9beeb394fe85f3e647bfcccd58acea575b0e/contracts/transmuter/facets/DiamondCut.sol)-                        | 10          | See ERC-2535.                                                   |                |
| [transmuter/contracts/transmuter/facets/DiamondLoupe.sol](https://github.com/AngleProtocol/angle-transmuter/tree/040f9beeb394fe85f3e647bfcccd58acea575b0e/contracts/transmuter/facets/DiamondLoupe.sol)                     | 92          | See ERC-2535.                                                   |                |
| [transmuter/contracts/transmuter/facets/Getters.sol](https://github.com/AngleProtocol/angle-transmuter/tree/040f9beeb394fe85f3e647bfcccd58acea575b0e/contracts/transmuter/facets/Getters.sol)                               | 105         | View functions ot fetch the storage of the Transmuter           |                |
| [transmuter/contracts/transmuter/facets/Redeemer.sol](https://github.com/AngleProtocol/angle-transmuter/tree/040f9beeb394fe85f3e647bfcccd58acea575b0e/contracts/transmuter/facets/Redeemer.sol)                             | 113         | Redeeming functionalities                                       |                |
| [transmuter/contracts/transmuter/facets/RewardHandler.sol](https://github.com/AngleProtocol/angle-transmuter/tree/040f9beeb394fe85f3e647bfcccd58acea575b0e/contracts/transmuter/facets/RewardHandler.sol)                   | 45          |                                                                 |                |
| [transmuter/contracts/transmuter/facets/SettersGovernor.sol](https://github.com/AngleProtocol/angle-transmuter/tree/040f9beeb394fe85f3e647bfcccd58acea575b0e/contracts/transmuter/facets/SettersGovernor.sol)               | 120         | Admin functions of the Transmuter - Governor Role               |                |
| [transmuter/contracts/transmuter/facets/SettersGuardian.sol](https://github.com/AngleProtocol/angle-transmuter/tree/040f9beeb394fe85f3e647bfcccd58acea575b0e/contracts/transmuter/facets/SettersGuardian.sol)               | 19          | Admin functions of the Transmuter - Guardian Role               |                |
| [transmuter/contracts/transmuter/facets/Swapper.sol](https://github.com/AngleProtocol/angle-transmuter/tree/040f9beeb394fe85f3e647bfcccd58acea575b0e/contracts/transmuter/facets/Swapper.sol)                               | 345         | User facing swap functions                                      |                |
| [transmuter/contracts/transmuter/libraries/LibDiamond.sol](https://github.com/AngleProtocol/angle-transmuter/tree/040f9beeb394fe85f3e647bfcccd58acea575b0e/contracts/transmuter/libraries/LibDiamond.sol)                   | 122         | See ERC-2535.                                                   |                |
| [transmuter/contracts/transmuter/libraries/LibHelpers.sol](https://github.com/AngleProtocol/angle-transmuter/tree/040f9beeb394fe85f3e647bfcccd58acea575b0e/contracts/transmuter/libraries/LibHelpers.sol)                   | 45          |                                                                 |                |
| [transmuter/contracts/transmuter/libraries/LibManager.sol](https://github.com/AngleProtocol/angle-transmuter/tree/040f9beeb394fe85f3e647bfcccd58acea575b0e/contracts/transmuter/libraries/LibManager.sol)                   | 29          |                                                                 |                |
| [transmuter/contracts/transmuter/libraries/LibOracle.sol](https://github.com/AngleProtocol/angle-transmuter/tree/040f9beeb394fe85f3e647bfcccd58acea575b0e/contracts/transmuter/libraries/LibOracle.sol)                     | 98          |                                                                 |                |
| [transmuter/contracts/transmuter/libraries/LibSetters.sol](https://github.com/AngleProtocol/angle-transmuter/tree/040f9beeb394fe85f3e647bfcccd58acea575b0e/contracts/transmuter/libraries/LibSetters.sol)                   | 201         |                                                                 |                |
| [transmuter/contracts/transmuter/libraries/LibStorage.sol](https://github.com/AngleProtocol/angle-transmuter/tree/040f9beeb394fe85f3e647bfcccd58acea575b0e/contracts/transmuter/libraries/LibStorage.sol)                   | 17          |                                                                 |                |
| [transmuter/contracts/transmuter/libraries/LibWhitelist.sol](https://github.com/AngleProtocol/angle-transmuter/tree/040f9beeb394fe85f3e647bfcccd58acea575b0e/ontracts/transmuter/libraries/LibWhitelist.sol)                | 19          |                                                                 |                |
| [transmuter/contracts/transmuter/libraries/LibGetters.sol](https://github.com/AngleProtocol/angle-transmuter/tree/040f9beeb394fe85f3e647bfcccd58acea575b0e/contracts/transmuter/libraries/LibGetters.sol)                   | 56          |                                                                 |                |
| [transmuter/contracts/transmuter/DiamondProxy.sol](https://github.com/AngleProtocol/angle-transmuter/tree/040f9beeb394fe85f3e647bfcccd58acea575b0e/contracts/transmuter/DiamondProxy.sol)                                   | 31          | See ERC-2535. Base Transmuter contract                          |                |
| [transmuter/contracts/transmuter/Storage.sol](https://github.com/AngleProtocol/angle-transmuter/tree/040f9beeb394fe85f3e647bfcccd58acea575b0e/contracts/transmuter/Storage.sol)                                             | 101         | Structs of the Transmuter storage                               |                |
| [merkl/contracts/DistributionCreator.sol](https://github.com/AngleProtocol/merkl-contracts/blob/febb61a09c8e81877159c6d89c12bd308b74d6ee/contracts/DistributionCreator.sol)                                                 | 301         | Contract to initiate a distribution of rewards to UniswapV3 LPs |                |
| [merkl/contracts/Distributor.sol](https://github.com/AngleProtocol/merkl-contracts/blob/febb61a09c8e81877159c6d89c12bd308b74d6ee/contracts/Distributor.sol)                                                                 | 184         | Contract to distribute incentives via Merkl tree airdrops       |                |

## Out of scope

| Contracts | SLOC | Purpose | Libraries used |
| --------- | ---- | ------- | -------------- |
|           |      |         |                |

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
git clone https://github.com/code-423n4/2023-06-angle --recursive
cd 2023-06-angle/transmuter
forge i
yarn test
cd ../merkl
yarn
forge i
yarn hardhat:test
```

## Slither

Slither can be run using `yarn slither` in the transmuter repository. We've already gone through the slither report.
