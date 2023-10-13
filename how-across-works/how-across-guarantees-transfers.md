---
description: >-
  How a user's bridge request gets fulfilled and how quickly users can expect to
  receive funds
---

# How Across Guarantees Transfers

The Across protocol essentially provides an open market for profit-maximizing relayers to compete to fulfill bridge requests using their proprietary capital. Any bridge requests or "deposits" that are not fulfilled in a timely manner by relayers will eventually be fulfilled using the Across "system capital" supplied by liquidity providers ("LP's").

## Fast Fills

A bridge request contains a "relayer fee" percentage that can be used to incentivize relayers to fill their request on the destination chain quickly. Naturally, the higher the fee percentage, the faster a user would expect to have their deposit fulfilled. [Relayers assume finality risk](user-roles.md#relayer) so there is a fundamental cap on how quickly a deposit will be fulfilled.&#x20;

Typically, users can expect to receive their funds in 1–4 minutes due to the speed of relayers funding users' transfer requests upfront. Deposits that originate on chains with more frequent chain reorganizations (like Polygon) or longer block times (like Ethereum) will take longer to fulfill due to finality risk.&#x20;

Any deposit fulfilled by a relayer will be referred to as a "Fast" fill. If relayers collectively don't have enough capital to fulfill a deposit, or the deposit has set too low of a relayer fee, then Across will use LP funds to "Slow" fill the deposit.

Relayers wait through the challenge period, taking on 2 hours worth of liveness (instead of the user) before receiving their refund from the liquidity pool.

## Slow Fills

In the event that relayers do not fill a deposit, it can be "slow filled" using LP capital. This means that an [Across Dataworker](user-roles.md) has flagged the deposit as being unfilled and wants the system to use its funds to fill the depositor. The depositor gets refunded the relayer fee in this case because the fill will take a longer time to complete.

Since the slow fill is included in a dataworker's bundle, the fill will take as long as the optimistic challenge window takes to complete.

A dataworker is made aware of these unfilled deposits by relayers who send partial fills for these deposits. These partial fills might look strange to users because they are "1 wei" fills: fills for 1 wei of the full deposited amount. This partial fill is important because it lets the dataworker know whether a deposit already has a slow fill payment enqueued for it.

## What affects the speed of the relayers?&#x20;

The speed of the relayers is mostly dependent on the relay code and bespoke deployment settings, which can be heavily optimized. People are economically incentivized to create exceptionally fast bots, as they want to earn fees paid by users when using across. These fees are set by the user and are a percentage of the deposited amount (to relay from origin to destination chain).

Finality risk is also a big factor when running a relayer, as mentioned above.

## A marketplace for exchanging investment time horizons

Across has low fees and a great user experience for depositors because it elegantly enables agents, who are willing to lend capital for medium and long term time horizons (Relayers, LP's), to match with agents who are willing to pay for a short term loan (Depositors).&#x20;

Depositors signal their desire to have funds on a destination chain _instantaneously;_ relayers lend their funds to the depositor on the destination chain for a _medium term (e.g. two hours)_, and LP's are willing to lend their funds as a fallback to "slow fill" any deposit or to refund a relayer. LP capital is essentially the "capital of last resort" for the Across protocol.

In order to act as the capital of last resort, LP capital is allocated throughout the system (i.e. across its HubPool and SpokePools deployed on each chain) to fulfill these slow fills and refund relayers. LP capital therefore can get stuck in the canonical bridges connecting chains when the system wants to reallocate the LP capital. These canonical bridges can freeze funds for a long time (up to seven days for optimistic rollup canonical bridges), so LP's intrinsically must have the longest time horizon within the Across system.

## User fees are lowered by relayer competition

Another reason why Across has such low fees is that it provides a marketplace for relayers to compete to fill user deposits. Relayers can tune how much finality risk they're willing to take on in order to win the most profitable deposits.&#x20;

We imagine that relayers will eventually specialize in which tokens and destination chains they cover, allowing them to dominate their niche of the relayer market.

You can think of the relayer competition as functioning like an auction. If the auction expires without a clearing price, then the Across system falls back to the LP capital to fulfill the deposit.

This process ensures that depositors have the best chance to bridge their funds cheaply and quickly without sacrificing guaranteed execution.

## An optimistic approach to bridging

Across is able to do near-instantaneous transfers because we operate optimistically.&#x20;

In our optimistic approach, the relayer fulfills users' deposits, which can be thought of as providing a loan to the user in exchange for a small fee. The relayer is fronting the money to the user because it trusts UMA’s optimistic oracle. Across differs in this sense as many other chains require multiple sign-offs, blocking the relayer from quickly performing the relay. Nothing is blocking our relayer.

By functioning optimistically relayers [relay instantly](http://across.to/), and are then refunded after a 2-hour challenge period. During this two-hour challenge period, the user is now out of the picture - they have already received their funds from the relayer. The relayer is trading places with the user in the sense that they’re willing to wait for the challenge window to complete in exchange for a small fee paid by the user.&#x20;

If something is disputed during the challenge period, the user does not endure any penalties. The user is completely out of the picture and does not accept any risk in this sense when bridging with Across, only the relayer does.

##
