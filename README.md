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

## Automated Findings / Publicly Known Issues

Automated findings output for the audit can be found [here](add link to report) within 24 hours of audit opening.

_Note for C4 wardens: Anything included in the automated findings output is considered a publicly known issue and is ineligible for awards._

[ ⭐️ SPONSORS ADD INFO HERE ]

# Overview

_Please provide some context about the code being audited, and identify any areas of specific concern in reviewing the code. (This is a good place to link to your docs, if you have them.)_

# Scope

_List all files in scope in the table below (along with hyperlinks) -- and feel free to add notes here to emphasize areas of focus._

_For line of code counts, we recommend using [cloc](https://github.com/AlDanial/cloc)._

| Contract                                                   | SLOC | Purpose                | Libraries used                                           |
| ---------------------------------------------------------- | ---- | ---------------------- | -------------------------------------------------------- |
| [contracts/folder/sample.sol](contracts/folder/sample.sol) | 123  | This contract does XYZ | [`@openzeppelin/*`](https://openzeppelin.com/contracts/) |

## Out of scope

_List any files/contracts that are out of scope for this audit._

# Additional Context

_Describe any novel or unique curve logic or mathematical models implemented in the contracts_

_Sponsor, please confirm/edit the information below._

## Scoping Details

```
- If you have a public code repo, please share it here:
- How many contracts are in scope?:   24
- Total SLoC for these contracts?:  2002
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

# Tests

_Provide every step required to build the project from a fresh git clone, as well as steps to run the tests with a gas report._

_Note: Many wardens run Slither as a first pass for testing. Please document any known errors with no workaround._
