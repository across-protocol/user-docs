# UMIP-157

The Across smart contracts plus the [UMIP](https://github.com/UMAprotocol/UMIPs/blob/master/UMIPs/umip-157.md) provide the fundamental rules of the Across Protocol. The Relayer and Dataworker are simply roles that anyone can assume in exchange for earning rewards and securing the system.

Risk labs provides [open source, opinionated implementations of the Relayer and Dataworker](https://github.com/across-protocol/relayer-v2/tree/master) but there technically many ways to customize the behavior of the software.

## Who should care about UMIP-157

* Relayers: must submit fills with fees that are valid as described by the UMIP
* Dataworkers: must submit bundles containing refunds, rebalances, and slow fills as described by the UMIP
* Fee quoting API: Risk Labs provides a [suggested fees API](https://docs.across.to/v/developer-docs/developers/across-api#calculating-suggested-fees) that depositors, front ends, and relayers can use to check estimated fees for a deposit at a point in time. This fee API should implement fees based on UMIP-157 otherwise it risks that its clients set fees that are too low or too high.
