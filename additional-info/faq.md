---
description: Read through some of our most common FAQs.
---

# FAQ

### What is Across?

Across is a cross-chain bridge for L2s and rollups secured by UMA's optimistic oracle. It is optimized for capital efficiency with a single liquidity pool, a competitive relayer landscape, and a no-slippage fee model.

Designed by the engineers who built UMA, Across was the result of approaching bridging not only as a technical concern but as a financial engineering concern.

### How long does it take to receive my funds?

Across' bridging speed depends on the number of relayers and the speed at which they are relaying.

The typical transfer occurs within 1-4 minutes. This occurs when relayers have sufficient assets on the destination chain.  If relayers have insufficient assets on the destination chain, but have excess assets on Mainnet, they will be sent to destination to complete the relay.  This process can take 10-30 minutes for the user transaction to complete.  If there are not enough assets on the destination chain plus Mainnet, the transfer will be slow relayed which can take 2-4 hours.  All of this will be communicated upfront for users in the 'time to destination' field.  If you have not received your funds within the quoted 'time to destination' value, please reach out to Dev Support in the [Across Discord](http://discord.across.to/).&#x20;

### Where can I use Across?

Across currently supports Ethereum mainnet, Arbitrum, Boba, Optimism, and Polygon.

You can find this list on the [Supported Chains and Tokens page](https://docs.across.to/how-across-works/supported-chains-and-tokens).

### What tokens can I bridge with Across?

Across currently supports bridging ACX, ETH, WETH, WBTC, USDC, DAI, BAL, POOL, SNX, and UMA.

You can find this list on the [Supported Chains and Tokens page](https://docs.across.to/how-across-works/supported-chains-and-tokens).

### What is a liquidity provider?

A liquidity provider (LP) is someone that provides liquidity to one of the Across pools. This liquidity is used to reimburse relayers after the relay has been verified by the optimistic oracle.&#x20;

In return for providing this liquidity, LPs receive fees. These fees are described on the [Fees page](https://docs.across.to/reference/fees-in-the-system).

Provided there is enough liquidity in the pool, a liquidity provider can withdraw their position at any time.

### What does a relayer do?

A relayer enables users to make instantaneous transfers between chains by providing the capital upfront. In return for providing this service, they are able to collect fees from the users.

To learn about how to run a relayer, visit the [Running a Relayer page](https://docs.across.to/v/developer-docs/developers/running-a-relayer) in our [developer docs](https://docs.across.to/v/developer-docs).&#x20;

### **When were the snapshots taken for users and LPs?**

The snapshot for early users was taken on July 19th, 2022 at midnight UTC (i.e. no transfers on the 19th are included).

The snapshot for the Bridge Traveler program was taken on September 1st, 2022 at midnight UTC (i.e. no transfers in September are included.)

The snapshot for liquidity provider airdrop eligibility was taken on November 22nd, 2022 at midnight UTC. LPs could earn ACX for the airdrop by being an LP up to this date.&#x20;

You can see the allocation scripts [here.](https://github.com/across-protocol/acx-drop)

### **Who is Risk Labs and what role do they play as a foundation?**

Risk Labs is a foundation that supports the UMA protocol, which is the optimistic oracle that secures Across.

The Risk Labs foundation supports a team working on Across, full-time. Risk Labs will work alongside the DAO to iterate on the design of the bridge and drive adoption.

### **How can I help Across win?**

Join the [Across community in Discord](https://discord.across.to), [bridge with Across](https://across.to/), [LP in our pools](https://across.to/pool), and participate in governance!

### How do I make contact?

If you have questions or want to connect with the Across community, join our [Discord](https://discord.across.to) or follow us on [Twitter](https://twitter.com/AcrossProtocol). Our dev support currently operates through Discord.&#x20;
