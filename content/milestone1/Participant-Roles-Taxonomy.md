**Last Update:** November 22nd, 2025  **Draft Stage:** 4th Draft


# Avalanche Economic System: Participant Specification

**Last Update:** November 7, 2025
**Version:** 2.0 

***

## 1.0 Overview

This document defines the taxonomy of participant roles within the Avalanche network. Each role is specified as a system component with defined functions, requirements, interfaces, and economic models. These roles are not mutually exclusive; a single entity may fulfill multiple roles.

***

## 2.0 Network Security Participants

This category includes roles directly responsible for network consensus and security.

### 2.1 Primary Network Validator (PNV)

**Definition:**  
A PNV is a full node that participates in the consensus of the Avalanche Primary Network (X-Chain, P-Chain, and C-Chain) by staking AVAX.

**System Functions:**
- Validate and produce blocks on the Primary Network.  
- Participate in consensus by repeatedly sampling other validators.  
- Maintain the state of all three Primary Network chains.  
- (Optional) Validate L1s.

**Participation Requirements:**
- **Stake:** 2,000 AVAX minimum.  
- **Uptime:** Must maintain greater than 80% uptime, as measured by peers, to receive rewards.  
- **Hardware:** Minimum specs (8 vCPU, 16GB RAM, 1TB SSD).  
- **BLS Key:** Must register a BLS key (per ACP-62).

**Configurable Parameters:**
- Staking Duration: 2 weeks (min) to 1 year (max).  
- Delegation Fee: 2% (min).

**Economic Incentives (Value Flow):**
- **Inflows:** Receives staking rewards from network issuance.  
- **Outflows:** Hardware, bandwidth, and operational costs. (Note: All transaction fees are burned.)

**Risk & Penalty Model:**
- No Slashing: No loss of principal stake.  
- Reward Forfeiture: Rewards are forfeited if uptime drops below 80% during the staking period.

***

### 2.2 L1 Validator (L1V)

**Definition:**  
An L1V participates in the consensus of a specific L1 (formerly Subnet), independent of the Primary Network.

**System Functions:**
- Validate and produce blocks for a specific L1.  
- Maintain the state of that L1.  
- (Optional) Send and sign Avalanche Warp Messages (AWM) for cross-chain communication.

**Participation Requirements:**
- Defined by L1 governance or Validator Manager contract (e.g., stake a native L1 token, hold an NFT, pass KYC).  
- **P-Chain Fee:** Continuous, dynamic AVAX fee (per ACP-77) to remain an active validator.  
- **Hardware:** As required by the specific L1.

**Configurable Parameters:**  
Defined by the L1’s implementation.

**Economic Incentives (Value Flow):**
- **Inflows:** L1-token rewards or share of L1 fees.  
- **Outflows:** Hardware and operation costs; continuous AVAX fee paid to P-Chain (burned).

**Risk & Penalty Model:**  
Defined by the L1’s Validator Manager contract. May include slashing of the L1’s native token or other penalties.

***

### 2.3 Delegator

**Definition:**  
A passive participant who delegates AVAX to a Primary Network Validator to contribute to network security and earn rewards.

**System Functions:**
- Select a PNV to delegate stake to.  
- Lock AVAX for the staking duration.  
- Claim rewards upon completion.

**Participation Requirements:**
- **Stake:** 25 AVAX minimum.

**Configurable Parameters:**
- Validator Choice: Selected PNV.  
- Staking Duration: 2 weeks (min) to 1 year (max).

**Economic Incentives (Value Flow):**
- **Inflows:** Receives staking rewards (minus validator’s delegation fee).  
- **Outflows:** Pays validator’s delegation fee (percentage of reward).

**Risk & Penalty Model:**
- No Slashing: Principal stake is not reduced.  
- Reward Forfeiture: Rewards forfeited if chosen PNV fails to maintain required uptime.

***

## 3.0 Economic & Utility Participants

This category covers roles that generate demand, utility, and liquidity within the Avalanche economy.

### 3.1 Token Holder (AVAX)

**Definition:**  
A base-level participant holding the network’s native asset, AVAX.

**System Functions:**
- Hold and transfer AVAX.  
- Pay system fees across the P-Chain, X-Chain, and C-Chain.  
- Supply capital through staking or delegation.  
- Participate in governance.

**Participation Requirements:**  
Control of a private key (wallet).

**Configurable Parameters:**  
N/A

**Economic Incentives (Value Flow):**
- **Inflows:** Token acquisition, staking rewards, DeFi yields.  
- **Outflows:** All transaction fees are burned.

**Risk & Penalty Model:**  
Exposure to market volatility and custody risk.

***

### 3.2 Application User

**Definition:**  
An actor who interacts with decentralized applications or smart contracts on the C-Chain or any L1.

**System Functions:**
- Execute smart contract calls (e.g., trade, mint NFTs, borrow assets).  
- Trigger state changes on EVM-compatible chains.

**Participation Requirements:**  
A wallet capable of sending signed transactions.

**Configurable Parameters:**  
Gas price (priority fee) selection for faster transaction inclusion.

**Economic Incentives (Value Flow):**
- **Inflows:** App-specific utility or value (digital assets, yields, services).  
- **Outflows:** Transaction fees burned; dApp-specific protocol fees.

**Risk & Penalty Model:**  
Smart contract vulnerability and asset-specific market risks.

***

### 3.3 Trader / Investor / Liquidity Provider

**Definition:**  
A participant focused on capital allocation, liquidity provision, and market efficiency.

**System Functions:**
- Provide liquidity to DEXs or lending protocols.  
- Execute trades and arbitrage opportunities.  
- Invest in ecosystem assets and derivatives.

**Participation Requirements:**  
Control of capital (tokens).

**Configurable Parameters:**  
Capital allocation and trading strategy.

**Economic Incentives (Value Flow):**
- **Inflows:** Trading profits, LP fees, yield farming rewards.  
- **Outflows:** Fees burned; potential impermanent loss; capital-at-risk.

**Risk & Penalty Model:**  
Exposure to market, liquidity, and smart contract risks.

***

## 4.0 Ecosystem Participants

This category defines organizational and technical roles supporting network infrastructure, development, and governance.

### 4.1 Developer

**Definition:**  
An individual or team building applications, tools, or new L1s on Avalanche.

**System Functions:**
- Deploy smart contracts on C-Chain or L1s.  
- Define and deploy new L1s and Validator Manager contracts.  
- Develop wallets and application interfaces.  
- Contribute to protocol development (ACPs).

**Participation Requirements:**  
None (permissionless development).

**Configurable Parameters:**  
L1 configuration parameters and smart contract logic.

**Economic Incentives (Value Flow):**
- **Inflows:** Application revenue, L1 token value, or grants.  
- **Outflows:** Development, audit, deployment, and transaction costs.

**Risk & Penalty Model:**  
Business risk and project execution uncertainty.

***

### 4.2 Infrastructure Provider

**Definition:**  
An entity providing data, compute, or network access infrastructure for Avalanche users and developers.

**System Functions:**
- Operate public/private RPC nodes.  
- Run indexers (block explorers).  
- Provide API or SDK access.  
- Include wallet providers such as Core.

**Participation Requirements:**  
Maintain high-availability infrastructure (full nodes, databases).

**Configurable Parameters:**  
Service-level agreements and API rate limits.

**Economic Incentives (Value Flow):**
- **Inflows:** Premium subscriptions, grants, or data service revenue.  
- **Outflows:** Hardware, bandwidth, and maintenance costs.

**Risk & Penalty Model:**  
Operational and reputational exposure to service downtime.

***

### 4.3 Ava Labs

**Definition:**  
Core development organization leading the engineering of Avalanche’s protocol and ecosystem infrastructure.

**System Functions:**
- Develop the AvalancheGo client.  
- Research and propose new protocol upgrades (ACPs).  
- Build ecosystem products such as Core Wallet.

**System Role:**  
Protocol Architect / Core Engineer.  

*Note: Ava Labs operates externally to the protocol’s consensus and fee models.*

***

### 4.4 Avalanche Foundation

**Definition:**  
A non-profit organization supporting Avalanche ecosystem growth and stewardship.

**System Functions:**
- Fund development through grants.  
- Coordinate community programs and marketing.  
- Manage treasury allocations (including staking delegations).

**System Role:**  
Ecosystem Steward / Grant Provider.  

*Note: Operations are independent of consensus and fee mechanics.*

***

## References

1. [Avalanche How to Stake](https://build.avax.network/docs/nodes/validate/how-to-stake)  
2. [Bloq Avalanche Staking](https://stake.bloq.com/protocols/avalanche/)  
3. [Why Does AVAX Have No Slashing Penalty? - Reddit](https://www.reddit.com/r/Avax/comments/scrcdd/why_does_avax_have_no_slashing_penalty_for/)  
4. [Avalanche Validators](https://www.avax.network/build/validators)  
5. [Coinbase Avalanche Staking FAQ](https://docs.cdp.coinbase.com/staking/staking-delegation-guides/avalanche/avalanche-faq)  
6. [Figment Avalanche Staking](https://figment.io/staking/protocols/avalanche/)  
7. [Bank Frick Avalanche Overview](https://www.bankfrick.li/en/avalanche-avax)  
8. [Kiln Avalanche Protocol](https://www.kiln.fi/protocols/avalanche)  

Additional resources:  
- [Avalanche Delegation Guide](https://avaunt-staking.com/avalanche-delegation-guide/)  
- [How to Run Avalanche Node](https://leasepacket.com/how-to-run-avalanche-node/)  
- [Avalanche System Requirements](https://build.avax.network/docs/nodes/system-requirements)  
- [GetBlock Avalanche Node Guide](https://getblock.io/blog/how-to-run-avax-node-requirements/)  
- [ACP Discussions - GitHub](https://github.com/avalanche-foundation/ACPs/discussions/78)  
- [Breaking Down ACP-77](https://chorus.one/articles/breaking-down-acp-77-reinventing-subnets-on-avalanche)  
- [ETNA Blog on Avalanche L1s](https://www.avax.network/about/blog/etna-enhancing-the-sovereignty-of-avalanche-l1-networks)  
- [ACP-77 Institutional Adoption](https://www.zeeve.io/blog/avalanches-acp-77-skyrocketing-subnet-growth-institutional-buy-in/)  
- [GoGoPool Liquid Staking](https://docs.gogopool.com/gogopool/liquid-staking/how-liquid-staking-works)  
- [Core Wallet for Avalanche L1s](https://core.app/discover/projects/avalanchel1s)  
- [Balancer Deploys On Avalanche](https://www.avax.network/about/press/balancer-deploys-on-avalanche/)  
- [Ultimate Guide to Avalanche Development](https://www.rapidinnovation.io/post/ultimate-guide-to-avalanche-ecosystem-development-and-implementation)  
- [AWS on Avalanche](https://aws.amazon.com/startups/learn/building-application-specific-blockchains-with-aws-on-avalanche)  
- [Avalanche Foundation](https://www.avax.network/about/foundation)  
- [Avalanche Delegation Guide - Coinbase](https://docs.cdp.coinbase.com/staking/staking-delegation-guides/avalanche/delegation-guide/avalanche-delegation-guide)

***

