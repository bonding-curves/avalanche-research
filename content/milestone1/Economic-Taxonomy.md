---
title: Avalanche Economic Primitives
---

**Last Updated:** November 28, 2025
**Draft Stage:** 3rd Draft

# Avalanche Economic Primitives

This document introduces the foundational economic mechanisms that govern the Avalanche network. These primitives—token issuance, staking, fees, and governance—form the building blocks of Avalanche's cryptoeconomic design and shape how value flows through the ecosystem.

For technical specifications of how these primitives interact as a dynamic system, see the [Differential Specification](/milestone3/Differential_Specification). For analysis of participant roles, see [Participant Roles Taxonomy](/milestone1/Participant-Roles-Taxonomy). For the broader macroeconomic context, see [Avalanche Economy relative to the Open Economy](../milestone1/Avalanche-Economy-relative-to-the-Open-Economy).

---

## Overview

The Avalanche economic model balances two fundamental forces: **inflation** (the cost of network security through staking rewards) and **deflation** (the value captured through fee burning). This tension creates a self-regulating system where network usage directly affects token scarcity.

| Primitive | Purpose | Key Mechanism |
|-----------|---------|---------------|
| Token Issuance | Define monetary supply | Fixed 720M cap with gradual release |
| Staking | Secure the network | Rewards proportional to stake and duration |
| Fee Structure | Price network resources | 100% fee burn creates deflationary pressure |
| L1 Economics | Enable sovereign chains | Continuous fees for validator resources |
| Governance | Evolve the protocol | Hybrid on-chain/community-driven process |

---

## Token Issuance

AVAX has a hard cap of 720 million tokens. At mainnet launch, 360 million tokens were available, with the remaining 360 million released gradually through staking rewards over time. This fixed supply model creates long-term scarcity while ensuring sufficient tokens for network security.

All tokens were created at genesis—there is no ongoing mining mechanism beyond staking rewards. The emission rate depends on network participation: rewards are calculated based on the gap between current supply and maximum supply, meaning emission naturally slows as the cap approaches. At current rates, the maximum supply would be reached in approximately 27 years, though this timeline is subject to governance decisions.

The community retains governance rights over long-term monetary policy, including the potential to adopt deflationary mechanisms through transaction fee burning. With over 4.6 million AVAX already burned through fees, the network has demonstrated meaningful deflationary capacity during periods of high activity.

---

## Staking Economics

Avalanche secures its network through proof-of-stake, where validators lock AVAX to participate in consensus. The staking system is designed around positive incentives rather than punitive measures—a distinctive feature that differentiates Avalanche from networks that implement slashing.

### Validator Requirements

The minimum stake to operate a validator is 2,000 AVAX. Validators must maintain at least 80% uptime to receive rewards; falling below this threshold results in reward forfeiture but not loss of principal stake. This "proof-of-uptime" approach reduces operator risk while maintaining network reliability.

To prevent excessive centralization, validator weight is capped at the lesser of 3 million AVAX or 5 times the validator's own stake. This means a validator with 100,000 AVAX can accept at most 400,000 AVAX in delegations, ensuring stake remains distributed across the network.

### Reward Structure

Staking rewards currently average 7-9% APR, varying with network participation levels and lockup duration. Longer commitments yield higher returns: the reward rate scales linearly from a minimum consumption rate (10%) at 2-week lockups to a maximum consumption rate (12%) at 52-week lockups. Rewards continue until the maximum supply is reached.

### Delegation

Token holders who prefer not to operate validator infrastructure can delegate their AVAX to existing validators. The minimum delegation is 25 AVAX. Delegators receive rewards proportional to their stake minus a commission fee (minimum 2%) set by the validator. This mechanism allows broad participation in network security while maintaining operational simplicity.

### No Slashing

Unlike Ethereum and many other proof-of-stake networks, Avalanche does not implement slashing penalties. Underperforming validators forfeit rewards but never lose their staked principal. This design choice reduces the risk profile for validators and delegators, though it places greater reliance on the consensus mechanism itself for Byzantine fault tolerance.

---

## Liquid Staking

Liquid staking protocols allow AVAX holders to earn staking rewards while maintaining liquidity. These protocols stake AVAX on users' behalf and issue liquid staking tokens (LSTs) that represent the staked position plus accrued rewards.

The major providers include:

- **BenQi (sAVAX)**: The largest liquid staking protocol on Avalanche, with over $250M in total value locked. Users stake on the C-Chain directly without bridging to P-Chain.
- **Hypha (ggAVAX)**: Formerly GoGoPool, focused on enabling permissionless validator participation through minipools.
- **Ankr (ankrAVAX)**: Part of Ankr's multi-chain liquid staking infrastructure with minimums as low as 1 AVAX.

LSTs can be deployed across DeFi protocols for lending, borrowing, and liquidity provision—enabling dual yield streams from both staking and DeFi activities. The Avalanche Foundation's Icebreaker Program supports LST adoption by deploying AVAX to bootstrap liquidity.

While LSTs trade freely on secondary markets, redeeming the underlying AVAX requires waiting for the staking lockup to expire (up to 4 weeks). Liquid staking also introduces smart contract risk and potential concerns around recursive leverage, where LSTs used as collateral could concentrate consensus influence. Protocol governance must monitor these dynamics.

---

## Fee Structure

All transaction fees across the P-Chain, X-Chain, and C-Chain are burned completely rather than redistributed to validators. This 100% fee burn creates a direct relationship between network usage and token scarcity—higher activity increases burning and reduces circulating supply.

### Dynamic Fee Mechanism

The C-Chain implements a dynamic fee mechanism inspired by Ethereum's EIP-1559. Gas prices adjust algorithmically based on network congestion: when demand exceeds the target throughput, fees rise exponentially; when demand falls below target, fees decrease toward the minimum.

Following the Etna upgrade (December 2024), [ACP-125](https://github.com/avalanche-foundation/ACPs/tree/main/ACPs/125-basefee-reduction) reduced the C-Chain minimum base fee from 25 nAVAX to 1 nAVAX—a 96% reduction. This change recognizes that the previous minimum was artificially constraining network usage and allows more accurate price discovery during low-demand periods.

The P-Chain and X-Chain also implement dynamic fees through [ACP-103](https://github.com/avalanche-foundation/ACPs/tree/main/ACPs/103-dynamic-fees), using a multidimensional gas model that accounts for bandwidth, database reads, database writes, and compute time. This comprehensive approach ensures fees reflect the actual resource costs imposed on the network.

### Deflationary Dynamics

Fee burning introduces deflationary pressure that counteracts staking inflation. When burn rates exceed emission rates, the network becomes net deflationary. Currently, daily burns (~1,500 AVAX) remain below daily emissions (~26,500 AVAX), resulting in modest net inflation of approximately 3.8% annually. However, the gap has narrowed significantly—burn rates tripled through 2025 as network activity increased.

The long-term economic health of the network depends on whether fee-driven deflation can outpace security-cost inflation. For detailed analysis of this dynamic, see [Avalanche Economy relative to the Open Economy](/milestone1/Avalanche-Economy-relative-to-the-Open-Economy).

---

## L1 Economics

Layer 1 blockchains (L1s, formerly called Subnets) enable application-specific chains with custom token models, fee structures, and governance parameters while leveraging Avalanche's consensus and interoperability infrastructure.

### Sovereign Economic Models

L1 creators define their own validator requirements and reward mechanisms. L1s may require validators to stake custom tokens rather than AVAX, enabling fully sovereign economic designs. This flexibility supports diverse use cases from gaming to regulated financial applications.

### Continuous Fee Model

Following [ACP-77](https://github.com/avalanche-foundation/ACPs/tree/main/ACPs/77-reinventing-subnets) (activated December 2024), L1 validators pay a continuous dynamic fee to the P-Chain for the computational resources they consume. This replaced the previous requirement that L1 validators also validate the Primary Network with a 2,000 AVAX stake—reducing the barrier to entry by approximately 99.9%.

The continuous fee (~1.33 AVAX/month per validator at baseline) properly meters the persistent load each validator adds to the network. Like other dynamic fees, this rate adjusts based on total L1 validator demand: below the target capacity of 10,000 validators, fees remain minimal; above target, fees increase exponentially to manage demand.

### Interoperability Value

While L1s operate sovereignly, they generate economic value for the Primary Network through cross-chain messaging (Avalanche Warp Messaging), asset bridging, and the continuous validator fees that are burned. Successful L1s create derived demand for Primary Network services, contributing to fee-driven deflation.

---

## Governance Architecture

Avalanche employs a hybrid governance model combining limited on-chain voting with community-driven improvement proposals. This design balances decentralized decision-making with network stability.

### On-Chain Governance

Validators can vote directly on critical network parameters including minimum stake requirements, staking durations, reward emission rates, and fee structures. However, governance is restricted to predetermined parameters rather than allowing arbitrary system modifications—prioritizing predictability over flexibility.

### Avalanche Community Proposals (ACPs)

The primary framework for protocol evolution operates through ACPs, which follow a structured multi-stage process:

1. **Idea Vetting**: Public discussion on GitHub
2. **Formal Proposal**: Drafting and submission via pull request
3. **Proposed Status**: Active community iteration
4. **Implementable Status**: Ready for deployment
5. **Activated Status**: Coordinated network upgrade

Community members voice support through "Straw Polls," but final activation requires coordinated adoption by validators and node operators running compatible client software.

ACPs are categorized into three tracks:
- **Standards Track**: Protocol-level changes (e.g., [ACP-77](/milestone2/ACP-Summaries#acp-77-reinventing-subnets), [ACP-103](/milestone2/ACP-Summaries#acp-103-add-dynamic-fees-to-the-x-chain-and-p-chain))
- **Best Practices Track**: Recommended approaches for builders
- **Meta Track**: Modifications to the ACP process itself

For a comprehensive summary of all ACPs and their economic implications, see [ACP Summaries](/milestone2/ACP-Summaries).

### Governance Safeguards

Economic parameters include built-in hysteresis mechanisms that prevent rapid manipulation. Once a parameter changes, it becomes increasingly difficult to modify the same parameter by large amounts in quick succession—this difficulty decreases gradually over time. Time delays between proposals and activation provide adequate review periods, while range limitations ensure changes occur within economically sustainable bounds.

These safeguards balance decentralized governance with economic stability, protecting against both adversarial manipulation and well-intentioned but destabilizing rapid changes.

---

## References

1. Ava Labs. *Avalanche Platform Whitepaper*. 2020. https://www.avalabs.org/whitepapers

2. Avalanche Foundation. *Avalanche Community Proposals (ACPs)*. GitHub Repository. https://github.com/avalanche-foundation/ACPs

3. Avalanche. *AVAX Token*. Avalanche Builder Hub. https://build.avax.network/docs/quick-start/avax-token

4. Avalanche. *How to Stake*. Avalanche Builder Hub. https://build.avax.network/docs/nodes/validate/how-to-stake

5. Avalanche Foundation. *ACP-77: Reinventing Subnets*. 2024. https://github.com/avalanche-foundation/ACPs/tree/main/ACPs/77-reinventing-subnets

6. Avalanche Foundation. *ACP-103: Add Dynamic Fees to the X-Chain and P-Chain*. 2024. https://github.com/avalanche-foundation/ACPs/tree/main/ACPs/103-dynamic-fees

7. Avalanche Foundation. *ACP-125: Reduce C-Chain Minimum Base Fee*. 2024. https://github.com/avalanche-foundation/ACPs/tree/main/ACPs/125-basefee-reduction

8. BenQi. *Liquid Staking Overview*. https://docs.benqi.fi/benqi-liquid-staking/overview

9. Avalanche. *Etna: Enhancing the Sovereignty of Avalanche L1 Networks*. 2024. https://www.avax.network/about/blog/etna-enhancing-the-sovereignty-of-avalanche-l1-networks
