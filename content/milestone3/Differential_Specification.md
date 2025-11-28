
# Avalanche Differential Specification and Protocol Architecture

## 1. Overview

This differential specification characterizes how the Avalanche economic system evolves over time, providing a mathematical framework for understanding system dynamics that may be governable, environmental, relational, or mechanistic. The specification builds upon the Avalanche Economic Network exploratory analysis developed in previous milestones and seeks to formalize the state dynamics and feedback loops inherent in the Avalanche network.

The Avalanche network represents a complex adaptive dynamical system where technical and economic components influence each other continuously. This creates distinct economic challenges and opportunities that require sophisticated control-theoretic understanding to navigate effectively. This specification provides formal and analytic contexts through which to analyze the unique architecture of the AVAX Token, the Primary Network, and application-specific Layer 1 blockchains (L1s).

Building on the foundational economic concepts (Milestone 1) and systems engineering perspective (Milestone 2), this differential specification provides a rigorous mathematical framework consisting of coupled differential equations that model the dynamic interactions between token supply, staking behavior, fee markets, and the L1 ecosystem. The specification transforms qualitative understanding into mathematical relationships, enabling systematic analysis of how financial and governance interfaces can impact network behavior.

---

## 2. Mathematical Framework

This section provides comprehensive reference tables for all variables, equations, and parameters used throughout the specification. These tables serve as a quick reference, with detailed explanations provided in subsequent sections.

### 2.1 State Variables

| Variable | Units | Subsystem |
|----------|-------|-----------|
| total_staked | AVAX | Staking |
| validator_staked | AVAX | Staking |
| delegator_staked | AVAX | Staking |
| staking_apr | % | Staking |
| validator_count | Integer | Staking |
| total_supply | AVAX | Token Supply |
| circulating_supply | AVAX | Token Supply |
| cumulative_burned | AVAX | Token Supply |
| issuance_rate | AVAX/day | Token Supply |
| gas_price | nAVAX | Fee Dynamics |
| fee_burn_rate | AVAX/day | Fee Dynamics |
| network_utilization | % | Fee Dynamics |
| l1_count | Integer | L1 Ecosystem |
| l1_fee_burn_rate | AVAX/day | L1 Ecosystem |
| standard_acp_count | Integer | Governance |
| best_practices_acp_count | Integer | Governance |
| meta_acp_count | Integer | Governance |
| l1_acp_count | Integer | Governance |
| proposed_acp_count | Integer | Governance |
| implementable_acp_count | Integer | Governance |
| stale_acp_count | Integer | Governance |
| activated_acp_count | Integer | Governance |

### 2.2 Dynamic Functions

| Function | Description |
|----------|-------------|
| staking_inflow() | Rate of new AVAX entering staking pools |
| unstaking_outflow() | Rate of AVAX leaving staking pools |
| reward_distribution() | Staking rewards distributed per unit time |
| token_issuance() | New AVAX minted per unit time |
| validator_entry_rate() | New validators joining per unit time |
| validator_exit_rate() | Validators leaving per unit time |
| l1_creation_rate() | New L1s deployed per unit time |
| l1_abandonment_rate() | L1s discontinued per unit time |

### 2.3 Differential Equations Summary

The following table presents all laws of motion. Detailed explanations are provided in Section 4.

| Variable | Law of Motion | Description |
|----------|---------------|-------------|
| total_staked | d(total_staked)/dt = staking_inflow() − unstaking_outflow() + AVG_RESTAKE_RATE × reward_distribution() | Total stake changes via inflows, outflows, and re-staking |
| validator_staked | d(validator_staked)/dt = validator_staking_inflow() − validator_unstaking_outflow() + 0.70 × validator_rewards() | Validator stake with 70% reward re-staking |
| delegator_staked | d(delegator_staked)/dt = delegator_staking_inflow() − delegator_unstaking_outflow() + 0.50 × delegator_rewards() | Delegator stake with 50% reward re-staking |
| validator_count | d(validator_count)/dt = validator_entry_rate() − validator_exit_rate() | Validator count changes via entry/exit |
| total_supply | d(total_supply)/dt = issuance_rate | Total supply increases by issuance (capped at MAX_SUPPLY) |
| circulating_supply | d(circulating_supply)/dt = issuance_rate − d(total_staked)/dt + unlock_rate() | Circulating supply adjusted for staking and unlocks |
| cumulative_burned | d(cumulative_burned)/dt = fee_burn_rate + l1_fee_burn_rate | Cumulative burn from Primary Network and L1 fees |
| gas_price | gas_price = MIN_GAS_PRICE × exp(excess_gas / FEE_ADJUSTMENT_CONSTANT) | Gas price via exponential adjustment (ACP-103) |
| fee_burn_rate | fee_burn_rate = gas_price × gas_consumed | Fee burn rate equals gas price times consumption |
| l1_count | d(l1_count)/dt = l1_creation_rate() − l1_abandonment_rate() | L1 count changes via creation/abandonment |
| l1_fee_burn_rate | l1_fee_burn_rate = L1_BASE_FEE_RATE × l1_validator_count | L1 fees from continuous validator payments (ACP-77) |
| acp_count_by_track | d(acp_count)/dt = proposal_rate() − implementation_rate() − stale_rate() | ACP counts by track |

**Key Identities:**
- total_staked = validator_staked + delegator_staked (stake accounting)
- circulating_supply + total_staked + locked_supply ≤ total_supply (supply conservation)
- l1_validator_count ≤ validator_count (L1 validators must be Primary Network validators)

### 2.4 Parameters and Constants

#### Protocol Constants

| Parameter | Value | Source |
|-----------|-------|--------|
| MAX_SUPPLY | 720,000,000 AVAX | Protocol |
| MIN_VALIDATOR_STAKE | 2,000 AVAX | Protocol |
| MAX_VALIDATOR_STAKE | 3,000,000 AVAX | Protocol |
| MIN_STAKE_DURATION | 14 days | Protocol |
| MAX_STAKE_DURATION | 365 days | Protocol |
| MIN_CONSUMPTION_RATE | 10% | Protocol |
| MAX_CONSUMPTION_RATE | 12% | Protocol |
| MINTING_PERIOD | 365 days | Protocol |

#### Fee Mechanism Parameters (ACP-103)

| Parameter | Value | Description |
|-----------|-------|-------------|
| FEE_ADJUSTMENT_CONSTANT | 2,164,043 | Exponential scaling factor |
| TARGET_GAS_RATE | 50,000 gas/s | Equilibrium utilization target |
| BANDWIDTH_WEIGHT | 1 | Gas cost per byte |
| READ_WEIGHT | 1,000 | Gas cost per state read |
| WRITE_WEIGHT | 1,000 | Gas cost per state write |
| COMPUTE_WEIGHT | 4 | Gas cost per microsecond |

#### L1 Fee Parameters (ACP-77)

| Parameter | Value | Description |
|-----------|-------|-------------|
| L1_BASE_FEE_RATE | 512 nAVAX/s | ≈ 1.33 AVAX/month |
| L1_FEE_SCALING_CONSTANT | 1,246,488,515 | Exponential scaling factor |
| TARGET_L1_VALIDATOR_CAPACITY | 10,000 | Before fee escalation |

#### Observed Behavioral Parameters

| Parameter | Value | Description |
|-----------|-------|-------------|
| VALIDATOR_RESTAKE_RATE | 70% | Fraction of rewards re-staked by validators |
| DELEGATOR_RESTAKE_RATE | 50% | Fraction of rewards re-staked by delegators |
| AVG_RESTAKE_RATE | 67% | Weighted average |

#### Current Network State (Reference)

| Metric | Value | Description |
|--------|-------|-------------|
| total_supply | ~456M AVAX | Current minted tokens |
| staking_ratio | ~52% | total_staked / circulating_supply |
| staking_apr | ~9.5% | Current reward rate |
| daily_issuance | ~26,555 AVAX | issuance_rate |
| daily_burn | ~749 AVAX | fee_burn_rate + l1_fee_burn_rate |
| validator_count | ~1,372 | Active validators |
| l1_count | ~66 | Active L1s |

### 2.5 Subsystem Coupling Matrix

This matrix shows which subsystems directly affect each other through shared state variables or feedback mechanisms.

| Affects → | Staking | Token Supply | Fee Dynamics | L1 Ecosystem | Governance |
|-----------|---------|--------------|--------------|--------------|------------|
| **Staking** | — | issuance_rate depends on total_staked | Effective APR | l1_validator_count ≤ validator_count | Stake-weighted voting |
| **Token Supply** | APR calculation | — | — | — | — |
| **Fee Dynamics** | Real returns | cumulative_burned rate | — | Combined burn | Fee parameters |
| **L1 Ecosystem** | Validator load | l1_fee_burn_rate | L1 activity | — | L1 proposals |
| **Governance** | Stake params | Inflation params | Fee params | L1 params | — |

**Primary Feedback Loops:**

| Loop | Type | Mechanism |
|------|------|-----------|
| Fee Burning Value | Reinforcing | Activity ↑ → Burn ↑ → Scarcity ↑ → Value ↑ → Activity ↑ |
| Staking Security | Balancing | APR ↑ → Staking ↑ → Liquidity ↓ → Activity ↓ |
| L1 Growth | Reinforcing | L1s ↑ → Activity ↑ → Ecosystem Value ↑ → L1s ↑ |

### 2.6 System Architecture

The following diagram illustrates the interconnected subsystems and their relationships within the Avalanche economic model:

![Avalanche Differential Specification System Architecture](/static/diff-spec.png)

---

## 3. Component Specification

This section describes the qualitative processes and mechanisms that drive system dynamics. The mathematical formulations are provided in Section 2.3, with detailed explanations in Section 4.

### 3.1 Environmental Processes

Environmental processes represent external forces modeled as potentially state-dependent stochastic processes. These serve as driving inputs during simulation and are fed with real data during live system operation.

| Process | Description | Affects |
|---------|-------------|---------|
| transaction_volume | Network demand for block space | Fee dynamics, burn rate |
| market_conditions | AVAX price, crypto sentiment, macro factors | Staking behavior, validator participation |
| l1_demand | Developer demand for application-specific chains | L1 creation, validator requirements |
| validator_behavior | Entry/exit decisions, operational reliability | Network security, decentralization |
| cross_chain_activity | Bridge usage, wrapped tokens, interoperability | AVAX demand/supply |

### 3.2 Behavioral Processes

Behavioral processes represent deterministic responses to system state by network participants.

| Behavior | Agent | Key Factors |
|----------|-------|-------------|
| staking_decision | Token holders | staking_apr, duration options, opportunity cost |
| validator_role | Node operators | Rewards, operational costs, technical requirements |
| delegator_role | Passive stakers | Validator performance, commission rates, capacity |
| l1_developer_role | Builders | Economic viability, technical requirements |
| transaction_submission | Users | gas_price, congestion, urgency |
| governance_participation | Stakeholders | Stake holdings, proposal impacts |

### 3.3 Controlled Processes

Controlled processes are algorithmic policies under protocol control.

| Control | Mechanism | Reference |
|---------|-----------|-----------|
| inflation_rate_policy | Duration-dependent consumption rate (MIN_CONSUMPTION_RATE to MAX_CONSUMPTION_RATE) | Avalanche Whitepaper |
| fee_market_control | Exponential adjustment to TARGET_GAS_RATE | ACP-103 |
| l1_validator_fee_policy | Continuous fees with exponential scaling | ACP-77 |
| staking_parameters | MIN_VALIDATOR_STAKE, duration limits | Protocol |
| governance_parameters | Voting thresholds, hysteresis constraints | Protocol |

### 3.4 Mechanisms

Mechanisms are the deterministic state update functions implementing protocol rules.

| Mechanism | Function | Key Formula |
|-----------|----------|-------------|
| staking_rewards | Distribute rewards to stakers | reward_distribution() = (MAX_SUPPLY − total_supply) × (total_staked / total_supply) × (avg_duration / MINTING_PERIOD) × effective_consumption_rate |
| fee_burning | Burn 100% of transaction fees | d(cumulative_burned)/dt = fee_burn_rate + l1_fee_burn_rate |
| token_issuance | Mint new AVAX as rewards | issuance_rate = reward_distribution() |
| l1_validator_fees | Continuous fee collection | l1_fee_burn_rate = L1_BASE_FEE_RATE × exp(excess / L1_FEE_SCALING_CONSTANT) × l1_validator_count |
| validator_management | Entry/exit processing | d(validator_count)/dt = validator_entry_rate() − validator_exit_rate() |
| delegation_processing | Reward distribution with commission | delegator_rewards() = reward_distribution() × (1 − commission_rate) |
| governance_execution | Parameter updates via ACP process | Subject to hysteresis constraints |

---

## 4. System Dynamics

This section provides intuitive explanations of how each subsystem evolves over time. The mathematical equations are summarized in Section 2.3; here we focus on the economic meaning and practical implications.

### 4.1 Staking Dynamics

The staking subsystem governs the flow of AVAX between liquid and staked states, determining network security and reward distribution.

**How Staking Evolves:**
The total_staked amount changes through three channels: new deposits enter via the staking_inflow() function, existing stakes exit via the unstaking_outflow() function, and a portion of rewards are re-staked. Empirically, validators re-stake about 70% of rewards (VALIDATOR_RESTAKE_RATE) while delegators re-stake about 50% (DELEGATOR_RESTAKE_RATE), yielding AVG_RESTAKE_RATE of 67%.

**What Drives Staking Decisions:**
Participants compare the staking_apr against opportunity costs—what they could earn elsewhere. When staking_apr exceeds alternatives, staking increases; when alternatives are more attractive, unstaking accelerates. The staking_inflow() function uses a tanh response curve, ensuring bounded behavior even under extreme APR differentials.

**Validator Population:**
The validator_count evolves based on profitability. New validators enter when expected returns exceed MIN_VALIDATOR_STAKE (2,000 AVAX) and operational costs. Validators exit when profitability falls below sustainable levels or L1 validation burden becomes excessive.

**The Accounting Identity:**
Total stake always equals validator stake plus delegator stake (total_staked = validator_staked + delegator_staked). This constraint is fundamental and must be preserved by all state updates.

### 4.2 Token Supply Dynamics

The token supply subsystem tracks AVAX creation and destruction, governing long-term monetary policy.

**Supply Growth:**
The total_supply increases through issuance_rate, which flows entirely to stakers as rewards. The issuance rate depends on how much supply remains below MAX_SUPPLY (720M)—as total_supply approaches the maximum, issuance naturally decreases toward zero.

**The Reward Formula:**
The official Avalanche reward formula creates duration-dependent returns. The effective_consumption_rate interpolates between MIN_CONSUMPTION_RATE (10% for minimum 14-day stake) and MAX_CONSUMPTION_RATE (12% for maximum 365-day stake), incentivizing longer commitments.

**Circulating Supply:**
The circulating_supply equals total_supply minus total_staked and locked_supply. It increases with issuance and token unlocks, but decreases when staking increases. This creates a natural tension between staking rewards and liquid supply.

**Deflationary Pressure:**
All transaction fees are burned, permanently removing AVAX from circulation. The cumulative_burned grows by the combined burn rate from Primary Network fees (fee_burn_rate) and L1 fees (l1_fee_burn_rate). Currently burning ~749 AVAX/day against ~26,555 AVAX/day issuance, the network will become net deflationary when fee activity increases approximately 33-fold.

### 4.3 Fee Market Dynamics

The fee subsystem implements congestion pricing through the ACP-103 multidimensional fee mechanism.

**How Fees Adjust:**
The gas_price follows an exponential adjustment mechanism. When network_utilization exceeds TARGET_GAS_RATE (50,000 gas/second), an excess_gas state variable accumulates, driving prices up exponentially. When utilization drops below target, the excess decays and gas_price falls back toward the minimum.

**Why Exponential:**
The exponential mechanism (gas_price = MIN_GAS_PRICE × exp(excess_gas / FEE_ADJUSTMENT_CONSTANT)) provides several benefits: rapid response to sudden congestion, smooth price curves, and guaranteed minimum fees. The FEE_ADJUSTMENT_CONSTANT controls responsiveness—larger values mean slower adjustment.

**Multidimensional Gas:**
Transaction costs reflect actual resource consumption across four dimensions: bandwidth (bytes), state reads, state writes, and compute time. The gas formula:

```
gas_consumed = bytes × BANDWIDTH_WEIGHT + reads × READ_WEIGHT + writes × WRITE_WEIGHT + compute_us × COMPUTE_WEIGHT
```

weights these appropriately (1, 1000, 1000, 4 respectively), ensuring heavy operations pay proportionally more.

**Equilibrium:**
At equilibrium, network_utilization equals TARGET_GAS_RATE, excess_gas is zero, and gas_price equals MIN_GAS_PRICE. The system naturally returns to this state during low-demand periods.

### 4.4 L1 Ecosystem Dynamics

The L1 subsystem tracks application-specific blockchain creation and the continuous fee mechanism from ACP-77.

**L1 Lifecycle:**
The l1_count evolves through creation and abandonment. The l1_creation_rate() depends on developer demand and fee levels—higher fees dampen creation exponentially. The l1_abandonment_rate() increases when L1 profitability falls below sustainable thresholds.

**Continuous Fees:**
Unlike one-time staking requirements, ACP-77 introduces continuous fees for L1 validators. The L1_BASE_FEE_RATE (512 nAVAX/second ≈ 1.33 AVAX/month) scales exponentially when total l1_validator_count exceeds TARGET_L1_VALIDATOR_CAPACITY (10,000). This right-sizes validator participation to actual demand.

**Validator Constraint:**
Every L1 validator must also be a Primary Network validator (l1_validator_count ≤ validator_count). This ensures L1 security derives from the broader network while allowing L1-specific customization.

### 4.5 Governance Dynamics

The governance subsystem tracks ACP proposal flows and implements stability constraints.

**Proposal Lifecycle:**
ACPs flow through stages: proposed_acp_count → implementable_acp_count → activated_acp_count, with some becoming stale_acp_count. Each track (Standard, Best Practices, Meta, L1) has its own proposal dynamics based on community activity.

**Hysteresis Constraints:**
To prevent instability, parameter changes face rate limits. The maximum change magnitude depends on time since the last change, and minimum intervals between changes are enforced. This prevents rapid oscillations that could destabilize the network.

---

## 5. Equilibrium and Stability Analysis

This section analyzes system equilibria and stability properties derived from the differential equations.

### 5.1 Staking Equilibrium

At equilibrium, staking inflows equal outflows adjusted for re-staking:

```
staking_inflow_eq = unstaking_outflow_eq − AVG_RESTAKE_RATE × reward_distribution_eq
```

The equilibrium staking ratio depends on the staking_apr versus opportunity cost differential. With current parameters, the target range is 50-60% of circulating_supply staked. Below 50%, security concerns may arise; above 60%, liquidity constraints may impede network utility.

**Stability:** The staking system exhibits negative feedback—higher staking dilutes staking_apr, reducing staking incentives. This creates a self-correcting mechanism that stabilizes the staking ratio around equilibrium.

### 5.2 Fee Market Equilibrium

When utilization equals the target rate:

```
gas_consumed_eq = TARGET_GAS_RATE → excess_gas_eq = 0 → gas_price_eq = MIN_GAS_PRICE
```

At equilibrium, gas_price equals MIN_GAS_PRICE. Deviations trigger the exponential adjustment mechanism, which rapidly corrects congestion-induced price spikes and gradually returns prices to baseline during low demand.

**Stability:** The fee market is stable for reasonable parameter choices. The exponential mechanism provides strong negative feedback—higher fees reduce demand, lowering utilization and prices.

### 5.3 Supply Equilibrium

**Long-term Behavior:**
As total_supply approaches MAX_SUPPLY:

```
lim(total_supply → MAX_SUPPLY) issuance_rate = 0
```

Issuance naturally ceases, and the system becomes purely deflationary. At this point:
- d(total_supply)/dt = 0 (no new supply)
- d(cumulative_burned)/dt = fee_burn_rate + l1_fee_burn_rate > 0 (continued burning)

**Net Inflation Crossover:**
The transition from inflationary to deflationary occurs when:

```
issuance_rate = fee_burn_rate + l1_fee_burn_rate
```

At current rates (issuance_rate ≈ 26,555 AVAX/day, fee_burn_rate + l1_fee_burn_rate ≈ 810 AVAX/day), this requires approximately 33× increase in fee activity or equivalent issuance reduction.

### 5.4 System-Wide Stability

The coupled system exhibits several stabilizing properties:

1. **Bounded State Variables:** Supply caps, stake limits, and exponential mechanisms ensure all variables remain bounded.

2. **Negative Feedback Dominance:** The primary loops (staking-APR, fee-demand) are balancing, providing natural correction mechanisms.

3. **Governance Hysteresis:** Rate limits on parameter changes prevent rapid oscillations that could destabilize interconnected subsystems.

4. **Conservation Laws:** Token conservation (circulating_supply + total_staked + locked_supply ≤ total_supply) and stake accounting (total_staked = validator_staked + delegator_staked) provide consistency constraints.

---

## 6. Performance Indicators and Metrics

### 6.1 Security Metrics

| Indicator | Description | Target |
|-----------|-------------|--------|
| network_security_ratio | total_staked / circulating_supply | 50-60% |
| validator_decentralization | HHI of stake distribution | Lower is better |
| delegation_efficiency | delegator_staked / total_staked | ~75% |

### 6.2 Economic Health Metrics

| Indicator | Description | Current |
|-----------|-------------|---------|
| token_velocity | transaction_volume / circulating_supply | Activity measure |
| burn_rate_sustainability | (fee_burn_rate + l1_fee_burn_rate) / issuance_rate | ~3% |
| l1_economic_viability | Fee coverage ratio | Per-L1 |

### 6.3 Stability Metrics

| Indicator | Description | Interpretation |
|-----------|-------------|----------------|
| staking_ratio_stability | Variance of total_staked / circulating_supply | Lower is better |
| fee_market_efficiency | Correlation(network_utilization, gas_price) | Higher is better |
| apr_consistency | Variance of staking_apr | Lower is better |

### 6.4 Growth Metrics

| Indicator | Description | Trend |
|-----------|-------------|-------|
| l1_adoption_rate | d(l1_count)/dt | Positive growth |
| utilization_growth | d(network_utilization)/dt | Positive growth |
| validator_economics | Profitability margin | Sustainable |

---

## 7. Insights into the Avalanche Economy

### 7.1 Security

The regulatory subsystem (validators and delegators) is subsidized by network inflation and incentivized for good behavior through reward mechanisms. This creates a wealth-gaining economic force for valid transactions and wealth-reducing force proportional to faults, aligning incentives with network health.

Due to the entanglement of stakeholder behaviors, the regulatory subsystem should be managed as a "policy space" with higher-level parameters affecting the subsystem collectively. This approach enables more efficient modeling and control of network security dynamics.

### 7.2 Sustainability

The governing mechanisms have several control levers including parameter changes, upgrade implementations, and economic policy adjustments. Clear visibility into how governance choices impact the network is critical, especially given the cascading effects across subsystems.

Monitoring network parameters through specific KPIs and health metrics enables successful long-term steering. A computational model representing all subsystems and their relationships assists decision-makers in running experiments and scenario analyses.

### 7.3 Value Creation

The L1 ecosystem serves as a proxy for value creation in the platform through the continuous fee mechanism. The system's connection to real-world value flows through L1 utility and adoption, creating intrinsic value that cascades into the network's economic health.

The financial isolation of L1 activity from the Primary Network, combined with the economic alignment through fees, creates strong incentive alignment while maintaining security separation.

### 7.4 Stability

Economic stability requires navigation and control through policies that address both internal dynamics and external forces. The system's power over L1 economics and governance periodicity provides key levers for systemic control.

Treasury management should incorporate buffer mechanisms to absorb volatility, particularly during early network phases. The buffer size should adapt based on network maturity and observed volatility patterns.

---

## 8. Conclusion

The Avalanche economic network represents a sophisticated control system where careful mechanism design achieves multiple objectives simultaneously. The differential specification provides the mathematical foundation necessary for understanding these complex dynamics and enables a scientific approach to network governance and optimization.

The control-theoretic framework establishes rigorous foundations for analyzing system stability, controllability, and robustness. This approach enables evidence-based governance decisions and provides tools for maintaining economic health as the network evolves.

The journey from theoretical foundations through systems engineering to this differential specification provides a complete toolkit for understanding and governing complex blockchain economic systems in the Web3 era.

---

## References

[1] Ogata, K. (2010). Modern Control Engineering. Prentice Hall.

[2] Khalil, H. K. (2002). Nonlinear Systems. Prentice Hall.

[3] Avalanche Community Proposals. ACP-103: Dynamic Fees. https://github.com/avalanche-foundation/ACPs

[4] Avalanche Community Proposals. ACP-77: Reinventing Subnets. https://github.com/avalanche-foundation/ACPs

[5] Chen, C. T. (1999). Linear System Theory and Design. Oxford University Press.

[6] Narendra, K. S., & Annaswamy, A. M. (2012). Stable Adaptive Systems. Dover Publications.

[7] Astrom, K. J., & Murray, R. M. (2021). Feedback Systems: An Introduction for Scientists and Engineers. Princeton University Press.

[8] Sontag, E. D. (2013). Mathematical Control Theory: Deterministic Finite Dimensional Systems. Springer.

[9] Boyd, S., & Vandenberghe, L. (2004). Convex Optimization. Cambridge University Press.

[10] Bemporad, A., & Morari, M. (1999). Control of systems integrating logic, dynamics, and constraints. Automatica, 35(3), 407-427.
