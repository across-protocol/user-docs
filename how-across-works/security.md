---
description: Across Protocol's primary focus is its users' security.
---

# Security

Across is secured by UMA's optimistic oracle. The optimistic oracle depends on a one-step escalation game that allows _anyone_ to propose the answer to certain types of questions and, if this answer is undisputed, then the answer becomes "verified" after a (relatively short) dispute window. As long as users of the optimistic oracle believe that false answers would be disputed and punished, then we would only see truthful answers proposed in equilibrium. It only takes one honest actor to dispute and stop invalid transfers. This means that usable answers should be produced within the dispute period.

Since launch in 2021, this system has secured hundreds of millions of dollars of value for Across. For more information on the optimistic oracle, we refer users to [UMA's optimistic oracle documentation](https://docs.umaproject.org/getting-started/oracle#optimistic-oracle).

At Across, the Dataworker proposes to the optimistic oracle batches of valid refunds that Across should pay out as well as reallocations of LP capital that Across should make to [optimize for LP capital efficiency.](speed.md#a-marketplace-for-exchanging-investment-time-horizons)

**Canonical Token Maximalism**&#x20;

Across exclusively transfers canonical (genuine) assets, never minted representative assets, which introduce trust assumptions and can put users funds at risk. When users send funds cross-chain via Across, relayers use their own capital to front the users assets on the destination chain and wait to get repaid by the user's original funds on via the canonical (or official) bridge.
