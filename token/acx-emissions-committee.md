---
description: The AEC determines emissions of bridge liquidity incentives
---

# ACX Emissions Committee

The AEC gives the Across DAO an efficient and transparent way to manage ACX emissions so that ACX is optimally used for incentives for bridge liquidity. It was implemented in January 2024 after passing a [governance vote](https://snapshot.org/#/acrossprotocol.eth/proposal/0xe95b8fd6890d01f6a8d0cd536b804db8f44f0d98267ffa9c16a40620e6dbbdbf).

### Committee Design

The AEC owns the [Accelerating Distributor](https://github.com/across-protocol/across-token/blob/master/contracts/AcceleratingDistributor.sol) contract, which controls the parameters of the Across [Reward Locking](https://medium.com/across-protocol/introducing-reward-locking-78b26c792b11) program, through a 3 of 5 multisig.&#x20;

### Adjustment Framework

The AEC uses a clear and transparent framework to adjust ACX emissions. The framework is restrictive so that only predictable and measured actions are taken to modify ACX emissions. Decisions are driven by two observable factors:

* Across pool utilization - LPs should be rewarded for how much demand there is for an asset for transfers. The AEC will track the 7-day average pool utilization of each asset.&#x20;
* Competing yield - LPs should be rewarded a fair yield in comparison to yields paid by competing protocols. The AEC can track a Yield Index for each asset that is computed as a 7-day average of the TVL weighted yield of pools on Stargate, Hop, and Synapse.

The AEC uses this framework to determine whether action needs to be taken on ETH, USDC, USDT, and DAI. If an action is required, the AEC can only increase or decrease emissions of an asset by 25% and then wait 14 days to re-evaluate and take further action if needed.&#x20;

| Across Pool Utilization | Decrease emissions by 25% if total Base LP APY vs Yield Index is | Increase emissions by 25% if total Base LP APY vs Yield Index is |
| ----------------------- | ---------------------------------------------------------------- | ---------------------------------------------------------------- |
| 0 - 40%                 | +25%                                                             | -75%                                                             |
| 40 - 70%                | +50%                                                             | -50%                                                             |
| 70 - 100%               | +100%                                                            | -25%                                                             |

### Resources

* [Change log](https://docs.google.com/spreadsheets/d/1T3HkqynpXS5vFBehgUYybrusNELeUk9GWK4D2aE9djQ/edit#gid=0) - History of AEC emissions adjustments
* [Monitoring Dashboard](https://dune.com/risk\_labs/across-emissions-committee/290672f1-6676-4476-9471-19be6f6637e3) - Every necessary metric the AEC uses to make adjustments

### Long-term Objective

The AEC will set and manage a long term plan for ACX emissions to ensure the Across DAO does not deplete its treasury too quickly and has assets for future growth and other initiatives.

