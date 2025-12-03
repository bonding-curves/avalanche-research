---
title: Mission Elements Need Statement
---

**Last Updated:** December 3, 2025
**Draft Stage:** 1st Draft

# Mission Elements Need Statement (MENS)

## Avalanche Economic System Analysis

This document establishes the Mission Elements Need Statement (MENS) for the Avalanche Economic System research program. As a foundational systems engineering artifact, it captures the mission context, identifies stakeholders and their concerns, derives system-level needs, and establishes traceability between stakeholder interests and economic mechanisms.

For the research methodology, see [About The BCRG](/about/About-The-BCRG). For project scope, see [Project Proposal](/about/Project-Proposal). For economic foundations, see [Economic Taxonomy](/milestone1/Economic-Taxonomy) and [Mechanism Taxonomy](/milestone1/Mechanism-Taxonomy).

---

## Table of Contents

- [1. Introduction](#1-introduction)
- [2. Mission Context](#2-mission-context)
- [3. System Boundary Definition](#3-system-boundary-definition)
- [4. Stakeholder Analysis](#4-stakeholder-analysis)
- [5. Stakeholder Concerns](#5-stakeholder-concerns)
- [6. System Needs](#6-system-needs)
- [7. Mission Deficiencies](#7-mission-deficiencies)
- [8. Capability Gaps](#8-capability-gaps)
- [9. Measures of Effectiveness](#9-measures-of-effectiveness)
- [10. Constraints](#10-constraints)
- [11. Concern-to-Need Traceability](#11-concern-to-need-traceability)
- [12. Future Considerations](#12-future-considerations)

---

## 1. Introduction

### 1.1 Purpose of This Document

The Mission Elements Need Statement (MENS) serves as the foundational systems engineering document for analyzing the Avalanche Economic System. It establishes:

- **Mission clarity**: What the economic system must accomplish
- **Stakeholder identification**: Who participates in and is affected by the system
- **Need derivation**: What capabilities the system must provide
- **Deficiency analysis**: Where the system falls short of meeting needs
- **Capability gaps**: What must be developed to address deficiencies
- **Traceability**: How stakeholder concerns map to system requirements

This document bridges the gap between qualitative understanding of Avalanche economics and the formal mathematical specifications developed in subsequent milestones.

### 1.2 Document Relationships

| Document | Relationship to MENS |
|----------|---------------------|
| [Economic Taxonomy](/milestone1/Economic-Taxonomy) | Defines economic primitives that address system needs |
| [Mechanism Taxonomy](/milestone1/Mechanism-Taxonomy) | Specifies technical mechanisms implementing economic functions |
| [Participant Roles Taxonomy](/milestone1/Participant-Roles-Taxonomy) | Details stakeholder roles and documents specific concerns |
| [Systems Engineering Perspective](/milestone2/Avalanche-Economic-Model-A-Systems-Engineering-Perspective) | Applies MBSE methodology using MENS as foundation |
| [Differential Specification](/milestone3/Differential_Specification) | Formalizes dynamics that satisfy system needs |
| [Economic Hypotheses](/milestone4/economic_hypotheses) | Tests whether system meets stakeholder needs |

### 1.3 Methodology

This MENS follows Model-Based Systems Engineering (MBSE) principles as applied to blockchain economic systems. The approach:

1. **Identifies stakeholders** through analysis of on-chain participation patterns
2. **Elicits concerns** by examining economic interactions and friction points
3. **Derives needs** by abstracting concerns into capability requirements
4. **Identifies deficiencies** where current mechanisms fail to meet needs
5. **Defines capability gaps** that must be addressed
6. **Establishes traceability** through explicit mapping between concerns and needs

---

## 2. Mission Context

### 2.1 Mission Statement

The Avalanche Economic System exists to **sustain a secure, scalable, and decentralized blockchain network** by aligning the economic incentives of diverse participants toward collective network health while enabling individual value creation.

### 2.2 Mission Objectives

The Avalanche Economic System must achieve four primary objectives:

| Objective | Description | Key Mechanisms |
|-----------|-------------|----------------|
| **Security** | Maintain Byzantine fault tolerance through economic incentives | Staking rewards, uptime requirements, stake distribution |
| **Sustainability** | Balance inflation and deflation for long-term viability | Fee burning, capped supply, reward decay |
| **Value Creation** | Enable economic activity that generates utility | L1 sovereignty, fee accessibility, cross-chain messaging |
| **Stability** | Resist destabilizing perturbations and attack vectors | Dynamic fees, governance hysteresis, no slashing |

These objectives exist in tension—maximizing security through high staking may reduce liquidity for value creation; aggressive deflation may compromise sustainability. The economic system must navigate these trade-offs.

### 2.3 Current System State (November 2025)

| Metric | Value | Significance |
|--------|-------|--------------|
| Total Supply | ~460.6M AVAX | 64% of 720M maximum |
| Staking Ratio | ~41% of circulating | Security level indicator |
| Primary Network Validators | ~855 | Decentralization measure |
| L1 Validators | ~1,600 | Ecosystem growth indicator |
| Active L1s | 53 (14 modern, 39 legacy) | Application adoption |
| Daily Burn Rate | ~1,500 AVAX | Deflation pressure |
| Daily Issuance | ~49,000 AVAX | Inflation rate |
| Net Annual Inflation | ~3.76% | Sustainability trajectory |

For current data, see [Data Snapshot](/data/snapshot-2025-11-28).

---

## 3. System Boundary Definition

### 3.1 System of Interest

The **Avalanche Economic System (AES)** governs:

- AVAX scarcity through capped supply and fee burning
- Staking mechanics and reward issuance
- Transaction fee calculation and destruction
- Continuous validator fees for sovereign L1s (per ACP-77)
- Economic relationships between the Primary Network and sovereign L1s
- Governance-controlled economic parameters

### 3.2 Explicit Exclusions

The AES boundary explicitly excludes:

| Excluded Domain | Rationale |
|-----------------|-----------|
| Consensus protocols (Snowman/Avalanche) | Operational mechanism, not economic |
| Networking, messaging, and cross-chain routing | Infrastructure layer |
| Execution environments (EVM, custom VMs) | Computation layer |
| Bridge protocols (Warp, ICM, external bridges) | Infrastructure layer |
| Application-layer economics | Downstream from protocol economics |

The AES is strictly the **economic subsystem**—not a networking, consensus, execution, or bridging subsystem. Concerns related to these excluded domains are noted but classified as outside scope.

### 3.3 Meta-System Environment

The AES interacts with, but does not include:

- Global capital markets and external yield opportunities
- Cross-chain ecosystems and competing networks
- Sovereign L1 competition for users and capital
- Governance dynamics and social coordination
- Regulatory frameworks and compliance requirements

These shape stakeholder incentives but are not part of the system of interest. For detailed analysis, see [Avalanche Economy relative to the Open Economy](/milestone1/Avalanche-Economy-relative-to-the-Open-Economy).

---

## 4. Stakeholder Analysis

### 4.1 Stakeholder Categories

The Avalanche Economic System serves participants organized into functional categories:

**Security Suppliers** — Provide network security through stake commitment:
- Primary Network Validators
- Delegators

**Security Consumers** — Utilize security infrastructure for applications:
- L1 Creators
- L1 Operators
- L1 Validators

**Developers & Users** — Build and use network services:
- Primary Network developers
- L1 developers
- Application users

**Governance & Stewards** — Guide protocol evolution:
- ACP authors and reviewers
- Client maintainers
- Treasury stewards

**Market Actors** — Facilitate price discovery and liquidity:
- Traders
- Liquidity providers
- Exchanges

**Infrastructure Providers** — Operate supporting services:
- RPC providers
- Indexers and explorers

For detailed role definitions, see [Participant Roles Taxonomy](/milestone1/Participant-Roles-Taxonomy).

### 4.2 Stakeholder Influence Map

```
                    ┌─────────────────────────────────────┐
                    │     GOVERNANCE & STEWARDS           │
                    │   (ACPs, Parameter Changes)         │
                    └───────────────┬─────────────────────┘
                                    │
        ┌───────────────────────────┼───────────────────────────┐
        │                           │                           │
        ▼                           ▼                           ▼
┌───────────────┐           ┌───────────────┐           ┌───────────────┐
│   SECURITY    │           │   SECURITY    │           │  DEVELOPERS   │
│  SUPPLIERS    │◄─────────►│  CONSUMERS    │◄─────────►│   & USERS     │
│               │           │               │           │               │
│ • Validators  │           │ • L1 Creators │           │ • App Devs    │
│ • Delegators  │           │ • L1 Operators│           │ • Users       │
│               │           │ • L1 Validators│          │               │
└───────┬───────┘           └───────┬───────┘           └───────┬───────┘
        │                           │                           │
        │    ┌──────────────────────┴──────────────────────┐    │
        │    │                                             │    │
        └───►│          AVALANCHE ECONOMIC SYSTEM          │◄───┘
             │                                             │
             │  Staking ◄─► Supply ◄─► Fees ◄─► L1s       │
             │                                             │
             └──────────────────┬──────────────────────────┘
                                │
                    ┌───────────┴───────────┐
                    │                       │
            ┌───────▼───────┐       ┌───────▼───────┐
            │ MARKET ACTORS │       │ INFRASTRUCTURE│
            │               │       │   PROVIDERS   │
            │ • Traders     │       │ • RPC nodes   │
            │ • LPs         │       │ • Indexers    │
            │ • Exchanges   │       │ • Explorers   │
            └───────────────┘       └───────────────┘
```

---

## 5. Stakeholder Concerns

This section documents specific concerns raised by stakeholder analysis. Each concern represents a structural tension between stakeholder interests and current system design. Concerns are organized by stakeholder category.

### 5.1 Primary Network Validator Concerns

#### Fee Revenue Exclusion

Transaction fees are burned completely, providing validators no direct economic benefit from increased network usage. Validators earn only from issuance-based rewards, creating a disconnect between network utility growth and validator returns.

*Related Needs:* Proportional Economic Contribution, Cross-Layer Incentive Coherence, Macro-Level Demand Responsiveness

#### Inflation-Dependent Yield

Real validator yield depends on net inflation rather than productive economic activity. As supply approaches the 720M cap and issuance declines, validator economics become uncertain without alternative revenue sources.

*Related Needs:* Explicit Sustainability Boundaries, Macro-Level Demand Responsiveness

#### L1 Revenue Isolation

Primary Network validators secure the infrastructure that all L1s depend upon (P-Chain state, AWM registry) but receive no participation in L1-generated economic value beyond the minimal continuous fees that are burned.

*Related Needs:* Proportional Economic Contribution, Cross-Layer Incentive Coherence

#### Negligible L1 Fee Contribution

The continuous L1 validator fee (~1.33 AVAX/month per ACP-77) is economically negligible relative to the security infrastructure L1 validators depend on. These fees are burned rather than distributed to Primary Network validators.

*Related Needs:* Proportional Economic Contribution, Predictable Cost Structures

#### Burned L1 Fees

Continuous L1 fees are burned rather than redistributed to Primary Network validators who secure the infrastructure L1s rely upon.

*Related Needs:* Proportional Economic Contribution, Cross-Layer Incentive Coherence

### 5.2 Delegator Concerns

#### Dilution-Based Returns

Delegator returns are driven by token dilution (inflation) rather than productive network usage. Delegators benefit from issuance but not from fee-generating economic activity that increases network value.

*Related Needs:* Proportional Economic Contribution, Cross-Layer Incentive Coherence, Explicit Sustainability Boundaries

### 5.3 L1 Creator and Operator Concerns

#### Fee Volatility at Validator Saturation

When L1 validator count approaches the 10,000 target capacity, fees increase exponentially per ACP-77. This creates unpredictable cost structures for L1 operators planning validator expansion.

*Related Needs:* Predictable Cost Structures, Adaptive Economic Behavior, Macro-Level Demand Responsiveness

#### Sovereignty Creates Liquidity Isolation

L1s with native tokens may face liquidity challenges—shallow markets complicate validator economics and user onboarding when bridging costs exceed transaction value.

*Related Needs:* Scalable Multi-Chain Economic Coherence, Interoperability & Liquidity Connectivity

#### No Incentive to Contribute to Primary Network

L1s have no structural incentive to contribute economically to the Primary Network beyond the minimal continuous fee. Success of L1 ecosystems may not proportionally benefit Primary Network security.

*Related Needs:* Proportional Economic Contribution, Cross-Layer Incentive Coherence

### 5.4 Developer Concerns

#### Macro-Economy Does Not React to Demand

Network economic parameters (issuance, fees) remain static regardless of developer activity or application success. Economic conditions don't adapt to ecosystem growth signals.

*Related Needs:* Adaptive Economic Behavior, Macro-Level Demand Responsiveness

#### EVM Upgrade Lag

*Classification:* Outside AES scope (execution layer concern)

### 5.5 User Concerns

#### Fragmented Multi-Chain Experience

Sovereign L1s create fragmented user experiences—each L1 may have different tokens, wallets, bridges, and interaction patterns, increasing friction and complexity.

*Related Needs:* Scalable Multi-Chain Economic Coherence

### 5.6 Token Holder Concerns

#### Undefined Sustainability Equilibrium

The relationship between issuance, burn rate, and long-term token economics lacks defined equilibrium targets. Holders cannot assess whether current parameters lead to sustainable value accrual.

*Related Needs:* Explicit Sustainability Boundaries

#### Security Budget Tied to Issuance

Network security depends on inflation subsidies rather than fee-based revenue. As issuance declines toward the supply cap, security funding becomes uncertain.

*Related Needs:* Explicit Sustainability Boundaries, Macro-Level Demand Responsiveness

### 5.7 Governance Concerns

#### Slow Parameter Adaptation

Economic parameters change only through governance cycles that span weeks to months. The ACP process, while thorough, cannot respond quickly to market conditions or emerging opportunities.

*Related Needs:* Adaptive Economic Behavior

#### Absence of Real-Time Economic Levers

Macro-economic adjustments require code changes, governance approval, and coordinated network upgrades. No mechanisms exist for continuous, market-driven economic adjustment.

*Related Needs:* Adaptive Economic Behavior, Macro-Level Demand Responsiveness

### 5.8 Market Actor Concerns

#### Cross-Chain Liquidity Fragmentation

Capital is dispersed across multiple sovereign L1s rather than concentrated, reducing market depth and capital efficiency across the ecosystem.

*Related Needs:* Scalable Multi-Chain Economic Coherence, Interoperability & Liquidity Connectivity

#### Bridge Trust Heterogeneity

Cross-chain liquidity depends on bridges with varying security models, introducing counterparty and technical risks that complicate liquidity provision strategies.

*Related Needs:* Interoperability & Liquidity Connectivity

### 5.9 Infrastructure Provider Concerns

#### P-Chain Scalability Constraints

Infrastructure providers relying on P-Chain data face constraints from consensus and serialization limits. This concern relates to consensus/networking rather than economic mechanisms.

*Classification:* Outside AES scope (consensus/networking concern)

---

## 6. System Needs

System needs are derived by abstracting stakeholder concerns into capability requirements. Each need represents what the Avalanche Economic System should provide to address one or more concerns.

### 6.1 Proportional Economic Contribution

**Statement:** The economic system should support proportional economic relationships across Primary Network and L1 activity, ensuring those who contribute to network value creation capture proportional benefits.

**Rationale:** Current fee burning creates a disconnect between network usage and validator/delegator returns. Active security providers have no direct claim on usage-generated value.

**Derived From Concerns:**
- Fee revenue exclusion (validators receive no usage upside)
- L1 revenue isolation (validators don't participate in L1 success)
- Negligible L1 fee contribution (fees too small to matter economically)
- Burned L1 fees (fees destroyed rather than redistributed)
- Dilution-based returns (rewards from inflation, not productivity)
- No incentive to contribute to Primary Network (L1s don't feed back)

**Satisfaction Criteria:**
- Participants who increase network utility should receive commensurate economic benefit
- Security providers should have exposure to network growth beyond inflationary rewards
- Value capture should scale with contribution, not merely with capital deployed

---

### 6.2 Predictable Cost Structures

**Statement:** The economic system should provide participants with predictable and transparent cost structures that enable long-term planning and investment decisions.

**Rationale:** Exponential fee scaling at capacity thresholds creates cost uncertainty for L1 operators. Unpredictable costs discourage investment and complicate business modeling.

**Derived From Concerns:**
- Negligible L1 fee contribution (small now, uncertain future)
- Fee volatility at validator saturation (exponential scaling at capacity)

**Satisfaction Criteria:**
- Fee mechanisms should have clearly communicated scaling behaviors
- Cost trajectories should be modelable under various growth scenarios
- Transition zones should have gradual rather than sharp cost increases

---

### 6.3 Cross-Layer Incentive Coherence

**Statement:** The economic system should ensure incentives are aligned across protocol layers (Primary Network, L1s, applications) such that success at any layer contributes to overall network health.

**Rationale:** Primary Network validators secure infrastructure that L1s depend upon but capture no value from L1 success. L1s have no structural incentive to contribute to Primary Network beyond minimal fees.

**Derived From Concerns:**
- Fee revenue exclusion (validators disconnected from usage growth)
- L1 revenue isolation (validators excluded from L1 economics)
- Burned L1 fees (potential redistribution not occurring)
- Dilution-based returns (rewards don't reflect layer contribution)
- No incentive to contribute to Primary Network (structural misalignment)

**Satisfaction Criteria:**
- L1 economic success should create positive externalities for Primary Network security
- Primary Network security providers should have exposure to L1 ecosystem growth
- Application layer activity should translate into infrastructure layer sustainability

---

### 6.4 Explicit Sustainability Boundaries

**Statement:** The economic system should define and communicate clear boundaries for sustainable operation, including target equilibria for key metrics and transition paths between economic regimes.

**Rationale:** Stakeholders cannot assess whether current parameters lead to sustainable outcomes. The relationship between issuance, burn rate, staking ratio, and long-term economics lacks defined targets.

**Derived From Concerns:**
- Inflation-dependent yield (uncertainty as issuance declines)
- Dilution-based returns (sustainability of reward model)
- Undefined sustainability equilibrium (no clear targets)
- Security budget tied to issuance (post-cap uncertainty)

**Satisfaction Criteria:**
- Target ranges should be defined for key sustainability metrics (staking ratio, burn/issuance ratio)
- Transition dynamics should be characterized (path from inflationary to deflationary regime)
- Economic health indicators should have clear interpretation guidelines

---

### 6.5 Adaptive Economic Behavior

**Statement:** The economic system should incorporate mechanisms that automatically adapt to changing conditions without requiring governance intervention for routine adjustments.

**Rationale:** Current parameter changes require ACP governance cycles spanning weeks to months. The network cannot respond quickly to market conditions, demand shocks, or emerging opportunities.

**Derived From Concerns:**
- Fee volatility at validator saturation (need adaptive response)
- Macro-economy does not react to demand (static parameters)
- Slow parameter adaptation (governance bottleneck)
- Absence of real-time economic levers (no automatic adjustment)

**Satisfaction Criteria:**
- Routine economic adjustments should occur algorithmically
- Market signals should inform parameter adaptation in real-time
- Governance should focus on structural changes, not operational tuning

---

### 6.6 Scalable Multi-Chain Economic Coherence

**Statement:** The economic system should maintain coherent economic relationships across an expanding number of L1 blockchains while preserving L1 sovereignty.

**Rationale:** User experience fragments across sovereign L1s with different tokens, interfaces, and interaction patterns. Liquidity disperses rather than concentrates. The ecosystem becomes harder to navigate as it grows.

**Derived From Concerns:**
- Sovereignty creates liquidity isolation (fragmented capital)
- Fragmented multi-chain experience (user friction)
- Cross-chain liquidity fragmentation (dispersed markets)

**Satisfaction Criteria:**
- Cross-L1 interactions should have consistent economic semantics
- Users should be able to operate across L1s without prohibitive friction
- L1 sovereignty should be preserved while enabling economic interoperability

---

### 6.7 Interoperability & Liquidity Connectivity

**Statement:** The economic system should enable efficient liquidity flow between chains and minimize trust assumptions in cross-chain value transfer.

**Rationale:** Cross-chain liquidity depends on bridges with varying security models. Capital fragmentation reduces market depth. Bridge trust heterogeneity introduces counterparty risk.

**Derived From Concerns:**
- Sovereignty creates liquidity isolation (capital locked in L1s)
- Cross-chain liquidity fragmentation (dispersed pools)
- Bridge trust heterogeneity (variable security models)

**Satisfaction Criteria:**
- Native cross-chain mechanisms should minimize trust assumptions
- Liquidity should flow efficiently across ecosystem boundaries
- Bridge security should be verifiable and standardized

---

### 6.8 Macro-Level Demand Responsiveness

**Statement:** The economic system should respond to aggregate demand signals at the network level, adjusting economic parameters to maintain target operating conditions.

**Rationale:** Network economic parameters remain static regardless of demand conditions. The system cannot distinguish between growth phases requiring different economic policies. Security budget depends on issuance rather than demand-driven revenue.

**Derived From Concerns:**
- Fee revenue exclusion (no connection to demand growth)
- Inflation-dependent yield (disconnected from usage)
- Fee volatility at validator saturation (need demand-aware adjustment)
- Macro-economy does not react to demand (static system)
- Security budget tied to issuance (not demand-responsive)
- Absence of real-time economic levers (no demand signal processing)

**Satisfaction Criteria:**
- Economic parameters should adapt to demand regime changes
- Security funding should have sustainable sources beyond issuance
- Growth phases should be supported by appropriate economic conditions

---

## 7. Mission Deficiencies

Mission deficiencies represent gaps between what the system needs to accomplish and what it currently achieves. They are derived from analyzing which needs are inadequately met by current mechanisms.

### 7.1 Structural Cross-Layer Economic Decoupling

**Definition:** The AES fails to couple sovereign L1 economic activity with Primary Network sustainability. L1 success does not proportionally contribute to the security infrastructure L1s depend upon.

**Evidence:**
- L1 continuous fees (~1.33 AVAX/month) are economically negligible
- All fees are burned, providing no direct validator benefit
- L1s have no structural incentive to contribute beyond minimum fees
- Primary Network validators excluded from L1 economic growth

**Derived From Needs:**
- Proportional Economic Contribution
- Cross-Layer Incentive Coherence
- Scalable Multi-Chain Economic Coherence
- Interoperability & Liquidity Connectivity

**Impact:** As L1 ecosystem grows, the economic disconnect between L1 success and Primary Network security may create sustainability challenges. Security providers lack participation in the value they enable.

---

### 7.2 Non-Adaptive Macro-Economic Behavior

**Definition:** The AES cannot adjust macro-economic variables in response to system conditions without governance intervention. Economic parameters remain static regardless of demand, usage patterns, or market conditions.

**Evidence:**
- Fee parameters require ACP governance to modify
- No automatic response to demand shocks
- Security budget tied to fixed issuance schedule
- Gap between governance pace and market dynamics

**Derived From Needs:**
- Predictable Cost Structures
- Explicit Sustainability Boundaries
- Adaptive Economic Behavior
- Macro-Level Demand Responsiveness

**Impact:** The system cannot optimize economic conditions in response to changing circumstances. Governance cycles are too slow for operational adjustments, leaving the system unable to self-regulate effectively.

---

## 8. Capability Gaps

Capability gaps identify what must be developed or enhanced to address mission deficiencies.

### 8.1 Cross-Layer Economic Coupling Capability

**Definition:** The capability for the AES to establish proportional, predictable economic relationships between L1 activity and Primary Network sustainability.

**Required Capabilities:**
- Mechanisms to channel L1 economic value to Primary Network security
- Transparent and predictable cross-layer fee structures
- Incentive alignment between L1 success and PN validator returns

**Addresses Deficiency:** Structural Cross-Layer Economic Decoupling

**Potential Approaches:**
- Fee sharing models that redirect portion of L1 fees to validators
- L1 success-linked rewards for Primary Network validators
- Cross-chain value capture mechanisms

---

### 8.2 Adaptive Macro-Economic Regulation Capability

**Definition:** The capability for the AES to autonomously adjust macro-economic behavior in response to internal and external conditions without requiring governance intervention for routine adjustments.

**Required Capabilities:**
- Real-time economic parameter adjustment mechanisms
- Demand-responsive fee and reward structures
- Autonomous stabilization within governance-defined bounds

**Addresses Deficiency:** Non-Adaptive Macro-Economic Behavior

**Potential Approaches:**
- Algorithmic parameter adjustment (building on ACP-176 model)
- Demand-indexed economic variables
- Automated stabilization mechanisms with governance oversight

---

## 9. Measures of Effectiveness

Measures of effectiveness (MoE) provide quantifiable criteria for evaluating whether capability gaps have been successfully addressed.

### 9.1 Cross-Layer Value Contribution Index

**Evaluates:** Cross-Layer Economic Coupling Capability

**Definition:** A quantitative measure of the relationship between L1 economic activity and Primary Network sustainability metrics.

**Components:**
- Ratio of L1-derived revenue to Primary Network security budget
- Correlation between L1 growth and validator profitability
- Economic value flow from L1s to Primary Network

**Target:** Positive correlation between L1 ecosystem growth and Primary Network validator economics.

---

### 9.2 Macro-Economic Responsiveness Time

**Evaluates:** Adaptive Macro-Economic Regulation Capability

**Definition:** The time required for macro-economic variables to adjust after significant demand shifts.

**Components:**
- Latency between demand signal and parameter response
- Magnitude of achievable adjustment per time period
- Coverage of automatically-adjustable parameters

**Target:** Sub-day responsiveness for operational parameters within governance-defined bounds.

---

## 10. Constraints

Constraints define boundaries within which solutions to capability gaps must operate.

### 10.1 External Constraints

| Constraint | Description | Impact |
|------------|-------------|--------|
| External Markets | Global capital markets set alternative yield expectations | Limits on how low staking APR can go |
| Regulatory Frameworks | Compliance requirements vary by jurisdiction | May restrict certain economic mechanisms |
| Sovereign L1 Autonomy | L1s control their own economic parameters | Cannot mandate L1 contribution |

### 10.2 Stakeholder-Imposed Constraints

| Constraint | Description | Impact |
|------------|-------------|--------|
| AVAX Scarcity Preference | Long-term holders prefer deflationary dynamics | Limits fee redistribution options |
| Burn Model Preference | Community values 100% fee burn | Constraints on fee allocation |
| Governance Hysteresis | Preference for gradual parameter changes | Limits adaptation speed |

### 10.3 Operational Constraints

| Constraint | Description | Impact |
|------------|-------------|--------|
| Consensus Throughput | P-Chain serialization limits (outside AES) | Affects L1 validator capacity |
| Observability Limits | Not all L1 economic data is accessible | Limits demand signal precision |
| Upgrade Cycles | Node operators need time to deploy changes | Minimum time between parameter changes |

---

## 11. Concern-to-Need Traceability

### 11.1 Traceability Matrix

| Stakeholder Concern | Primary Need | Secondary Needs |
|---------------------|--------------|-----------------|
| Fee revenue exclusion | Proportional Economic Contribution | Cross-Layer Coherence, Demand Responsiveness |
| Inflation-dependent yield | Explicit Sustainability Boundaries | Demand Responsiveness |
| L1 revenue isolation | Proportional Economic Contribution | Cross-Layer Coherence |
| Negligible L1 fee contribution | Proportional Economic Contribution | Predictable Cost Structures |
| Burned L1 fees | Proportional Economic Contribution | Cross-Layer Coherence |
| Dilution-based returns | Proportional Economic Contribution | Cross-Layer Coherence, Sustainability Boundaries |
| Fee volatility at saturation | Predictable Cost Structures | Adaptive Behavior, Demand Responsiveness |
| Sovereignty creates liquidity isolation | Multi-Chain Coherence | Interoperability |
| No incentive to contribute to PN | Proportional Economic Contribution | Cross-Layer Coherence |
| Macro-economy static to demand | Adaptive Economic Behavior | Demand Responsiveness |
| Fragmented multi-chain experience | Multi-Chain Coherence | Interoperability |
| Undefined sustainability equilibrium | Explicit Sustainability Boundaries | — |
| Security budget tied to issuance | Explicit Sustainability Boundaries | Demand Responsiveness |
| Slow parameter adaptation | Adaptive Economic Behavior | — |
| No real-time economic levers | Adaptive Economic Behavior | Demand Responsiveness |
| Cross-chain liquidity fragmentation | Multi-Chain Coherence | Interoperability |
| Bridge trust heterogeneity | Interoperability | Multi-Chain Coherence |

### 11.2 Need Coverage Summary

| Need | Concerns Addressed | Priority Assessment |
|------|-------------------|---------------------|
| Proportional Economic Contribution | 6 | High — core economic alignment |
| Predictable Cost Structures | 2 | Medium — L1 operator specific |
| Cross-Layer Incentive Coherence | 5 | High — ecosystem scaling |
| Explicit Sustainability Boundaries | 4 | High — long-term viability |
| Adaptive Economic Behavior | 4 | Medium — operational efficiency |
| Multi-Chain Economic Coherence | 3 | High — ecosystem growth |
| Interoperability & Liquidity | 3 | High — capital efficiency |
| Macro-Level Demand Responsiveness | 6 | Highest — systemic adaptation |

---

## 12. Future Considerations

### 12.1 Emerging Concerns

As the Avalanche ecosystem evolves, new stakeholder concerns may emerge:

**Liquid Staking Concentration**
Large LST protocols may accumulate significant consensus influence through recursive leverage, potentially centralizing security in ways not captured by traditional stake distribution metrics.

**L1 Migration Dynamics**
The transition from legacy subnets to modern L1s under ACP-77 creates temporary economic asymmetries between validator classes.

**Post-Issuance Economics**
As total supply approaches the 720M cap over the coming decades, the transition to a fee-only security budget requires planning and may necessitate mechanism redesign.

### 12.2 Research Directions

This MENS establishes the foundation for ongoing research:

| Direction | Related Needs | Approach |
|-----------|---------------|----------|
| Fee Revenue Models | Proportional contribution, cross-layer coherence | Model alternative fee distribution mechanisms |
| Sustainability Modeling | Explicit boundaries, demand responsiveness | Quantify equilibrium conditions and transition paths |
| Adaptive Mechanism Design | Adaptive behavior, demand responsiveness | Design market-driven parameter adjustment mechanisms |
| Cross-Chain Economics | Multi-chain coherence, interoperability | Analyze AWM/ICM economic implications |

### 12.3 Document Evolution

This MENS is a living document that should be updated as:

- New stakeholder concerns are identified through network operation
- System needs evolve with ecosystem growth
- Protocol changes (ACPs) modify economic mechanisms
- Research findings refine understanding of system dynamics

---

## References

1. Avalanche Foundation. *Avalanche Community Proposals (ACPs)*. GitHub Repository. https://github.com/avalanche-foundation/ACPs

2. Ava Labs. *Avalanche Platform Whitepaper*. 2020. https://www.avalabs.org/whitepapers

3. Shevchenko, N. (2020). *Introduction to Model Based Systems Engineering*. Software Engineering Institute, Carnegie Mellon University.

4. INCOSE. *Systems Engineering Handbook*. 4th Edition. 2015.

5. Zargham, M., & Ben-Meir, I. (2023). *Block by Block: Managing Complexity with Model-Based Systems Engineering*. BlockScience Blog.

6. ISO/IEC/IEEE 29148:2018. *Systems and Software Engineering — Life Cycle Processes — Requirements Engineering*.
