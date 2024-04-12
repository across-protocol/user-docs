---
description: >-
  The Across referral rewards program offers bridge users a way to earn $ACX for
  using Across.
---

# Referral Rewards

## Program Details

The Across referral rewards program lets people earn $ACX for introducing friends to bridging with Across. Anyone who gets referred to Across is also eligible to earn $ACX through this program and link creators themselves can even earn by using their own link!

This program covers 40-80% of Across bridge fees, offering huge savings on transfers. Your referral tier will rise as per the criteria in the chart below. Once rewards are claimed your tier will be reset to the Copper level. Create your referral link [here](https://across.to/rewards/referrals).

<figure><img src="../../.gitbook/assets/image (2).png" alt=""><figcaption><p>Note: Claiming referral rewards will reset your tier to Copper.</p></figcaption></figure>

The referrer receives 75% of the reward, while the new user gets the remaining 25%. For example, for referrers on the Copper tier, the new user they refer receives 10% of their 40% bridge fee allocation.

**You can see referral rewards in actions each time you bridge, but you must ensure that you are copying your referral link into your browser each time you need to make a transfer.**

<figure><img src="../../.gitbook/assets/image (3).png" alt=""><figcaption><p>By using a referral link, you can save up to 80% on bridge fees!</p></figcaption></figure>

## FAQ

1. **Does the bridge user (i.e. the "referee") earn rewards?**\
   Yes, referral rewards will be split between the referrer (75%) and the referee (25%).
2. **Can a referrer refer themselves?**\
   Yes. In this case, the referrer would earn 100% of the referral rewards.
3.  **How are referral rewards calculated per deposit?**\
    The referral rewards earned by a referrer are proportional to the bridge fees [(explained more here)](https://docs.across.to/how-across-works/fees) paid by a user.  The formula is provided and explained below. Each referrer has a "referral tier" (based on their historical referred volume + number of unique wallets referred) which ranges from 40% to 80%. \
    \
    For example, Alex generates a referral link and sends it to Britt. Britt clicks on the link and does a bridge transfer of 10ETH that pays a 0.10% bridge fee. Alex is in the platinum referral tier which rewards 80% of the bridge fee. \
    \
    The referral reward from this bridge transfer is 0.008 ETH (10\*0.0010\*0.80). If ETHUSD is $1000 and ACXUSD is $0.20 then the reward denominated in ACX is 80 ACX (0.008 \* 1000 / 0.20).\
    \
    Referral rewards are split between referrer and referee 75%/25% respectively. So in this example, Alex earns 60 ACX (80\*0.75) and Britt earns 20 ACX (80\*0.25)

    $$
    x = depositAmount
    $$

    $$
    r = referralTier
    $$

    $$
    fee = min(0.12, bridgeFee)
    $$

    $$
    usd = tokenUSDExchangeRate
    $$

    $$
    acx = 1/ACXUSDExchangeRate
    $$

    $$
    B = rewardBoost
    $$

    $$
    referralReward=B*x*r*fee*usd*acx
    $$

    _(Note that the highest bridge fee in the reward calculation is 0.12% of the deposit amount.)_
4. **When did Across start referral rewards?**\
   For bridge transfers before July 11, 2022: Any address that has submitted at least one transaction on Ethereum Mainnet can receive referral rewards. This transaction does not have to be Across-related. The technical check here is that the [account has a nonce](https://help.myetherwallet.com/en/articles/5461509-what-is-a-nonce) greater than 0.\
   \
   After July 11, 2022: Any address can receive referral rewards regardless of its nonce.\
   \
   The different logic before and after the seemingly arbitrary July 11, 2022 date is necessary because the referral tagging logic changed after that day and we needed a way to distinguish addresses from random strings of bytes before it. For those who can read code and are curious, [this code commit to the frontend](https://github.com/across-protocol/frontend-v2/commit/93644eff4a3efcb222b952ed9218b105253776a8) made it far easier to identify eligible referrer accounts and thereafter it is no longer necessary to check a wallet's nonce.
5. **How do referrers receive $ACX?**\
   Referral rewards will be claimable periodically (not continuously) via a claim dApp. Users will always be able to view their pending claimable rewards but the rewards will usually not be claimable right away. Rewards will be distributed in batches and the frequency of these batches is still to be determined. Note that the first set of rewards will not be claimable until the token exists.\
   \
   For those curious, referral rewards will be distributed via [this MerkleDistributor contract](https://github.com/UMAprotocol/protocol/blob/ea52fb022fb8e8b345a8e965a406bd3461cd5e8f/packages/core/contracts/merkle-distributor/implementation/MerkleDistributor.sol) which has been audited by OpenZeppelin and Paladin. The OZ audit report can be found [here](https://blog.openzeppelin.com/uma-continuous-audit/) and the specific section on this contract can be found by searching for "MerkleDistributor". The Paladin report can be found [here](https://paladinsec.co/projects/covenant/).
6. **Does my referee need to click my referral link each time for me to reap the rewards?**\
   No. Unless your referee clicks on another referral link, they will be linked to you for all of their transfers. The referral links are "sticky."
7. **Does my referral reward tier change after I claim rewards?**\
   Yes. If you claim your rewards, you will forfeit your referral tier status _and_ existing referrer addresses will no longer accrue to you. Your volume and number of referrals reset back to 0. You start from the beginning again at the **Copper** tier. &#x20;
8.  **How do we know whether a bridged transfer originated via a custom referral URL?**\
    This section explains how bridged transfers are ultimately associated with referrer addresses. \
    \
    Do we store all such transfers in a database? The answer is that referrer data is appended to the end of bridged transaction [calldata](https://docs.soliditylang.org/en/v0.8.13/internals/layout\_in\_calldata.html). \
    \
    Specifically, the referrer address should follow a special 8 byte delimiter: "0xd00dfeeddeadbeef". Here's [example React.js code](https://github.com/across-protocol/frontend-v2/blob/93644eff4a3efcb222b952ed9218b105253776a8/src/utils/format.ts#L104) that implements this tagging.\
    \
    This is an example transaction for a deposit from Arbitrum: [https://arbiscan.io/tx/0x1f4c7c0dc54171ebb965cba21ce7deffa6298edc2e9503a8e411e146ffef5876](https://arbiscan.io/tx/0x1f4c7c0dc54171ebb965cba21ce7deffa6298edc2e9503a8e411e146ffef5876). If you click on the transaction page and go to the "Input Data" field, we can see the "calldata". The last 28 bytes are highlighted and is (1) 8 byte delimiter + (2) the referrer's address (1 byte equals 2 characters, so "9a" is 1 byte). To be clear, in this example the referrer address is "0x9a8f92a830a5cb89a3816e3d267cb7791c16b04d".\


    ![](<../../.gitbook/assets/Screen Shot 2022-07-08 at 12.16.35.png>)

    Users who navigate to [across.to](https://across.to/) via a referral URL will automatically have their transactions tagged by this [piece of code ](https://github.com/across-protocol/frontend-v2/blob/93644eff4a3efcb222b952ed9218b105253776a8/src/utils/format.ts#L104)in the [React](https://www.w3schools.com/whatis/whatis\_react.asp) dApp. This dApp enables users to call the Across contracts directly bridge transfers, but it's also possible to call the Across contracts via another contract. This is how [Socket, a bridge aggregator](https://docs.socket.tech/socket-api/contracts), routes bridge transactions to Across.\
    \
    Referrer tags can be included in any smart contract transaction that ultimately bridges via Across as long as the resultant transaction calldata includes the referrer tag.
