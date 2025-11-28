---
title: Subsystem Analysis and MultiGraph
---

**Last Updated:** November 28, 2025
**Draft Stage:** 3rd Draft

# Avalanche Economic Model: Subsystem Analysis and Multigraph Agent Modeling

This document decomposes the Avalanche network into five critical subsystems and models their interactions, providing the analytical foundation for the formal [Differential Specification](/milestone3/Differential_Specification). For foundational concepts, see [Economic Taxonomy](/milestone1/Economic-Taxonomy) and [Mechanism Taxonomy](/milestone1/Mechanism-Taxonomy). For participant role definitions, see [Participant Roles Taxonomy](/milestone1/Participant-Roles-Taxonomy). Current network metrics are sourced from the [Data Snapshot](/data/snapshot-2025-11-28).

---

## Table of Contents

- [Executive Summary](#executive-summary)
- [1. Introduction](#1-introduction)
- [2. Subsystem Specification Map](#2-subsystem-specification-map)
- [3. Multigraph State-Space Model](#3-multigraph-state-space-model)
- [4. Conclusion and Future Research](#4-conclusion-and-future-research)
- [Bibliography](#bibliography)

---

## Executive Summary

This report analyzes the Avalanche blockchain's economic model using a systems engineering approach. By decomposing the network into five critical subsystems and exploring their interactions, we provide a comprehensive framework for understanding Avalanche's economic dynamics. Additionally, we introduce a multigraph state-space model that maps complex agent behaviors across multiple roles, capturing emergent phenomena not visible in traditional analyses.

| Subsystem | Purpose | Key State Variables |
|-----------|---------|---------------------|
| Staking Dynamics | Network security via proof-of-stake | Total stake, validator/delegator counts, APR |
| Token Supply | Monetary policy and scarcity | Total supply, burn rate, net inflation |
| Fee Dynamics | Resource pricing and deflation | Gas price, excess consumption, burn rate |
| L1 Ecosystem | Application-specific chains | Active L1s, L1 validators, continuous fees |
| Governance | Protocol evolution | Parameter states, proposal rates, hysteresis |

The Avalanche network represents a sophisticated economic system with multiple participants, incentive structures, and value flows. Its distinctive architecture of a Primary Network with application-specific Layer 1 blockchains (L1s) creates unique economic challenges and opportunities. This report aims to support informed protocol development, governance decisions, and ecosystem growth.

---

## 1. Introduction

### 1.1 The Need for Systemic Analysis

Blockchain protocols are complex adaptive systems where changes to one component can have unforeseen consequences elsewhere. Traditional analyses often examine economic mechanisms in isolation, missing critical interactions that lead to unintended outcomes. A subsystem approach models the Avalanche network as interconnected functional modules, each with specific roles, state variables, and behaviors.

### 1.2 Core Economic Principles of Avalanche

| Principle | Description | Reference |
|-----------|-------------|-----------|
| **Capped Supply** | Maximum 720M AVAX tokens; ~460.6M currently minted | [Token Supply](#22-token-supply-subsystem) |
| **Deflationary Fees** | 100% of transaction fees burned, increasing scarcity with usage | [Fee Dynamics](#23-fee-dynamics-subsystem) |
| **Staking Incentives** | Rewards for network security via validation and delegation | [Staking Dynamics](#21-staking-dynamics-subsystem) |
| **Multi-Chain Architecture** | Economic specialization via application-specific L1s | [L1 Ecosystem](#24-l1-ecosystem-subsystem) |
| **Dynamic Fee Mechanism** | Fees adjust based on congestion ([ACP-103](/milestone2/ACP-Summaries#acp-103), [ACP-176](/milestone2/ACP-Summaries#acp-176)) | [Fee Dynamics](#23-fee-dynamics-subsystem) |
| **Governance Hysteresis** | Built-in stability controls prevent rapid parameter oscillations | [Governance](#25-governance-subsystem) |
| **Continuous L1 Fees** | L1 validators pay ongoing fees rather than large upfront stakes ([ACP-77](/milestone2/ACP-Summaries#acp-77)) | [L1 Ecosystem](#24-l1-ecosystem-subsystem) |

### 1.3 Key Network Participants

| Participant | Role | Current Count |
|-------------|------|---------------|
| **Primary Network Validators** | Stake AVAX and run consensus on P/X/C chains | ~1,400 |
| **L1 Validators** | Validate specific L1 chains, pay continuous fees | ~1,600 |
| **Delegators** | Delegate AVAX to validators for shared rewards | ~7,500 |
| **Users** | Conduct transactions and use dApps | — |
| **L1 Operators** | Launch and maintain application-specific chains | 53 L1s |
| **Developers** | Build applications and services | — |
| **Governance Participants** | Propose and vote on protocol changes via ACPs | — |

For detailed role definitions, see [Participant Roles Taxonomy](/milestone1/Participant-Roles-Taxonomy).

### 1.4 Recent Protocol Evolution

The subsystem dynamics documented here reflect the protocol state as of November 2025, incorporating major upgrades:

- **Etna / Avalanche9000 (December 2024)**: Fundamentally restructured L1 economics via [ACP-77](/milestone2/ACP-Summaries#acp-77), replacing 2,000 AVAX stake requirement with ~1.33 AVAX/month continuous fees
- **Octane (April 2025)**: Introduced dynamic gas limits via [ACP-176](/milestone2/ACP-Summaries#acp-176), enabling validator-driven throughput adjustment
- **Granite (November 2025)**: Added P-Chain epoched views ([ACP-181](/milestone2/ACP-Summaries#acp-181)), secp256r1 precompile ([ACP-204](/milestone2/ACP-Summaries#acp-204)), and dynamic block times ([ACP-226](/milestone2/ACP-Summaries#acp-226))

---

## 2. Subsystem Specification Map

### 2.1 Staking Dynamics Subsystem

The staking subsystem secures the network through proof-of-stake, balancing security requirements against capital efficiency. See [Economic Taxonomy: Staking Economics](/milestone1/Economic-Taxonomy#staking-economics) for foundational concepts.

#### 2.1.1 State Variables

| Variable | Symbol | Current Value | Description |
|----------|--------|---------------|-------------|
| Total Stake | $S_s$ | ~248M AVAX | Total AVAX staked across validators and delegators |
| Staking Ratio | — | ~57.8% | Percentage of circulating supply staked |
| Validator Stake | $S_v$ | ~210M AVAX | Direct validator stake |
| Delegation Stake | $S_d$ | ~38M AVAX | Delegated stake |
| Primary Validators | $V_p$ | ~1,400 | Validators securing P/X/C chains |
| L1 Validators | $V_l$ | ~1,600 | Validators securing specific L1s |
| Delegators | $D$ | ~7,500 | Active delegator addresses |

#### 2.1.2 Flow Variables

| Variable | Symbol | Current Value | Description |
|----------|--------|---------------|-------------|
| Reward Distribution | $R$ | ~49,000 AVAX/day | Daily staking rewards distributed |
| New Stake Rate | $\dot{S}_{in}$ | Variable | Rate of new stake entering the system |
| Unstake Rate | $\dot{S}_{out}$ | Variable | Rate of stake exiting the system |
| Validator Restake Rate | $R_v$ | ~70% | Proportion of validator rewards restaked |
| Delegator Restake Rate | $R_d$ | ~50% | Proportion of delegator rewards restaked |

#### 2.1.3 Parameters

| Parameter | Value | Description |
|-----------|-------|-------------|
| Min Validator Stake | 2,000 AVAX | Minimum to operate a Primary Network validator |
| Max Validator Stake | 3,000,000 AVAX | Maximum effective stake per validator |
| Min Delegator Stake | 25 AVAX | Minimum delegation amount |
| Staking Duration | 14–365 days | Allowable lockup period |
| Min Delegation Fee | 2% | Minimum validator commission on delegator rewards |
| Max Weight Factor | 5× | Maximum delegation relative to validator's own stake |
| Current APR | 7.65%–8.5% | Staking annual percentage rate |
| Uptime Requirement | 80% | Minimum uptime to receive rewards |

#### 2.1.4 Core Functions

Rewards are computed according to the Avalanche reward function:

$$
\mathrm{Reward} = (S_{\max} - S) \times \frac{S_{\text{stake}}}{S} \times \frac{T_{\text{stake}}}{T_{\text{mint}}} \times \mathrm{ECR}
$$

where the Effective Consumption Rate (ECR) scales linearly with duration:

$$
\mathrm{ECR} = \frac{r_{\min}}{D} \left(1 - \frac{T_{\text{stake}}}{T_{\text{mint}}}\right) + \frac{r_{\max}}{D} \cdot \frac{T_{\text{stake}}}{T_{\text{mint}}}
$$

Key operations:
- `calculateRewards(stake, duration)` — Compute expected rewards for given stake and lockup
- `projectStakeEvolution(horizon)` — Project stake distribution over time
- `calculateSecurityMetric()` — Assess network security based on stake distribution
- `optimizeStakingParams(targetSecurity)` — Find optimal parameters for security targets

#### 2.1.5 Key Interactions

| Coupled Subsystem | Interaction | Direction |
|-------------------|-------------|-----------|
| Token Supply | Reward issuance increases total supply | Staking → Supply |
| Governance | Staking parameters adjustable via ACPs | Governance → Staking |
| Fee Dynamics | Higher burns may increase staking APR attractiveness | Fees → Staking |
| L1 Ecosystem | L1 validators now separate from Primary Network validators | L1 ↔ Staking |

**Important Note (Post-Etna)**: L1 validators no longer require Primary Network validation or the 2,000 AVAX stake. This decoupling fundamentally changed staking dynamics—L1 validator growth no longer directly increases Primary Network stake.

---

### 2.2 Token Supply Subsystem

The token supply subsystem manages monetary policy through the tension between reward issuance (inflation) and fee burning (deflation). See [Economic Taxonomy: Token Issuance](/milestone1/Economic-Taxonomy#token-issuance) for foundational concepts.

#### 2.2.1 State Variables

| Variable | Symbol | Current Value | Description |
|----------|--------|---------------|-------------|
| Total Supply | $S$ | 460.6M AVAX | All tokens currently in existence |
| Max Supply | $S_{\max}$ | 720M AVAX | Hard cap on token supply |
| Circulating Supply | $S_c$ | ~429M AVAX | Tokens available for transactions |
| Locked Tokens | $S_l$ | ~31.6M AVAX | Tokens in lockup (staking, vesting) |
| Burned Tokens | $S_b$ | ~4.8M AVAX | Total tokens permanently destroyed |
| Remaining to Mint | — | ~259.4M AVAX | Tokens available for future rewards |

#### 2.2.2 Flow Variables

| Variable | Symbol | Current Value | Description |
|----------|--------|---------------|-------------|
| Issuance Rate | $\dot{S}_i$ | ~49,000 AVAX/day | Daily reward distribution |
| Burning Rate | $\dot{S}_b$ | ~1,500 AVAX/day | Daily fee burn (3× increase in 2025) |
| Net Inflation | $\dot{S}_n$ | ~47,500 AVAX/day | Issuance minus burn |
| Unlock Rate | $\dot{S}_l$ | Variable | Rate of token unlocks |

#### 2.2.3 Parameters

| Parameter | Value | Description |
|-----------|-------|-------------|
| Gross Annual Inflation | ~3.88% | From staking reward issuance |
| Annual Burn Rate | ~0.12% | From transaction fee destruction |
| Net Annual Inflation | ~3.76% | Gross inflation minus burn |
| Time to Max Supply | ~27 years | At current emission rates |

#### 2.2.4 Core Functions

- `projectSupplyEvolution(horizon)` — Model supply trajectory under various scenarios
- `calculateNetInflation()` — Compute current net inflation rate
- `simulateSupplyScenario(issuanceMod, burnMod)` — Test parameter change impacts
- `optimizeInflationParams(targetInflation)` — Find parameters achieving target inflation

#### 2.2.5 Key Interactions

| Coupled Subsystem | Interaction | Direction |
|-------------------|-------------|-----------|
| Staking | Rewards drive issuance; stake ratio affects emission rate | Staking → Supply |
| Fee Dynamics | All fees burned, creating deflationary pressure | Fees → Supply |
| L1 Ecosystem | L1 continuous fees contribute to burn | L1 → Supply |
| Governance | Emission parameters governable | Governance → Supply |

**Burn Rate Evolution**: The burn rate has increased 3× through 2025 (from ~500 to ~1,500 AVAX/day), driven by increased network activity. During peak periods (late 2025), burn rates spiked dramatically—at times reaching near-deflationary levels where burn approached issuance.

---

### 2.3 Fee Dynamics Subsystem

The fee subsystem prices network resources and generates deflationary pressure through burning. Major updates via [ACP-103](/milestone2/ACP-Summaries#acp-103) (dynamic P/X-Chain fees), [ACP-125](/milestone2/ACP-Summaries#acp-125) (96% C-Chain base fee reduction), and [ACP-176](/milestone2/ACP-Summaries#acp-176) (dynamic gas limits).

#### 2.3.1 State Variables

| Variable | Symbol | Current Value | Description |
|----------|--------|---------------|-------------|
| C-Chain Min Base Fee | $M$ | 1 nAVAX | Minimum gas price (reduced 96% via ACP-125) |
| Excess Gas Consumption | $x$ | Variable | Accumulated excess above target |
| Fee Adjustment Constant | $K$ | Protocol-defined | Controls price sensitivity |
| Daily Burn | $F_b$ | ~1,500 AVAX | AVAX burned from fees daily |
| Target Gas Rate | $T$ | 2.1M gas/second | C-Chain target (increased 30% via ACP-176) |

#### 2.3.2 Flow Variables

| Variable | Symbol | Description |
|----------|--------|-------------|
| Gas Consumption Rate | $G$ | Current gas usage per second |
| Fee Change Rate | $\dot{\phi}$ | Rate of base fee adjustment |
| L1 Fee Rate | $\dot{F}_l$ | Continuous fees from L1 validators |

#### 2.3.3 Parameters

| Parameter | Value | Description |
|-----------|-------|-------------|
| Target Throughput | 2.1M gas/s | C-Chain target (adjustable by validators) |
| Price Adjustment Constant | $K$ | Exponential scaling factor |
| Resource Weights | B + 1000R + 1000W + 4C | Bandwidth, Reads, Writes, Compute |

#### 2.3.4 Core Functions

**Multidimensional Gas (ACP-103)**:

$$
G = B + 1000 \cdot R + 1000 \cdot W + 4 \cdot C
$$

**Dynamic Fee Calculation**:

$$
\phi(t) = M \cdot e^{x/K}
$$

$$
\dot{x} = \begin{cases}
G - T, & G > T \\
\max(0, x - T), & G \le T
\end{cases}
$$

**Dynamic Gas Limit (ACP-176)**: Validators vote on target gas rate by signaling preferences in blocks. The effective rate converges where 50% of stake weight wants increase and 50% wants decrease—a market-discovered capacity equilibrium.

Key operations:
- `calculateGasConsumed(resources)` — Compute gas for transaction resources
- `calculateFeeRate(x)` — Get current fee given excess consumption
- `updateExcessConsumption(gas, T, dt)` — Update state after block
- `simulateFeeResponses(load)` — Model fee behavior under load scenarios
- `optimizeFeeParameters(util, maxVol)` — Find optimal fee parameters

#### 2.3.5 Key Interactions

| Coupled Subsystem | Interaction | Direction |
|-------------------|-------------|-----------|
| Token Supply | Burns reduce circulating supply | Fees → Supply |
| Staking | Lower fees may increase relative APR attractiveness | Fees → Staking |
| L1 Ecosystem | L1 continuous fees use same mechanism | L1 ↔ Fees |
| Governance | Dynamic limits reduce governance burden | Fees ↔ Governance |

---

### 2.4 L1 Ecosystem Subsystem

The L1 ecosystem enables application-specific sovereign chains with custom economic models. **Fundamentally restructured by [ACP-77](/milestone2/ACP-Summaries#acp-77) (Etna upgrade, December 2024)**—the largest economic change since mainnet launch.

#### 2.4.1 State Variables

| Variable | Symbol | Current Value | Description |
|----------|--------|---------------|-------------|
| Active L1s | $L$ | 53 (14 modern, 39 legacy) | Total L1 chains |
| L1 Validators | $V_l$ | ~1,600 | Validators serving L1s |
| Legacy L1 Stake | $S_{l,\text{leg}}$ | ~470,000 AVAX | Pre-Etna subnet stake |

#### 2.4.2 Flow Variables

| Variable | Symbol | Description |
|----------|--------|-------------|
| Creation Rate | $\dot{L}_c$ | New L1s launched per period |
| Abandonment Rate | $\dot{L}_a$ | L1s going inactive per period |
| Migration Rate | $\dot{L}_m$ | Legacy subnets converting to modern L1s |
| Continuous Fee Generation | $\dot{F}_l$ | L1 validator fees burned to P-Chain |

#### 2.4.3 Economic Model Evolution

**Legacy Model (Pre-Etna)**:
- L1 validators required 2,000 AVAX stake
- Must also validate Primary Network (P/X/C chains)
- Capital barrier: ~$70,000 per validator
- Minimum 5 validators per subnet: $350,000+ total capital

**Modern Model (Post-Etna/ACP-77)**:
- L1 validators pay continuous fee (~1.33 AVAX/month at baseline)
- No Primary Network validation required
- No 2,000 AVAX stake requirement
- Capital barrier reduced 99.9%
- Custom validation rules (PoA, PoS, ERC-20/ERC-721 staking)
- P-Chain only synchronization (reduced hardware costs)

#### 2.4.4 Parameters

| Parameter | Value | Description |
|-----------|-------|-------------|
| Continuous Fee Base | 512 nAVAX/second | ~1.33 AVAX/month per validator |
| Target Validator Capacity | 10,000 | L1 validators before fee escalation |
| Max Validator Capacity | 20,000 | Hard limit on L1 validators |
| Fee Scaling Factor | $e^{(V-T)/K}$ | Exponential above target |

#### 2.4.5 Core Functions

**Continuous Fee Calculation**:

$$
C_L = M \cdot e^{x/K}, \quad x \leftarrow \max(x + (V - T), 0)
$$

Where $V$ is current L1 validator count and $T$ is target capacity.

Key operations:
- `projectL1Growth(horizon)` — Model L1 ecosystem expansion
- `calculateL1Fee(validatorCount)` — Compute current continuous fee rate
- `simulateNetworkEffects(crossActivity)` — Model cross-L1 value flows
- `optimizeL1Params(targetGrowth, maxFee)` — Find optimal fee parameters

#### 2.4.6 Key Interactions

| Coupled Subsystem | Interaction | Direction |
|-------------------|-------------|-----------|
| Token Supply | L1 continuous fees burned | L1 → Supply |
| Staking | L1 validators decoupled from Primary Network (post-Etna) | L1 ↔ Staking |
| Fee Dynamics | L1 fees use same dynamic mechanism | L1 ↔ Fees |
| Governance | L1 parameters adjustable; L1s have sovereign governance | Governance ↔ L1 |

**Sovereignty Features**: Post-ACP-77, L1s can implement custom validation rules, use any token for staking (ERC-20, ERC-721), and manage their own validator sets via Validator Manager contracts ([ACP-99](/milestone2/ACP-Summaries#acp-99)).

---

### 2.5 Governance Subsystem

The governance subsystem manages protocol evolution through the ACP process and parameter adjustment mechanisms. See [Economic Taxonomy: Governance Architecture](/milestone1/Economic-Taxonomy#governance-architecture) and [ACP Summaries](/milestone2/ACP-Summaries) for details.

#### 2.5.1 State Variables

| Variable | Symbol | Description |
|----------|--------|-------------|
| Governable Parameters | $P$ | Set of adjustable protocol parameters |
| Last Change Timestamp | $t_{\text{last}}$ | When parameter was last modified |
| Change History | $H$ | Record of parameter modifications |
| Active Proposals | — | ACPs under consideration |

#### 2.5.2 Flow Variables

| Variable | Symbol | Description |
|----------|--------|-------------|
| Proposal Rate | $\dot{P}_r$ | New ACPs submitted per period |
| Implementation Rate | $\dot{P}_i$ | ACPs activated per period |
| Parameter Change Rate | $\dot{p}$ | Rate of parameter modification |

#### 2.5.3 Parameters

| Parameter | Description |
|-----------|-------------|
| Max Change Rate | Maximum parameter adjustment per time unit |
| Min Interval | Minimum time between changes to same parameter |
| Hysteresis Factor | Difficulty increase for rapid sequential changes |

#### 2.5.4 Core Functions

**Hysteresis Constraint**: A parameter change is valid only if:

$$
|p_{\text{new}} - p_{\text{cur}}| \le \text{MaxChangeRate} \cdot (t - t_{\text{last}}), \quad t - t_{\text{last}} \ge \text{MinInterval}
$$

Key operations:
- `validateParameterChange(newP)` — Check change against hysteresis constraints
- `simulateGovernanceDecision(proposal, voters)` — Model voting outcomes
- `optimizeParams(objectives, constraints)` — Multi-objective parameter optimization
- `projectParameterEvolution(horizon)` — Forecast parameter trajectories

#### 2.5.5 Governance Mechanisms

| Mechanism | Description |
|-----------|-------------|
| **ACP Process** | Formal proposal, review, implementation cycle |
| **On-Chain Voting** | Limited parameters adjustable via validator voting |
| **Dynamic Adjustment** | ACP-176 enables validator-driven gas limit changes |
| **L1 Sovereignty** | L1s control their own governance parameters |

#### 2.5.6 Key Interactions

| Coupled Subsystem | Interaction | Direction |
|-------------------|-------------|-----------|
| Staking | Adjust reward parameters, duration limits | Governance → Staking |
| Token Supply | Modify emission parameters | Governance → Supply |
| Fee Dynamics | Change fee structure; dynamic limits reduce governance burden | Governance ↔ Fees |
| L1 Ecosystem | Update L1 parameters; L1s have sovereign governance | Governance ↔ L1 |

---

### 2.6 Subsystem Interactions

#### 2.6.1 Critical Feedback Loops

| Loop | Subsystems | Mechanism | Effect |
|------|------------|-----------|--------|
| **Staking-Supply** | Staking ↔ Supply | Rewards inflate supply; inflation affects staking attractiveness | Self-regulating |
| **Fee-Supply** | Fees ↔ Supply | Burns deflate supply; lower supply may increase fee willingness | Deflationary pressure |
| **L1-Validator Decoupling** | L1 ↔ Staking | Post-Etna, L1 growth doesn't increase Primary Network stake | Independence |
| **Dynamic Adjustment** | Fees ↔ Governance | Validator voting on gas limits reduces governance overhead | Self-tuning |

#### 2.6.2 Emergent Properties

- **Economic Equilibria**: Balances emerge between staking rewards, fee burning, and L1 adoption
- **Self-Regulation**: Dynamic fee mechanisms maintain target utilization without governance intervention
- **Parameter Sensitivity**: Identify high-impact governance levers through subsystem coupling analysis

#### 2.6.3 Resilience Considerations

- **Parameter Coupling**: Monitor interdependencies to avoid unintended cascades
- **Stress Testing**: Simulate extreme scenarios (demand spikes, validator exits)
- **Feedback Loop Management**: Hysteresis mechanisms prevent runaway parameter changes

For formal mathematical treatment of these dynamics, see [Differential Specification](/milestone3/Differential_Specification).

---

## 3. Multigraph State-Space Model

### 3.1 Introduction to Multigraph Modeling

Traditional models treat participants as single-role actors. In Avalanche, participants occupy multiple roles and deploy cross-mechanism strategies. The Multigraph State-Space Model (MSSM) explicitly captures these behaviors by modeling:

- **Agents** as nodes with multi-role assignments
- **Roles** as functional positions (validator, delegator, trader, L1 operator)
- **Edges** representing agent-role and agent-agent relationships

This approach reveals emergent behaviors invisible in role-isolated analysis. For participant role definitions, see [Participant Roles Taxonomy](/milestone1/Participant-Roles-Taxonomy).

### 3.2 Model Structure and Components

#### 3.2.1 Agent State Vector

Each agent $i$ maintains state:

$$
\mathbf{a}_i = \begin{bmatrix}
b_i & \text{(token balance)} \\
\mathbf{r}_i & \text{(role assignments)} \\
\mathbf{s}_i & \text{(strategy parameters)} \\
\mathbf{h}_i & \text{(interaction history)}
\end{bmatrix}
$$

#### 3.2.2 Role Definitions

| Role | State Components | Strategy Space |
|------|------------------|----------------|
| **Validator** | Stake amount, commission rate, uptime, reputation | Commission setting, hardware investment |
| **Delegator** | Delegated amount, validator selection | Validator choice, restaking decisions |
| **Governance Participant** | Voting weight, proposal history | Vote allocation, proposal timing |
| **Trader** | Position size, trading strategy | Buy/sell timing, size optimization |
| **L1 Operator** | L1 stake, validator set, fee revenue | L1 parameters, validator recruitment |
| **Liquid Staking User** | LST balance, protocol selection | Protocol choice, leverage decisions |

#### 3.2.3 Edge Types

| Edge Type | Connects | Carries |
|-----------|----------|---------|
| **Agent-Role** | Agent → Role | Role-specific state, strategy |
| **Delegation** | Delegator → Validator | Delegated amount, fee agreement |
| **L1 Validation** | Validator → L1 | Validation commitment, fees |
| **Token Transfer** | Agent → Agent | Transfer amount, timestamp |
| **Governance** | Agent → Proposal | Vote weight, direction |

### 3.3 Agent Behavior Modeling

#### 3.3.1 Multi-Role Strategy Integration

Agents optimize across roles simultaneously, creating cross-role strategies:

| Strategy | Roles Combined | Behavior |
|----------|----------------|----------|
| **Validator-Trader** | Validator + Trader | Time reward claims with market conditions |
| **Delegator-Governance** | Delegator + Governance | Choose validators aligned with governance preferences |
| **L1 Operator-Validator** | L1 Operator + Validator | Self-validate for cost reduction |
| **LST User-DeFi** | LST Holder + DeFi User | Recursive leverage via liquid staking |

#### 3.3.2 Strategy Function Representation

Each strategy maps state and history to action:

$$
S_{i,r}(\text{state}, \text{history}) \to \text{action}
$$

where $i$ is agent index and $r$ is role.

**Example: Validator Commission Strategy**:

$$
c_i(t) = c_{\min} + \alpha \cdot (\text{reputation}_i - \text{rep}_{\text{avg}})
$$

High-reputation validators can charge higher commissions; new validators must compete on price.

#### 3.3.3 Emergent Behavior Examples

| Behavior | Mechanism | System Impact |
|----------|-----------|---------------|
| **Stake Concentration Cycles** | Top validators attract more delegation, increasing reward share | Centralization pressure |
| **Cross-Role Arbitrage** | Exploit pricing differences across roles (e.g., LST vs native staking) | Market efficiency |
| **Coalition Formation** | Validators coordinate on governance votes | Governance centralization |
| **Liquid Staking Recursive Leverage** | Stake → LST → Collateral → Borrow → Stake | Systemic risk |

### 3.4 Simulation and Analysis Framework

#### 3.4.1 Agent-Based Simulation

**Initialization**:
- Instantiate agents with realistic distributions (stake amounts, role assignments)
- Calibrate from on-chain data (validator distribution from Avascan, delegation patterns)

**Execution**:
- Each timestep: agents observe state, execute strategies, update positions
- Protocol mechanics process transactions, distribute rewards, burn fees
- Record emergent metrics

**Calibration Sources**:
- Validator distribution: P-Chain state queries
- Delegation patterns: Staking transaction history
- Trading behavior: C-Chain DEX activity
- L1 activity: L1-specific RPC endpoints

#### 3.4.2 Network Analysis Metrics

| Metric | Measure | Interpretation |
|--------|---------|----------------|
| **Degree Centrality** | Connection count per agent | Influence breadth |
| **Betweenness Centrality** | Bridge position frequency | Information/value flow control |
| **Eigenvector Centrality** | Connection quality | Influence via connected agents |
| **Community Detection** | Cluster identification (Louvain, label propagation) | Coalition identification |
| **Flow Analysis** | Token/influence path tracing | Value concentration patterns |

#### 3.4.3 System Health Indicators

| Indicator | Formula | Target |
|-----------|---------|--------|
| **Decentralization Index** | $1 - \text{Gini}(\text{stake})$ | Higher is better (>0.3) |
| **Economic Efficiency** | $\text{TVL} / \text{Total Stake}$ | Higher indicates capital efficiency |
| **System Resilience** | Tolerance to top-N validator failure | Survive loss of top 10 validators |
| **Governance Participation** | Active voters / total stake weight | >50% participation |

### 3.5 Applications to Economic Design

#### 3.5.1 Mechanism Alignment Analysis

Detect incentive misalignments before deployment:
- Do validator rewards align with network security goals?
- Does L1 fee structure encourage efficient resource use?
- Are delegation incentives balanced against centralization risks?

#### 3.5.2 Incentive Gap Detection

Identify unintended arbitrage opportunities:
- Cross-role strategies that extract value without providing security
- Recursive leverage patterns that amplify systemic risk
- Governance attack vectors through stake accumulation

#### 3.5.3 Parameter Optimization

Multi-objective optimization across subsystems:
- Security constraints (minimum stake distribution)
- Efficiency goals (capital utilization, transaction throughput)
- Fairness requirements (reward distribution, access costs)

#### 3.5.4 Regulatory Impact Assessment

Model external policy effects:
- Staking reporting requirements
- Exchange delisting scenarios
- Institutional participation constraints

---

## 4. Conclusion and Future Research

### 4.1 Key Insights

| Insight | Implication |
|---------|-------------|
| **Subsystem Interdependence** | Changes to one subsystem propagate to others; isolated analysis insufficient |
| **Participant Complexity** | Multi-role agents create emergent behaviors beyond simple models |
| **Post-Etna Decoupling** | L1 economics now largely independent of Primary Network staking |
| **Dynamic Self-Tuning** | ACP-176 enables market-discovered capacity without governance overhead |

### 4.2 Protocol Design Implications

- **Holistic Evaluation**: Assess mechanism changes across all five subsystems
- **Behavior Anticipation**: Model multi-role strategies before deployment
- **Parameter Coupling Management**: Use hysteresis and gradual rollouts
- **Governance Efficiency**: Shift routine adjustments to validator voting mechanisms

### 4.3 Future Research Directions

| Direction | Description | Related Documents |
|-----------|-------------|-------------------|
| **Differential Specification** | Formalize subsystem dynamics as differential equations | [Differential Specification](/milestone3/Differential_Specification) |
| **Economic Hypotheses** | Derive testable predictions from subsystem models | [Economic Hypotheses](/milestone4/economic_hypotheses) |
| **Empirical Validation** | Calibrate models against on-chain data | [Data Snapshot](/data/snapshot-2025-11-28) |
| **Governance Simulation** | Long-term scenario analysis of parameter evolution | Future work |
| **LST Systemic Risk** | Model recursive leverage and depegging scenarios | Future work |

---

## Bibliography

1. Ava Labs. *Avalanche Platform Whitepaper*. 2020. https://www.avalabs.org/whitepapers

2. Ava Labs. *Avalanche Consensus Protocol Whitepaper*. 2020. https://www.avalabs.org/whitepapers

3. Avalanche. *AVAX Token Documentation*. Avalanche Builder Hub. https://build.avax.network/docs/quick-start/avax-token

4. Avalanche. *Staking Documentation*. Avalanche Builder Hub. https://build.avax.network/docs/nodes/validate/how-to-stake

5. Avalanche Foundation. *Avalanche Community Proposals (ACPs)*. GitHub. https://github.com/avalanche-foundation/ACPs

6. Avalanche Foundation. *ACP-77: Reinventing Subnets*. 2024. https://github.com/avalanche-foundation/ACPs/tree/main/ACPs/77-reinventing-subnets

7. Avalanche Foundation. *ACP-103: Dynamic Fees*. 2024. https://github.com/avalanche-foundation/ACPs/tree/main/ACPs/103-dynamic-fees

8. Avalanche Foundation. *ACP-176: Dynamic EVM Gas Limits*. 2025. https://github.com/avalanche-foundation/ACPs/tree/main/ACPs/176-dynamic-evm-gas-limit-and-price-discovery-updates

9. Messari. *State of Avalanche Q1 2025*. https://messari.io/report/state-of-avalanche-q1-2025

10. Messari. *State of Avalanche Q2 2025*. https://messari.io/report/state-of-avalanche-q2-2025
