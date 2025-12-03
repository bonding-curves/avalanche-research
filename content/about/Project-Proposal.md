---
title: Project Proposal
---

# Avalanche Economic Research Project

## Project Overview

This research project provides a comprehensive economic analysis of the Avalanche blockchain ecosystem, progressing from foundational taxonomies through systems engineering to mathematical specifications. Our goal is to understand how Avalanche can achieve security, sustainability, value creation, and stability through optimal economic design.

**Current Network State (November 2025):** ~460.6M AVAX total supply (64% of 720M cap), ~189M AVAX staked (~41% of circulating), ~855 Primary Network validators + ~1,600 L1 validators. See [Data Snapshot](/data/snapshot-2025-11-28) for current metrics.

---

## Milestone 1: Economic Foundations

### [Participant Roles Taxonomy](/milestone1/Participant-Roles-Taxonomy)

The Avalanche network comprises diverse participants, each with unique roles and incentives. This taxonomy identifies eleven primary participant roles across three categories—network participants, development organizations, and community members. Understanding these roles is crucial as participants often occupy multiple positions simultaneously, creating complex incentive structures.

### [Economic Taxonomy](/milestone1/Economic-Taxonomy)

Avalanche's economic mechanisms form an interconnected web of incentives and constraints. This taxonomy classifies the core economic components including staking rewards, fee structures, token supply dynamics, and governance mechanisms. The unique aspects of Avalanche's economy—such as the 100% fee burn mechanism and duration-based staking rewards—create distinctive economic equilibria.

### [Mechanism Taxonomy](/milestone1/Mechanism-Taxonomy)

Protocol mechanisms are the operational rules that govern network behavior. This taxonomy analyzes Snow consensus, validation processes, delegation systems, and cross-chain communications via Avalanche Warp Messaging. Avalanche's novel consensus protocol and multi-chain architecture create unique mechanism designs, particularly in how the Primary Network secures application-specific L1 blockchains.

### [Avalanche Economy vs Open Economy](/milestone1/Avalanche-Economy-relative-to-the-Open-Economy)

Avalanche doesn't exist in isolation—it interfaces with traditional financial systems and other blockchain networks. This analysis positions Avalanche within the broader economic context, examining how external market forces, regulatory environments, and cross-chain interactions affect the network. We explore concepts like the Taylor Rule adapted for crypto-economics.

---

## Milestone 2: Systems Engineering Perspective

### [Systems Engineering Framework](/milestone2/Avalanche-Economic-Model-A-Systems-Engineering-Perspective)

Model-Based Systems Engineering (MBSE) provides a rigorous methodology for analyzing complex systems like Avalanche. This report applies MBSE principles to decompose the network into five core subsystems—Staking Dynamics, Token Supply, Fee Dynamics, L1 Ecosystem, and Governance—and analyze how changes in one subsystem propagate through others. This systems approach reveals feedback loops and emergent behaviors not visible when examining components in isolation.

### [Subsystem Analysis and Multigraph Model](/milestone2/Subsystem_Analysis_and_MultiGraph)

Building on the MBSE framework, this detailed analysis specifies each subsystem with state variables, flow dynamics, parameters, and interaction points. The multigraph model captures how agents engage with multiple subsystems simultaneously, revealing complex strategic behaviors and system-wide patterns.

### [ACP Summaries](/milestone2/ACP-Summaries)

Avalanche Community Proposals (ACPs) represent the evolution of the protocol through governance. This analysis examines key ACPs across four major upgrades:

| Upgrade | Date | Key ACPs | Impact |
|---------|------|----------|--------|
| Durango | March 2024 | 23, 24, 30, 31 | AWM on C-Chain |
| Etna | December 2024 | 77, 103, 125 | L1 restructuring, dynamic fees |
| Octane | April 2025 | 176 | Dynamic gas limits |
| Granite | November 2025 | 181, 204, 226 | Cross-chain reliability |

---

## Milestone 3: Mathematical Specifications

### [Differential Specification](/milestone3/Differential_Specification)

The differential specification provides a complete mathematical framework for modeling Avalanche's economic dynamics. Using control theory and differential equations, we formalize how the system evolves over time through:

- **State variables** for staking, token supply, fees, L1 ecosystem, and governance
- **Control parameters** for inflation rates, fee constants, and stake requirements
- **Conservation laws** ensuring system consistency
- **Behavioral functions** modeling participant responses

This mathematical foundation enables rigorous stability analysis, parameter optimization, and predictive modeling.

---

## Milestone 4: Economic Hypotheses and Framework

### [Economic Hypotheses](/milestone4/economic_hypotheses)

Translating mathematical models into actionable insights, this deliverable presents evidence-based hypotheses about optimal system configurations:

- **Staking equilibrium**: 50-60% ratio balances security with liquidity
- **Fee dynamics**: Exponential adjustment provides stability under demand shocks
- **L1 sustainability**: Continuous fee model (ACP-77) creates sustainable economics
- **Supply trajectory**: Burn rate increases (3× in 2025) indicate improving tokenomics

---

## Key Achievements

Through this systematic analysis, we've established:

| Achievement | Description |
|-------------|-------------|
| **Comprehensive Understanding** | Complete mapping of economic landscape from participant roles to mathematical dynamics |
| **Systems Perspective** | Identification of feedback loops, emergent behaviors, and cross-subsystem dependencies |
| **Mathematical Rigor** | Formal specifications enabling predictive modeling and stability analysis |
| **Practical Applications** | Actionable insights for governance decisions and protocol optimization |

## Impact and Applications

This research enables:

1. **Evidence-Based Governance**: Data-driven parameter adjustments based on system modeling
2. **Risk Mitigation**: Early identification of potential instabilities or attack vectors
3. **Economic Optimization**: Recommendations for improving capital efficiency and network security
4. **Strategic Planning**: Long-term roadmap development based on system trajectories

## Conclusion

By progressing from foundational taxonomies through systems engineering to mathematical specifications, this research provides Avalanche with the analytical tools necessary for sustainable growth. Each milestone builds upon previous work, creating a comprehensive framework that supports the network's core objectives of security, sustainability, value creation, and stability.

---

*Research conducted by the [Bonding Curve Research Group (BCRG)](/about/About-The-BCRG)*
