# Security Model

Across builds on UMA's optimistic oracle. The optimistic oracle depends on a one-step escalation game that allows _anyone_ to propose the answer to certain types of questions and, if this answer is undisputed, then the answer becomes "verified" after a (relatively short) dispute window. As long as users of the optimistic oracle believe that false answers would be disputed and punished, then we would only see truthful answers proposed in equilibrium. It only takes one honest actor to dispute and stop invalid transfers. This means that usable answers should be produced within the dispute period.

In practice, this system has performed well and has secured hundreds of millions of dollars of value without any issues. For more information on the optimistic oracle, we refer users to [UMA's optimistic oracle documentation](https://docs.umaproject.org/getting-started/oracle#optimistic-oracle).

[In Across, the dataworker](user-roles.md#dataworker) proposes to the optimistic oracle batches of valid refunds that Across should pay out as well as reallocations of LP capital that Across should make to [optimize for LP capital efficiency.](how-across-guarantees-transfers.md#a-marketplace-for-exchanging-investment-time-horizons)
