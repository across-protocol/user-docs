---
description: >-
  Across Reward Locking Program is a novel DeFi mechanism to further incentivize
  bridge LPs. Scroll down to the bottom for instructions on how to get started.
---

# Reward Locking

## **Program Details**

### Overview

Across is the first protocol to implement reward locking. It is used to further incentivize bridge liquidity positions by incrementally increasing reward APY over time for users who stake capital. For Across’ reward locking programming, an LP’s multiplier starts at 1x on day zero and can grow linearly to a maximum of 2x after capital has been staked for 100+ days.

Reward multipliers reset to 1x once rewards have been claimed or liquidity is unstaked.

<figure><img src="../../.gitbook/assets/image (4).png" alt=""><figcaption></figcaption></figure>

In September 2023, [a Snapshot proposal](https://snapshot.org/#/acrossprotocol.eth/proposal/0xb2bd26a68cceba984275a10c67efe3b06f24fc2a48907197614b62dc48d1dfc7) was passed to increase liquidity pool APY % by 50% and reduce the original multipler number of 3x to 2x. The following emissions changes were implemented:

* ~~50,000~~ → \~75,000 ACX per day for Across ETH LP tokens
* ~~50,000~~ → \~75,000 ACX per day for Across USDC LP tokens
* ~~5,000~~ → \~7,500 ACX per day for Across USDT LP tokens
* ~~5,000~~ → \~7,500 ACX per day for Across DAI LP tokens
* ~~5,000~~ → \~7,500 ACX per day for Across WBTC LP tokens
* ~~20,000~~ → \~30,000 ACX per day for Across ACX LP tokens

#### Information for Other Projects Looking To Implement Reward Locking

Risk Labs (the foundation that supports UMA and Across Protocol) has  deployed a contract called the[ Accelerating Distributor](https://github.com/across-protocol/across-token/blob/master/contracts/AcceleratingDistributor.sol) ([audit](https://blog.openzeppelin.com/across-token-and-token-distributor-audit/)) to allow any project to implement the concept of reward locking. You can read the full details in our[ Reward Locking article](https://medium.com/across-protocol/introducing-reward-locking-78b26c792b11).

### How to Start Earning a Reward Multiplier &#x20;

When you stake LP tokens on Across, you are automatically entered into the reward locking program and will immediately begin earning a higher APY incrementally each day. Please note that your APY multiplier will reset to 1x once capital is unstaked or rewards are claimed.

### Adding Additional Liquidity to Stake in Reward Locking.&#x20;

When you add additional tokens to your already existing staked assets your reward multiplier will change based on the average age of capital. Our formula uses the time-weighted sum of deposits.&#x20;

For example, if you deposit 10 tokens at time 1, the average age of capital is 1. If you deposit the next 5 tokens at time 5, the average age of capital = (1 \* (10/15) + 5 \* (5/15)) = 2.3333



## How to Stake, Unstake and Claim Staking Rewards

### How to Stake Your Liquidity on Across

**Step 1:** Go to [across.to/pool](https://across.to/pool)

**Step 2:** Connect your wallet&#x20;

**Step 3:** Select the pool you would like to add to

**Step 4:** Enter the amount of tokens you would like to add to the pool or click "MAX"

**Step 5:** Confirm details and click "Add liquidity"

<figure><img src="../../.gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>

**Step 6:** After you've added liquidity, click the arrow in the box (see above image) to stake your tokens&#x20;

**Step 7:** Enter the amount of LP tokens that you would like to stake or click "MAX"

**Step 8:** Confirm details and click "Stake"

**Step 9:** Approve the transaction in your wallet

**Step 10:** Congratulations, you are now enrolled in the Reward Locking Program at Across! You can review your multiplier level and total accrued rewards at [across.to/rewards](https://across.to/rewards)



### How to Unstake Liquidity from Across

_\*Please note that unstaking will reset your reward multiplier to 1x, which will reduce your APY %_

**Step 1:** Go to [across.to/pool](https://across.to/pool)

**Step 2:** Connect your wallet&#x20;

**Step 3:** Select the pool you would like to unstake liquidity from

<figure><img src="../../.gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>

**Step 4:** Click the arrow in the box (see above image) to access your staked position

**Step 5:** Click the "Unstake" tab

**Step 6:** Enter the amount of LP tokens you would like to unstake or click "MAX"

**Step 7:** Confirm details and click "Unstake"

**Step 8:** Approve the transaction in your wallet

**Step 9:** To review your liquidity positions go to [across.to/rewards](https://across.to/rewards)



### Claim Staking Rewards

_\*Please note that claiming rewards will reset your reward multiplier to 1x, which will reduce your APY %_

**Step 1:** Go to [across.to/rewards](https://across.to/rewards)

**Step 2:** Connect your wallet&#x20;

**Step 3:** Select the pool you would like to claim rewards from by clicking the arrow button to the right of the pool's "Rewards" tab

**Step 4:** At the bottom of the screen, click the "Caim Rewards" button

**Step 5:** Approve the transaction in your wallet

**Step 6:** To review your liquidity positions go to [across.to/rewards](https://across.to/rewards)

