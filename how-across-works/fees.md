---
description: Breaking down how fees are charged in Across
---

# Fees

[Relayers and Liquidity Providers](user-roles.md) earn fees in Across for taking on various risks included in any bridge event, while Users pay these fees.

## How Fees are Implemented In The Code

The Across smart contracts are un-opinionated about how these fees are charged; they only [enforce that a `relayerFeePct` is paid to the relayer and a `realizedLpFeePct` is paid to the LP's.](https://github.com/across-protocol/contracts-v2/blob/master/contracts/SpokePool.sol#L1163) The smart contracts also [enforce that a bundle of refunds (i.e. a bundle that passes the challenge liveness period) pays back relayers who submitted the validated fills.](https://github.com/across-protocol/contracts-v2/blob/master/contracts/HubPool.sol#L618)

On the other hand, the UMIP prescribes how fees _should_ be charged. The Dataworker will propose bundles of refunds to the Across smart contracts, and these bundles _should_ only pass the challenge period if every refund in the bundle is associated with a valid fill that charged the correct fees, as described in the UMIP.

The elegance of this optimistic validation mechanism is that the fee model prescribed in the UMIP can change more rapidly than if it were implemented completely within smart contract code.

### Relayer Fees

When a user submits a deposit request to bridge tokens to a destination chain, they can choose a `relayerFeePct` that is between 0% and 50% of the bridged amount. This portion of the bridge is transferred to the relayer as a payment. The user is free to choose any fee they want to but if they set it too low, then they risk that their deposit is never picked up by a relayer. Ultimately, relayers are incentivized by profits. So, the relayer fee should at a minimum include compensation for the gas cost incurred by the relayer on the destination chain to fulfill the deposit, and the opportunity cost of capital.

* Destination gas fees
  * In order for Across to deliver the tokens to the user on the destination chain, a transaction needs to be submitted on behalf of the user on the destination chain.
  * The destination gas fee encompasses the gas costs associated with this transaction.
* Cost of capital
  * A relayer is repaid after their fill is included in a bundle that passes the optimistic challenge period. This is currently set to two hours, so the relayer has essentially loaned its capital to Across for two hours.

Relayers can choose where to take repayment for any fill, and the choice of repayment chain doesn't affect the relayer's fees.&#x20;

_This is arguably a bug in the fee model currently and is part of the reason why Across is undergoing a transition to a new fee model with the V3 launch. The issue introduced by not making repayment chain choice affect the relayer fee is that the LP capital can end up over utilized._

_In the absence of any incentive as to where to take repayment, relayers will generally try to take repayment on the same chain that they submitted the fill on: the destination chain. This can lead to situations where the destination SpokePool is short a lot of funds in times of high bridge volume, which leads to LP capital inflows to that SpokePool and increased utilization for the system._

_Relayers are always repaid out of SpokePool balances. SpokePool balances accumulate in two ways: (1) users deposit into those spoke pools and (2) LP capital is sent from the HubPool to the SpokePool. If there is not enough user deposits to refund relayers, then LP capital must be sent out of the HubPool to pay for the refund. When LP capital is sent out of the HubPool, the system's utilization rises and future user deposits are subsequently charged a higher LP fee. This higher fee helps to protect LP's and also preserve capital in the HubPool that can be used to pay out future_ [_slow fills._](how-across-guarantees-transfers.md)

### LP Fees

LP capital is deposited in the HubPool contract on Ethereum and is used as a reserve pool of capital to send tokens to SpokePools that need to:

* Refund relayers
* Fulfill Slow Fills

The LP fee model is described in detail [here](https://docs.across.to/v/developer-docs/how-across-works/overview/fee-model). The UMIP prescribes that LP fees should be modeled after a lending protocol's fees, like Aave or Compound which are based on utilization. Across assumes that every single bridge transaction utilizes part of the LP capital to refund the relayer or slow fill the deposit. These fees are typically on the order of 0.06% to 0.12% of the transaction which means that on a 1 ETH transfer you would pay an LP fee of 0.0006 to 0.0012 ETH.

_This is an over aggressive fee model and increases fees for users unnecessarily, because in many cases, the SpokePool's existing balance can be used to refund relayers or fulfill a slow fill. This is why we are actively researching a more dynamic fee model that will result in lower fees for users on average, because it handles gracefully the case where LP capital is not utilized as part of a bridge event._

