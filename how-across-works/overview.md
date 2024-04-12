# Overview

## How Across Works

When a user submits an order to Across, for example to move assets from chain A to chain B, they deposit funds into a _Spoke Pool_ on chain A, with instructions about where they would like their funds to wind up and the fee that they are willing to pay.

Relayers view these deposits and, once they have verified that the details of the deposit are correct, immediately provide funds to the user on chain B. The user is now satisfied, having received their funds minus any fees and no longer needs to interact with Across.

After the relayer has performed the relay, a proof of that relay and the validity of the original deposit is submitted to the optimistic oracle (OO) and the relayer is reimbursed once this information has been verified by the OO.

The relayer's reimbursement is taken out of a single liquidity pool on Ethereum Mainnet escrowed in a contract called the _Hub Pool_. Liquidity providers ("LP's") to this pool also earn a fee per transfer that is assessed on the user's deposited amount.

The rules for how funds are moved between the L2 _Spoke Pools_ and the L1 _Hub Pool_ to reimburse relayers are explained in [UMIP-157](https://github.com/UMAprotocol/UMIPs/blob/master/UMIPs/umip-157.md). Anyone who wants to move funds between the pools must submit a valid proof to the OO that abides by the rules explained in the UMIP.

To see how this all comes together, check out the chart below showing a complete end-to-end flow of the process.

<figure><img src="../.gitbook/assets/image (1) (1).png" alt=""><figcaption></figcaption></figure>

### Resources

The smart contract code can be found [here](https://github.com/across-protocol/contracts-v2), including implementations of the HubPool and SpokePool.

The smart contracts were [audited by OpenZeppelin](https://blog.openzeppelin.com/uma-across-v2-audit/). The audit report contains a high-level summary of how the smart contract architecture works.

Moreover, [here is a 60-minute explainer ](https://www.youtube.com/watch?v=iuxf6Crv8MI)video of the smart contract architecture. [Slides](https://docs.google.com/presentation/d/1aEq7t7yUfUAFTWug9PLdSDLdZCUJO4q7pGAoB24piZI/edit?usp=sharing) for the explainer video can be found here.



## Ecosystem Roles

### User

A user is someone who bridges assets between L2s and L1 with Across. Users pay relayers and liquidity providers in order to send their tokens instantly across networks that support their token. You can find a step-by-step explainer on bridging [here](https://docs.across.to/how-to-use-across/bridging).&#x20;

### **Relayer**&#x20;

Relayers give out short-term token loans to Users in exchange for fees. Relayers fulfill deposit requests by sending the depositor their desired token on their requested “destination chain”. Relayers will send the recipient the full deposit amount minus a relayer fee, meaning that they will keep the relayer fee as an incentive for crediting the depositor funds.&#x20;

Relayers also assume the[ risk of finality](https://medium.com/across-protocol/dodging-the-finality-bullet-a-guide-to-finality-risk-7a1eef00271a) and take a chance that a deposit request submitted by a user can disappear in a chain [reorganization](https://www.alchemy.com/overviews/what-is-a-reorg) and get paid for taking on this risk by the user.

Relayers have the option to request repayment on any chain, which is a feature uniquely possible to Across because of the LP pool.&#x20;

Generally, relayers take on the following risks when fulfilling a deposit and are compensated accordingly by users:

* cost of capital: relayers send tokens to a user in order to fulfill a deposit and are reimbursed when their valid fill is included in a bundle (see "Dataworker" to learnmore about bundles)
* gas costs: relayers pay gas on destination chains to fulfill deposits
* software risk: an honest relayer might have a bug in its software that sends an invalid fill
* finality risk: a deposit on the origin chain might disappear if the origin chain reorganizes

Anyone with some technical skills can run open source relayer software or implement their own. You can find more information about running relayers [here](https://docs.across.to/v/developer-docs/developers/running-a-relayer).&#x20;

### Liquidity Provider

A liquidity provider or LP is an actor who deposits assets into one of the pools on [Across.to/pool](https://across.to/pool). Liquidity Providers provide the capital that enables relayers to have flexibility about where they want to take a refund in exchange for fees. Moreover, liquidity providers provide capital that can be used to fulfill deposits in the unlikely but possible case that no relayers can fast fill the deposit. You can find the step-by-step process for liquidity providers [here](https://docs.across.to/how-to-use-across/providing-liquidity).&#x20;

Generally, liquidity providers take on the following risks when passively providing liquidity to Across:

* cost of capital: LP's must deposit their tokens into an Across contract on mainnet
* liquidity risk: If Across is experiencing a lot of volume, then there is a chance that so much of the LP capital is reallocated to repaying relayers and fulfilling deposits that not all LP's who want to withdraw can withdraw at the current moment

### Dataworker

Dataworkers support stability and healthy functioning of the system by refunding relayers and moving system assets between networks.  Whitelisted dataworkers are in charge of proposing "bundles" to be optimistically validated by the Across system. These proposers must post a bond when proposing. Anyone can dispute an invalid bundle and earn a dispute bond, which includes part of the proposer's bond. Each bundle contains instructions for:

* Refunding relayers for valid fills
* Sending tokens to SpokePools that can be used to pay such refunds
* Sending tokens to SpokePools that can be used to execute [slow fills](https://docs.across.to/additional-info/faq#how-long-does-it-take-to-receive-my-funds)
* Withdrawing funds originating from deposits on SpokePools back to the HubPool

Each bundle has a list of "bundle end blocks" that mark the last blocks per SpokePool chain queried for that bundle. The start blocks are equal to the previous bundle's end blocks + 1. The bundle end blocks can be used to verify that the bundle's are correct for the data contained within the bundle's block range.

Finally, the bundle's summarize their instructions via merkle roots, so each bundle contains:

* bundle end blocks
* pool rebalance merkle root: instructions for net inflows/outflows to each spoke pool
* relayer refund merkle root: all relayers that need to be refunded and their aggregate refund
* slow relay merkle root: which deposits need to be slow filled because a relayer hasn't fully filled it&#x20;

The dataworker's responsibility is described in this [UMIP](https://github.com/UMAprotocol/UMIPs/blob/master/UMIPs/umip-157.md) and a reference implementation can be found [here](https://github.com/across-protocol/relayer-v2/blob/master/src/dataworker/Dataworker.ts). An example proposal transaction can be seen [here](https://etherscan.io/tx/0x2ec485712acd7ae75ba6ca1aa0485c700811b7ea4ac4f428ec48838006a3ae40).
