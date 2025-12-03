---
title: Avalanche Participant Roles Taxonomy
---

**Last Updated:** November 28, 2025
**Draft Stage:** 5th Draft

# Avalanche Participant Roles Taxonomy

This document defines the taxonomy of participant roles within the Avalanche network. Each role represents a distinct way of engaging with the ecosystem—securing the network, providing capital, building applications, or supporting infrastructure. Understanding these roles clarifies how value flows through the system and how different participants contribute to network health.

For the economic primitives that govern these roles, see [Economic Taxonomy](/milestone1/Economic-Taxonomy). For the technical mechanisms enabling participation, see [Mechanism Taxonomy](/milestone1/Mechanism-Taxonomy). For broader macroeconomic context, see [Avalanche Economy relative to the Open Economy](/milestone1/Avalanche-Economy-relative-to-the-Open-Economy).

---

## Overview

Avalanche's participant ecosystem spans three functional domains: network security (validators and delegators who secure consensus), economic activity (token holders and application users who generate demand), and ecosystem development (builders and organizations who expand capabilities).

| Role | Category | Primary Function | Capital Requirement |
|------|----------|------------------|---------------------|
| Primary Network Validator | Security | Consensus participation | 2,000 AVAX minimum |
| L1 Validator | Security | L1-specific consensus | ~1.33 AVAX/month (continuous fee) |
| Delegator | Security | Stake delegation | 25 AVAX minimum |
| Liquid Staking Participant | Security/Economic | LST-based staking | Varies by protocol (1-25 AVAX) |
| Token Holder | Economic | Capital provision | Any amount |
| Application User | Economic | Network utilization | Transaction fees |
| Trader/Liquidity Provider | Economic | Market efficiency | Variable |
| Developer | Ecosystem | Application building | Deployment costs |
| Infrastructure Provider | Ecosystem | Service provision | Infrastructure costs |
| Ava Labs | Ecosystem | Protocol development | N/A |
| Avalanche Foundation | Ecosystem | Ecosystem stewardship | N/A |

These roles are not mutually exclusive—a single entity may fulfill multiple roles simultaneously. A validator might also be a developer, a token holder might delegate while using applications, and infrastructure providers often hold significant stake.

---

## Network Security Participants

This category includes roles directly responsible for network consensus and security. These participants stake capital or delegate to those who do, collectively securing the Primary Network and its L1 ecosystems.

### Primary Network Validator (PNV)

A Primary Network Validator operates a full node that participates in the consensus of all three Primary Network chains (P-Chain, X-Chain, and C-Chain) by staking AVAX.

**System Functions:**
- Validate and produce blocks on the Primary Network
- Participate in Snow consensus by repeatedly sampling other validators
- Maintain the state of all three Primary Network chains
- Register BLS public keys for cross-chain message signing
- Optionally validate additional L1 blockchains

**Participation Requirements:**
- **Minimum Stake:** 2,000 AVAX
- **Uptime:** Must maintain >80% uptime (measured by peer sampling) to receive rewards
- **Hardware:** 8 vCPU, 16 GB RAM, 1 TB SSD, 5+ Mbps internet
- **BLS Key:** Must register a BLS key pair on P-Chain (per [ACP-62](/milestone2/ACP-Summaries#acp-62))

**Configurable Parameters:**
- **Staking Duration:** 2 weeks minimum, 1 year maximum
- **Delegation Fee:** 2% minimum (average ~7%)

**Economic Incentives:**
- **Inflows:** Staking rewards from network issuance (currently 7-9% APR, varying with stake duration and network participation)
- **Outflows:** Hardware, bandwidth, and operational costs (no transaction fee revenue—all fees are burned)

Longer stake commitments yield higher rewards: the effective consumption rate scales linearly from 10% (2-week minimum) to 12% (1-year maximum). This creates approximately 11% additional reward potential for maximum-duration stakes.

**Risk Model:**
- **No Slashing:** Principal stake is never reduced for any reason
- **Reward Forfeiture:** Rewards are forfeited if uptime drops below 80% during the staking period

**Validator Weight Limits:**
A validator's total weight (own stake plus delegations) cannot exceed the lesser of 3 million AVAX or 5× their own stake. This cap prevents excessive concentration while allowing efficient delegation.

For consensus mechanics, see [Mechanism Taxonomy: Snow Consensus](/milestone1/Mechanism-Taxonomy#the-snow-protocol-family).

---

### L1 Validator (L1V)

An L1 Validator participates in the consensus of a specific Layer 1 blockchain (formerly called a Subnet), operating independently from Primary Network validation.

**System Functions:**
- Validate and produce blocks for a specific L1
- Maintain the state of that L1's blockchain
- Sign Avalanche Warp Messages (AWM) for cross-chain communication
- Execute L1-specific consensus rules defined by the Validator Manager contract

**Participation Requirements:**
- **L1-Defined:** Each L1 sets its own validator requirements through its Validator Manager contract (e.g., stake a native L1 token, hold an NFT, pass KYC verification)
- **P-Chain Fee:** Continuous dynamic AVAX fee to remain registered (~1.33 AVAX/month at baseline per [ACP-77](/milestone2/ACP-Summaries#acp-77-reinventing-subnets))
- **Hardware:** As specified by the L1 (typically similar to Primary Network requirements)

The continuous fee model introduced by [ACP-77](/milestone2/ACP-Summaries#acp-77-reinventing-subnets) replaced the previous requirement that L1 validators also validate the Primary Network with a 2,000 AVAX stake. This reduced the barrier to L1 validation by approximately 99.9%, enabling more diverse L1 ecosystems.

**Fee Dynamics:**
- Below target capacity (10,000 L1 validators): fees remain at baseline (~1.33 AVAX/month)
- Above target: fees increase exponentially to manage demand
- Maximum capacity: 20,000 L1 validators network-wide

**Economic Incentives:**
- **Inflows:** L1-native token rewards, share of L1 transaction fees, or other L1-defined compensation
- **Outflows:** Hardware and operational costs; continuous AVAX fee (burned on P-Chain)

**Risk Model:**
Defined by each L1's Validator Manager contract. May include slashing of L1 native tokens, reward forfeiture, or other penalties specified by L1 governance.

---

### Delegator

A Delegator is a passive participant who contributes to network security by delegating AVAX to an existing Primary Network Validator, earning rewards without operating infrastructure.

**System Functions:**
- Select a Primary Network Validator to delegate stake to
- Lock AVAX for a specified staking duration
- Claim rewards upon delegation completion

**Participation Requirements:**
- **Minimum Stake:** 25 AVAX
- **Duration:** 2 weeks minimum, 1 year maximum (must not exceed validator's remaining stake period)

**Configurable Parameters:**
- **Validator Selection:** Choice of which PNV to delegate to
- **Stake Amount:** 25 AVAX minimum, no maximum (subject to validator's weight cap)
- **Duration:** Within the 2-week to 1-year range

**Economic Incentives:**
- **Inflows:** Staking rewards proportional to delegated stake, minus validator's delegation fee
- **Outflows:** Delegation fee (2-10%, averaging ~7%)

**Reward Calculation:**
Delegators receive rewards based on the same formula as validators, but pay a percentage fee to their chosen validator. If a validator charges 7% delegation fee and the base reward would be 100 AVAX, the delegator receives 93 AVAX.

**Risk Model:**
- **No Slashing:** Delegated principal is never reduced
- **Reward Forfeiture:** Rewards are forfeited if the chosen validator fails to maintain 80% uptime
- **Validator Selection Risk:** Choosing an unreliable validator results in lost rewards (but not principal)

Research indicates approximately 50% of delegator rewards are re-staked, compared to ~70% for validators—suggesting delegators have shorter investment horizons or greater liquidity needs.

---

### Liquid Staking Participant

A Liquid Staking Participant stakes AVAX through a liquid staking protocol, receiving a tradeable token representing their staked position plus accrued rewards.

**System Functions:**
- Deposit AVAX to a liquid staking protocol
- Receive liquid staking tokens (LSTs) representing the staked position
- Use LSTs in DeFi protocols while earning staking rewards
- Redeem underlying AVAX when unstaking (subject to lockup periods)

**Major Protocols:**
- **BenQi (sAVAX):** Largest LST on Avalanche (~$250M TVL), stake directly on C-Chain
- **Hypha (ggAVAX):** Formerly GoGoPool, enables permissionless minipool validation
- **Ankr (ankrAVAX):** Multi-chain liquid staking with minimums as low as 1 AVAX

**Participation Requirements:**
- **Minimum:** Varies by protocol (typically 1-25 AVAX)
- **Technical:** C-Chain wallet capable of interacting with staking contracts

**Economic Incentives:**
- **Inflows:** Staking rewards (reflected in LST value appreciation), DeFi yields from LST deployment
- **Outflows:** Protocol fees (typically 5-10% of rewards), smart contract interaction costs

**Risk Model:**
- **Smart Contract Risk:** Protocol vulnerabilities could affect staked funds
- **Liquidity Risk:** LST secondary market liquidity may vary; redemption requires waiting for unstaking period
- **Recursive Leverage Risk:** Using LSTs as collateral creates liquidation exposure during market volatility
- **Concentration Risk:** Large LST protocols may accumulate significant consensus influence

Liquid staking enables dual yield streams—base staking rewards plus DeFi yields—but introduces additional complexity and smart contract dependencies not present in direct staking.

For liquid staking protocol details, see [Economic Taxonomy: Liquid Staking](/milestone1/Economic-Taxonomy#liquid-staking).

---

## Economic & Utility Participants

This category covers roles that generate demand, provide liquidity, and create utility within the Avalanche economy. These participants drive network activity and contribute to the fee-burning mechanism that creates deflationary pressure.

### Token Holder (AVAX)

A Token Holder is any entity controlling AVAX, the network's native asset. This foundational role enables all other forms of participation.

**System Functions:**
- Hold and transfer AVAX across P-Chain, X-Chain, and C-Chain
- Pay transaction fees (100% burned, contributing to deflation)
- Supply capital for staking, delegation, or liquid staking
- Participate in ecosystem governance through validator support

**Participation Requirements:**
- Control of a private key (self-custody wallet or custodial service)

**Economic Incentives:**
- **Inflows:** Token acquisition, staking/delegation rewards, DeFi yields, price appreciation
- **Outflows:** Transaction fees (burned), opportunity costs of holding vs. staking

**Fee Burning Economics:**
Unlike networks that distribute fees to validators, Avalanche burns 100% of transaction fees. This creates a direct relationship between network usage and token scarcity:
- Current daily burn rate: ~1,500 AVAX
- Current daily emission rate: ~26,500 AVAX (staking rewards)
- Net inflation: ~3.8% annually (narrowing as burn rates increase)

Token holders benefit from fee burning through increased relative scarcity, even without actively staking. High network activity periods can produce net deflationary days.

**Governance Rights:**
Token holders do not vote directly on protocol parameters. Instead, governance influence flows through validator selection (choosing which validators to delegate to) and community participation in the ACP process. Validators can vote on specific network parameters.

**Risk Model:**
- Market price volatility
- Custody risk (key management, exchange exposure)
- Inflation dilution if not staking

---

### Application User

An Application User interacts with decentralized applications and smart contracts deployed on the C-Chain or L1 blockchains, generating the transaction activity that drives network utility.

**System Functions:**
- Execute smart contract calls (trades, mints, borrows, stakes)
- Trigger state changes on EVM-compatible chains
- Consume blockspace and computational resources
- Generate transaction fees (burned)

**Participation Requirements:**
- Wallet capable of signing and submitting transactions
- Sufficient AVAX (or L1 native tokens) for gas fees

**Configurable Parameters:**
- **Priority Fee:** Higher tips for faster transaction inclusion during congestion
- **Gas Limit:** Maximum computation willing to pay for

**Economic Incentives:**
- **Inflows:** Application-specific utility (digital assets, yields, services, entertainment)
- **Outflows:** Transaction fees (burned), protocol-specific fees (to dApp developers/treasuries)

**User Categories:**
Application users span diverse activities:
- **DeFi Participants:** DEX trading, lending, yield farming
- **NFT Users:** Minting, trading, gaming assets
- **Gaming Participants:** In-game transactions, asset transfers
- **Enterprise Users:** Tokenized asset interactions, supply chain operations

Post-[ACP-125](/milestone2/ACP-Summaries#acp-125), the C-Chain minimum base fee dropped 96% (25 nAVAX → 1 nAVAX), significantly reducing costs for routine transactions and enabling more accessible application usage.

**Risk Model:**
- Smart contract vulnerabilities
- Asset-specific market risk
- Front-running and MEV exposure

---

### Trader / Investor / Liquidity Provider

This composite role encompasses participants focused on capital allocation, market efficiency, and liquidity provision within the Avalanche DeFi ecosystem.

**System Functions:**
- Provide liquidity to decentralized exchanges and lending protocols
- Execute trades and capture arbitrage opportunities
- Invest in ecosystem assets, derivatives, and structured products
- Facilitate price discovery and market depth

**Participation Requirements:**
- Capital (tokens) to deploy
- Understanding of DeFi mechanics and risks

**Configurable Parameters:**
- Capital allocation strategy
- Risk tolerance and position sizing
- LP fee tiers and concentration ranges

**Economic Incentives:**
- **Inflows:** Trading profits, LP fees, yield farming rewards, lending interest
- **Outflows:** Transaction fees (burned), impermanent loss, protocol fees, capital-at-risk

**Role Distinctions:**
While grouped together, these activities have different risk profiles:
- **Traders:** Directional exposure, execution risk, short time horizons
- **Investors:** Long-term capital appreciation, project selection risk
- **Liquidity Providers:** Fee income vs. impermanent loss tradeoff, concentrated liquidity complexity

**Risk Model:**
- Market volatility and directional loss
- Impermanent loss in AMM positions
- Smart contract and protocol risk
- Counterparty risk in lending protocols
- Liquidation risk in leveraged positions

---

## Ecosystem Participants

This category defines organizational and technical roles supporting network infrastructure, application development, and ecosystem growth. These participants expand Avalanche's capabilities and drive adoption.

### Developer

A Developer builds applications, tools, infrastructure, or new L1 blockchains on Avalanche. This permissionless role drives ecosystem innovation and utility creation.

**System Functions:**
- Deploy smart contracts on C-Chain or L1 blockchains
- Define and launch new L1s with custom Validator Manager contracts
- Build wallets, SDKs, developer tools, and application interfaces
- Contribute to protocol development through the ACP process

**Developer Categories:**
- **Smart Contract Developers:** Build dApps on C-Chain or existing L1s
- **L1 Creators:** Launch application-specific blockchains with custom economics
- **Infrastructure Developers:** Build RPC services, indexers, bridges, SDKs
- **Core Protocol Contributors:** Contribute to AvalancheGo and propose ACPs

**Participation Requirements:**
- Technical skills (no permission required)
- Sufficient AVAX for deployment and testing fees

**Economic Incentives:**
- **Inflows:** Application revenue, protocol fees, L1 token appreciation, ecosystem grants
- **Outflows:** Development costs, audits, deployment fees, infrastructure expenses

**Ecosystem Support:**
Avalanche provides substantial builder support:
- **Codebase Incubator:** Official accelerator for early-stage Web3 startups
- **Retro9000:** Grant program rewarding L1 and tooling development
- **Builder Credits:** Infrastructure cost subsidies for L1 projects

**Risk Model:**
- Project execution and adoption uncertainty
- Smart contract vulnerabilities and liability
- Market timing and competition risk

---

### Infrastructure Provider

An Infrastructure Provider operates services that enable users and developers to interact with Avalanche without running their own nodes.

**System Functions:**
- Operate public or private RPC endpoints
- Run indexers and block explorers
- Provide API and SDK access to blockchain data
- Offer specialized services (oracles, bridges, analytics)

**Provider Categories:**
- **RPC Providers:** Node access for transaction submission and data queries
- **Indexers/Explorers:** Searchable blockchain data (Avascan, Snowtrace)
- **Wallet Providers:** User interfaces for asset management (Core Wallet)
- **Data Providers:** Analytics, pricing feeds, historical data services
- **Bridge Operators:** Cross-chain asset transfer infrastructure

**Participation Requirements:**
- High-availability infrastructure (full nodes, databases, redundancy)
- Technical expertise in node operation and API design

**Configurable Parameters:**
- Service level agreements (uptime, latency)
- Rate limits and access tiers
- Pricing models (freemium, subscription, usage-based)

**Economic Incentives:**
- **Inflows:** Premium subscriptions, enterprise contracts, grant funding, data licensing
- **Outflows:** Hardware, bandwidth, maintenance, and operational costs

**Risk Model:**
- Operational risk from service downtime
- Reputational exposure to reliability issues
- Competition from decentralized alternatives

---

### Ava Labs

Ava Labs is the core development organization leading Avalanche's protocol engineering and ecosystem infrastructure development.

**System Functions:**
- Develop and maintain the AvalancheGo client software
- Research and propose protocol upgrades through the ACP process
- Build ecosystem products (Core Wallet, Explorer, developer tools)
- Coordinate network upgrades with validators and ecosystem participants

**System Role:** Protocol Architect / Core Engineer

Ava Labs operates externally to the protocol's consensus and fee models—the organization does not receive transaction fees or protocol-level revenue. Its influence comes through technical leadership and ecosystem product development rather than on-chain governance power.

---

### Avalanche Foundation

The Avalanche Foundation is a non-profit organization supporting ecosystem growth, community programs, and long-term network stewardship.

**System Functions:**
- Fund development through grants and incentive programs
- Coordinate community initiatives and marketing efforts
- Manage treasury allocations (including strategic staking delegations)
- Support ecosystem events and educational resources

**System Role:** Ecosystem Steward / Grant Provider

Like Ava Labs, the Foundation operates independently of consensus and fee mechanics. Its economic influence comes through grant allocation and treasury management rather than protocol-level participation.

---

## Current Network Participation

| Metric | Value | Notes |
|--------|-------|-------|
| Primary Network Validators | ~855 | Stake 2,000+ AVAX each |
| L1 Validators | ~1,600 | Pay continuous fees |
| Unique Delegators | Not Available | Snowpeer API down |
| Total Staked | ~189M AVAX | ~41% of circulating supply |
| Delegated Stake | ~33M AVAX | ~7% of total supply |
| Active L1s | 53 | 14 modern (ACP-77), 39 legacy |
| Daily Transactions | 1M+ | Across Primary Network |

---

## Summary

Avalanche's participant ecosystem balances specialization with accessibility:

- **Network security** relies on validators staking significant capital and delegators extending that security through stake delegation, without the complexity of slashing penalties
- **Economic activity** flows from token holders and application users whose transactions generate fees that are burned, creating deflationary pressure that benefits all participants
- **Ecosystem development** depends on permissionless builder participation supported by organizational stewardship from Ava Labs and the Avalanche Foundation

The introduction of liquid staking and the ACP-77 continuous fee model have expanded participation options—lowering barriers for L1 validation while enabling stakers to maintain liquidity. These evolutions reflect Avalanche's ongoing balance between security, accessibility, and economic sustainability.

---

## References

1. Avalanche. *How to Stake*. Avalanche Builder Hub. https://build.avax.network/docs/nodes/validate/how-to-stake

2. Avalanche. *Validator FAQ*. Avalanche Support. https://support.avax.network/en/articles/6187511-validator-faq

3. Avalanche. *L1 Validator Requirements*. Avalanche Support. https://support.avax.network/en/articles/6593294-what-are-the-l1-validator-requirements

4. Avalanche. *Validator Manager Contracts*. Avalanche Builder Hub. https://build.avax.network/docs/avalanche-l1s/validator-manager/contract

5. Avalanche Foundation. *ACP-77: Reinventing Subnets*. 2024. https://github.com/avalanche-foundation/ACPs/tree/main/ACPs/77-reinventing-subnets

6. Avalanche Foundation. *ACP-62: Disable AddValidatorTx and AddDelegatorTx*. 2024. https://github.com/avalanche-foundation/ACPs/tree/main/ACPs/62-disable-addvalidatortx-and-adddelegatortx

7. Avalanche Foundation. *ACP-125: Reduce C-Chain Minimum Base Fee*. 2024. https://github.com/avalanche-foundation/ACPs/tree/main/ACPs/125-basefee-reduction

8. BenQi. *Liquid Staking Overview*. https://docs.benqi.fi/benqi-liquid-staking/overview

9. Hypha (GoGoPool). *How Liquid Staking Works*. https://docs.gogopool.com/gogopool/liquid-staking/how-liquid-staking-works

10. Avalanche. *Avalanche Validators*. https://www.avax.network/build/validators

11. Avalanche. *System Requirements*. Avalanche Builder Hub. https://build.avax.network/docs/nodes/system-requirements

12. Nansen Research. *Avalanche Q3 2025 Ecosystem Report*. 2025. https://research.nansen.ai/articles/avalanche-q3-2025-ecosystem-report
