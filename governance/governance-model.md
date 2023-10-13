# Governance Model

## **Overview**

The Across governance process will evolve to meet the needs of Across DAO as it grows, and this is a living document. Anyone can participate in the Across Governance process, and anyone with ACX voting power can vote on proposals.&#x20;

\
Presently, tokenholders control treasury spending and updates to governance.

## **Governance Components**

The Across Governance process follows the pathway from ideation, to draft, to proposal, to implementation. Anything subject to governance will follow this path and be decided on by ACX tokenholders.

### **Governance Toolkit:**

* [Forum](http://forum.across.to): A platform for discussion and deliberation on governance proposals
* [Snapshot](https://snapshot.org/#/acrossprotocol.eth): A platform for where all governance proposals are submitted for vote
* Optimistic Governance (future implementation): A mechanism for trustless execution of snapshot votes.

### **Governance Participants:**

* Across Council – The Council executes approved Snapshot proposals prior to the implementation of optimistic governance. The current signers are Risk Labs representatives.&#x20;
  * Address:  0xB524735356985D2f267FA010D681f061DfF03715
  * Threshold: 3/5&#x20;
  * Signers (eth):
    * 0x1d933Fd71FF07E69f066d50B39a7C34EB3b69F05
    * 0x1f11D8B72fc1B534448436BA60B4B371276DAb33
    * 0x837219D7a9C666F5542c4559Bf17D7B804E5c5fe
    * 0x996267d7d1B7f5046543feDe2c2Db473Ed4f65e9
    * 0xcc400c09ecBAC3e0033e4587BdFAABB26223e37d
* Council addresses on different chains. These are all Gnosis Safe contracts that have the same signers and threshold as above.
  * Ethereum: 0xB524735356985D2f267FA010D681f061DfF03715&#x20;
  * Polygon: 0x5BCBeBAFb2934400525FA53CF74f26Fe4cf75A5B&#x20;
  * Arbitrum: 0xd16D904b68429b93F1DFCD837F61AeDCd224e8F4&#x20;
  * Optimism: 0xfd0CF79C568c08b78484F2D165eB8c7f569BdCf9
*   Committees – Subject matter experts that consider and pursue goals specific to their domain, acting in the best interests of the Across DAO. Committees are able to make updates to parameters without the need for a full tokenholder voting cycle, allowing the bridge to remain adaptive. Shortly after launch, RL will upgrade the protocol to allow for committee implementation.&#x20;


* Voters – anyone who holds ACX, or ACX representative tokens that hold voting power, and participates actively in governance. See the list below for voting-eligible tokens.&#x20;
  * ACX (eth) = 1 vote
    * Address: 0x44108f0223A3C3028F5Fe7AEC7f9bb2E66beF82F
  * ACX LP = 1 vote
    * ACX tokens that have been provided as bridging liquidity within Across Protocol
    * Address: 0xb0C8fEf534223B891D4A430e49537143829c4817
  * ACX ST = 1 vote
    * ACX Success tokens. Min payout of 1 ACX, max payout of 2 ACX
    * Address: 0x4CBD49FCB56bBd06658103ab9fB3Ae0fAfFe365A
  * Staked ACX LP = 1 vote
    * Staked ACX LP tokens within Across
    * Multiplied by the current exchange rate of ACX-LP to ACX
  * Staked ACX Rewards
    * Unclaimed rewards accrued for all staked LP tokens within Across
    * Custom strategy for staked voting can be seen [here](https://github.com/snapshot-labs/snapshot-strategies/tree/master/src/strategies/across-staked-acx)
