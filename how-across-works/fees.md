---
description: Breaking down how fees are charged in Across
---

# Fees

[Relayers and Liquidity Providers](user-roles.md) earn fees in Across for taking on various risks included in any bridge event, while Users pay these fees.

## How Fees are Implemented In The Code

The Across smart contracts are un-opinionated about how these fees are charged; they only [enforce that a `relayerFeePct` is paid to the relayer and a `realizedLpFeePct` is paid to the LP's.](https://github.com/across-protocol/contracts-v2/blob/master/contracts/SpokePool.sol#L1163) The smart contracts also [enforce that a bundle of refunds (i.e. a bundle that passes the challenge liveness period) pays back relayers who submitted the validated fills.](https://github.com/across-protocol/contracts-v2/blob/master/contracts/HubPool.sol#L618)

On the other hand, the UMIP prescribes how fees _should_ be charged. The Dataworker will propose bundles of refunds to the Across smart contracts, and these bundles _should_ only pass the challenge period if every refund in the bundle is associated with a valid fill that charged the correct fees, as described in the UMIP.

The elegance of this optimistic validation mechanism is that the fee model prescribed in the UMIP can change more rapidly than if it were implemented completely within smart contract code.

For the first time in Across' lifespan, the fee model is undergoing a change. [This Pull Request](https://github.com/UMAprotocol/UMIPs/pulls) describes the transition to a new fee model, dubbed the "UBA" (or "Universal Bridge Adapter") fee model. The rest of this page will explain the pre-UBA and post-UBA fee models.

## Pre UBA Fee Model

### Relayer Fees

When a user submits a deposit request to bridge tokens to a destination chain, they can choose a `relayerFeePct` that is between 0% and 50% of the bridged amount. This portion of the bridge is transferred to the relayer as a payment. The user is free to choose any fee they want to but if they set it too low, then they risk that their deposit is never picked up by a relayer. Ultimately, relayers are incentivized by profits. So, the relayer fee should at a minimum include compensation for the gas cost incurred by the relayer on the destination chain to fulfill the deposit, and the opportunity cost of capital.

* Destination gas fees
  * In order for Across to deliver the tokens to the user on the destination chain, a transaction needs to be submitted on behalf of the user on the destination chain.
  * The destination gas fee encompasses the gas costs associated with this transaction.
* Cost of capital
  * A relayer is repaid after their fill is included in a bundle that passes the optimistic challenge period. This is currently set to two hours, so the relayer has essentially loaned its capital to Across for two hours.

Relayers can choose where to take repayment for any fill, and in the pre UBA model, the choice of repayment chain doesn't affect the relayer's fees.&#x20;

_This is arguably a bug in the design of Across and is part of the reason why Across is undergoing a transition to the UBA fee model. The issue introduced by not making repayment chain choice affect the relayer fee is that the LP capital can end up over utilized._

_In the absence of any incentive as to where to take repayment, relayers will generally try to take repayment on the same chain that they submitted the fill on: the destination chain. This can lead to situations where the destination SpokePool is short a lot of funds in times of high bridge volume, which leads to LP capital inflows to that SpokePool and increased utilization for the system._

_Relayers are always repaid out of SpokePool balances. SpokePool balances accumulate in two ways: (1) users deposit into those spoke pools and (2) LP capital is sent from the HubPool to the SpokePool. If there is not enough user deposits to refund relayers, then LP capital must be sent out of the HubPool to pay for the refund. When LP capital is sent out of the HubPool, the system's utilization rises and future user deposits are subsequently charged a higher LP fee. This higher fee helps to protect LP's and also preserve capital in the HubPool that can be used to pay out future_ [_slow fills._](how-across-guarantees-transfers.md)

### LP Fees

LP capital is deposited in the HubPool contract on Ethereum and is used as a reserve pool of capital to send tokens to SpokePools that need to:

* Refund relayers
* Fulfill Slow Fills

The LP fee model is described in detail [here](https://docs.across.to/v/developer-docs/how-across-works/overview/fee-model). The UMIP prescribes that LP fees should be modeled after a lending protocol's fees, like Aave or Compound which are based on utilization. Pre UBA, Across assumes that every single bridge transaction utilizes part of the LP capital to refund the relayer or slow fill the deposit. These fees are typically on the order of 0.06% to 0.12% of the transaction which means that on a 1 ETH transfer you would pay an LP fee of 0.0006 to 0.0012 ETH.

_This is an over aggressive fee model and increases fees for users unnecessarily, because in many cases, the SpokePool's existing balance can be used to refund relayers or fulfill a slow fill. This is another reason why the UBA fee model will result in lower fees for users on average, because it handles gracefully the case where LP capital is not utilized as part of a bridge event._

## UBA Fee Model

The main change to the fee model introduced by the UBA is the concept of "balancing" fees which are incentives paid to depositors and relayers based on SpokePool balances at the time of the bridge. The UBA model has a notion of "target" balances (e.g. 1000 ETH on Optimism, 1000 ETH on Arbitrum and 5000 ETH on Ethereum) and generally if a SpokePool is under balance, then deposit balancing fees will be rewards paid to those who deposit in that SpokePool while refund balancing fees will be penalties charged to relayers who take a refund on that SpokePool. These balancing fees therefore incentivize users to nudge SpokePool balances towards their targets.

These balancing fees will allow Across to reduce its reliance on LP fees, which can be used as a fallback to refund relayers. With the UBA model, the hope is that the balancing fees will cause enough balance to be preserved on SpokePools to pay out all refunds without having to transfer LP funds to that SpokePool.

### Relayer Fees

Relayers are paid the same fees as in the Pre UBA fee model but are charged (or possibly rewarded) an additional balancing fee, which incentivizes them to take refunds on chains that have sufficient existing token balance to pay out the refund without having to dip into LP capital. This balancing fee addresses the issue in the pre UBA model where the choice of repayment chain did not impact the relayer's net refund (see above); in the UBA fee model, the choice of repayment chain now affects the net relayer fee.

As before, the relayer fee is set by the user and should compensate the relayer for the costs their incur plus add an incentive on top since the relayer is assumed to be profit maximizing. The components at a minimum should include:

* Destination gas fee
* Cost of capital
* Refund Balancing Fee
  * The user will not know deterministically where the relayer will take their refund. The user can make a smart guess as to this choice, however, by evaluating spoke pool balances at the time of deposit and picking a chain that has a SpokePool balance at or above its target. Moreover, the user can also assume that all choices being equal, the relayer would prefer to maintain its funds on the same chain that it submitted the fill. So a simple heuristic would be to assume that the relayer will take their refund on the destination chain, if profitable, or the chain with the highest spoke pool excess balance above target.

As before, the protocol contracts allow the depositor to modify the relayer fee post-deposit by sending an update transaction. This might be more relied upon in the UBA model if the relayer fees are not sufficiently high to account for all fee components explained above.

### LP Fees

In the UBA model, the LP fee is paid to the system as usual. In the pre UBA fee model, the LP fee only comprised a utilization fee component, which assumed that every bridge would utilize LP fees. As mentioned, this is not always the case. Therefore, the UBA fee model has a utilization component that is non-zero only when LP capital is taken away from Ethereum.&#x20;

The UBA utilization formula is explained in detail here (TODO add link). The important thing to note is that the utilization fee is a reward for any deposits on Ethereum (because they added capital to Ethereum) and a penalty for any deposits to Ethereum (this assumes the relayer will take their refund on Ethereum, which subtracts capital from Ethereum).

In addition to the utilization fee, a balancing fee is charged to the depositor similar to the refund balancing fee described above. The depositor will be given a reward if they deposit to a SpokePool that is under balance and charged a penalty if the SpokePool is over balance.

In summary, the fee paid to the system or the "LP Fee" in the UBA model is comprised of:

* Utilization fee
* Deposit Balancing Fee
