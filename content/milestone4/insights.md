---
title: Research Insights and Future Roadmap
---

**Last Updated:** December 3, 2025
**Draft Stage:** 3rd Draft (Consolidated)

# Avalanche Economic Research: Insights, Recommendations, and Future Roadmap

## Introduction

This document represents the culmination of the Bonding Curve Research Group's (BCRG) comprehensive analysis of the Avalanche blockchain economic system. Over the course of four research milestones, we have systematically deconstructed, analyzed, and formalized the economic mechanisms that govern one of the most sophisticated blockchain platforms in operation today.

The Avalanche network presents a unique case study in blockchain economics. Unlike simpler single-chain systems, Avalanche operates as a heterogeneous multi-chain ecosystem with three primary chains (P-Chain, X-Chain, C-Chain) and a growing constellation of application-specific Layer 1 blockchains (L1s). This architectural complexity creates economic dynamics that cannot be understood through traditional single-variable analysis. Instead, Avalanche requires a systems-theoretic approach that accounts for feedback loops, emergent behaviors, and cross-subsystem interactions.

This document synthesizes the key insights from our research and provides a comprehensive roadmap for future work. Our goal is to transform theoretical understanding into practical tools—specifically, a cadCAD-based simulation framework capable of testing economic hypotheses, informing governance decisions, and monitoring network health in real-time.

**Prerequisite Reading:**

- [Economic Taxonomy](/milestone1/Economic-Taxonomy) — Fundamental economic primitives
- [Mechanism Taxonomy](/milestone1/Mechanism-Taxonomy) — Technical mechanisms underlying economic behaviors
- [Participant Roles Taxonomy](/milestone1/Participant-Roles-Taxonomy) — Stakeholder types and incentives
- [Systems Engineering Perspective](/milestone2/Avalanche-Economic-Model-A-Systems-Engineering-Perspective) — MBSE framework and five-pillar decomposition
- [Differential Specification](/milestone3/Differential_Specification) — Mathematical equations for simulation
- [Mission Elements Need Statement (MENS)](/milestone4/MENS) — Stakeholder concerns and system needs
- [Economic Hypotheses](/milestone4/economic_hypotheses) — Testable predictions

---

## Executive Summary

### Research Journey

The BCRG Avalanche Economic Research Project represents a systematic effort to understand blockchain economics through the lens of complex adaptive systems theory. Our approach recognizes that blockchain economies are living systems—constantly evolving through governance changes, market dynamics, and emergent participant behaviors.

**Milestone 1** established a rigorous vocabulary for discussing Avalanche economics by cataloging every economic primitive, mechanism, and participant type. The Economic Taxonomy identified five fundamental domains: Token Issuance, Staking Economics, Fee Structure, L1 Economics, and Governance.

**Milestone 2** applied Model-Based Systems Engineering (MBSE) principles to decompose the Avalanche economy into five interacting subsystems: Staking Dynamics, Token Supply, Fee Dynamics, L1 Ecosystem, and Governance. The critical insight was that these subsystems are deeply interconnected—changing any single parameter ripples through multiple subsystems.

**Milestone 3** translated our qualitative systems model into quantitative differential equations. Each subsystem was specified as state variables (quantities that persist), flow variables (rates of change), and parameters (protocol constants). The fundamental equation governing monetary dynamics is: net supply change equals minting rate minus burn rate.

**Milestone 4** used our formalized model to generate testable hypotheses ranging from straightforward predictions to complex emergent effects, providing the research agenda for future empirical work.

### Critical Findings

| Finding | Implication | Priority |
|---------|-------------|----------|
| **Net inflation ~3.76% annually** | Burn rate tripled in 2025 (~1,500 AVAX/day) but still lags issuance (~49,000 AVAX/day). Achieving deflation requires ~33× current activity. | Monitor |
| **Validator decline 40.5% in Q3 2025** | Primary Network validators dropped from 1,436 to 855—the most significant decline in history. Root causes unclear but may relate to ACP-77 migration, opportunity costs, or profitability. | Investigate |
| **ACP-77 reduced L1 costs 99.9%** | Entry cost dropped from approx. \$70,000 stake to approx. \$53/month continuous fee, democratizing L1 creation and enabling economic experimentation at new scales. | Opportunity |
| **Staking ratio dropped from 48% to 41%** | ~32.5M AVAX exited staking in Q3 2025. Below 40% may impact security assumptions. Optimal range is 50-60%. | Concern |
| **TVL grew 41.6% to \$2.2B** | DeFi activity remains strong despite infrastructure stress, indicating healthy user demand. | Positive |

### Understanding These Findings

These findings paint a picture of an ecosystem in transition. ACP-77 (Etna upgrade, December 2024) fundamentally changed the economic calculus for L1 validators. Previously, L1 operators had to stake 2,000 AVAX on the Primary Network. Post-ACP-77, this requirement was removed—validators can operate L1s through continuous fee payments instead.

This architectural change appears to have triggered a migration effect: validators who were only staking to enable L1 validation may be exiting now that this requirement is removed. If correct, the validator decline represents a one-time adjustment rather than ongoing deterioration. However, this hypothesis requires empirical testing through simulation.

The staking ratio decline is particularly noteworthy because Avalanche's security model depends on substantial token staking. As the ratio declines, the economic cost of attack potentially decreases. Our research suggests optimal staking is 50-60%, meaning current 41% may be suboptimal.

### Recommended Path Forward

**Phase 1 (0-3 months):** Build cadCAD simulation framework and establish real-time monitoring to enable quantitative analysis of the validator decline.

**Phase 2 (3-6 months):** Begin systematic hypothesis testing, prioritizing staking dynamics (H2 series) and L1 economics (H3 series) to address concerning trends.

**Phase 3 (6-12 months):** Develop governance decision support tools allowing the community to evaluate proposed ACPs through simulation before implementation.

**Phase 4 (12+ months):** Create a "digital twin" of the Avalanche economy—a continuously calibrated simulation model for governance, monitoring, and education.

---

## 1. Key Research Insights

### 1.1 Subsystem Interdependence

Perhaps the most significant finding is that **Avalanche's economic behavior emerges from subsystem interactions**, not from isolated mechanisms. Traditional blockchain analysis examines mechanisms in isolation, but this misses the crucial interconnections that determine actual behavior. Changing any single parameter ripples through multiple subsystems with second-order and third-order effects.

Our five-pillar decomposition reveals these subsystems are connected through multiple channels. The Staking Dynamics subsystem connects to Token Supply through reward issuance (~49,000 AVAX/day). Fee Dynamics connects to Token Supply through fee burning (~1,500 AVAX/day). The L1 Ecosystem connects to Token Supply through continuous validator fees (~2,100 AVAX/month) and to Staking Dynamics through the now-removed Primary Network validation requirement. Governance affects all subsystems through parameter adjustments via ACPs.

**Key Coupling Channels:**

| Source | Target | Mechanism | Magnitude |
|--------|--------|-----------|-----------|
| Staking | Token Supply | Reward minting | approx. 49,000 AVAX/day (approx. \$1.7M) |
| Fees | Token Supply | Fee burning | approx. 1,500 AVAX/day (approx. \$53K) |
| L1 Ecosystem | Token Supply | Validator fee burns | approx. 2,100 AVAX/month (approx. \$74K) |
| L1 Ecosystem | Staking | Pre-ACP-77 stake requirement | Transitional |
| Governance | All | Parameter modifications | Variable |

**Modeling Implications:** A model that treats subsystems independently will systematically mis-predict behavior. For example, projecting burn rates based on transaction growth alone misses the feedback loop where increased burning leads to increased scarcity, which affects token value, which modifies transaction costs and user behavior. Our cadCAD implementation must explicitly encode these coupling channels.

### 1.2 The Inflation-Deflation Tension

Avalanche does not have a predetermined monetary policy like Bitcoin's fixed supply schedule. Instead, Avalanche's monetary policy is **emergent**—arising from the interaction between inflationary forces (staking rewards) and deflationary forces (fee burning).

The fundamental equation is simple: net supply change equals minting rate minus burn rate. Currently, for every AVAX burned, approximately 31 AVAX are minted. This ratio must invert before Avalanche becomes deflationary.

**Current State (November 2025):**

| Metric | Daily Rate | Annual Rate | % of Supply |
|--------|------------|-------------|-------------|
| Gross Inflation (minting) | ~49,000 AVAX | ~17.9M AVAX | ~3.88% |
| Transaction Fee Burns | ~1,500 AVAX | ~547K AVAX | ~0.12% |
| L1 Validator Fee Burns | ~70 AVAX | ~25.5K AVAX | ~0.006% |
| **Total Burns** | **~1,570 AVAX** | **~573K AVAX** | **~0.126%** |
| **Net Inflation** | **~47,430 AVAX** | **~17.3M AVAX** | **~3.76%** |

The trend is encouraging—burn rates **tripled during 2025** from ~500 to ~1,500 AVAX/day, reflecting growing network adoption. However, achieving deflationary equilibrium requires approximately **33× current transaction volume**, though this estimate doesn't account for dynamic reward rates, non-linear fee mechanics, or L1 growth as an additional burn source.

**Stakeholder Implications:**

- **Token Holders:** 3.76% annual dilution unless staking
- **Stakers:** 7.65-8.5% APR more than offsets inflation
- **Non-Staking Users:** Full inflation impact without offsetting rewards
- **Developers:** Inflationary environment subsidizes security, enabling lower fees

These implications connect to stakeholder concerns identified in the [MENS](/milestone4/MENS): validators face *fee revenue exclusion* (no direct benefit from usage growth), while token holders contend with *undefined sustainability equilibrium* (unclear long-term balance between issuance and burning).

### 1.3 Validator Economics Under Pressure

The Q3 2025 data reveals the most significant validator decline in Avalanche's history:

| Metric | Q2 2025 | Q3 2025 | Change |
|--------|---------|---------|--------|
| Primary Network Validators | 1,436 | 855 | -40.5% |
| Total Staked AVAX | 221.7M | 189.2M | -14.7% |
| Staking Ratio | ~48% | ~41% | -7pp |

**Four Hypotheses for the Decline:**

**Hypothesis A (ACP-77 Migration):** Validators who were staking only to enable L1 validation can now exit since ACP-77 removed this requirement. This predicts a one-time step-function decline followed by stabilization. The timing (~9 months after Etna) is consistent with stake unlock periods.

**Hypothesis B (Opportunity Cost Pressure):** External yields have increased during 2025. Avalanche's 7.65-8.5% APR may now be below some validators' opportunity cost thresholds. This predicts ongoing decline until yields normalize.

**Hypothesis C (Operational Profitability):** Rising infrastructure costs or increased competition may have pushed marginal validators below profitability. This predicts smaller validators exit first.

**Hypothesis D (Market Sentiment Cascade):** Pessimism about AVAX price trajectory reduces expected reward value, triggering exits that reinforce negative sentiment. This predicts correlation with price movements.

**Why This Matters:** Fewer validators means more concentrated validation power. While 855 validators is substantial, continued decline threatens decentralization. If large validators remain while small ones exit, stake concentration increases. Our immediate research priority is using simulation to test these hypotheses.

The validator decline directly relates to MENS-identified concerns around *inflation-dependent yield* (validator returns tied to dilution rather than productive activity) and *L1 revenue isolation* (no participation in L1 revenue despite securing core infrastructure). See [MENS: Primary Network Validator Concerns](/milestone4/MENS#51-primary-network-validator-concerns) for the full analysis of structural tensions affecting validator economics.

### 1.4 L1 Economic Transformation

ACP-77 represents **the most significant economic restructuring since mainnet launch**.

| Aspect | Legacy Model | Modern Model (ACP-77) |
|--------|--------------|----------------------|
| Entry Cost | 2,000 AVAX (approx. \$70,000) | approx. 1.33 AVAX/month (approx. \$53) |
| Cost Type | Capital (one-time, recoverable) | Operating (ongoing, non-recoverable) |
| Primary Network | Must validate | Optional |
| Risk Profile | AVAX price exposure on stake | Fixed monthly cost |

**Economic Implications:**

- **Democratization:** At \$70,000, L1 creation was limited to well-funded teams. At \$53/month, small teams and individual developers can participate.
- **Sustainability Over Speculation:** The legacy model rewarded price speculation; the modern model rewards sustainable value creation.
- **Right-Sizing:** L1s can now dynamically adjust validator counts based on actual needs rather than over-provisioning due to sunk capital.
- **Risk Transfer:** Price risk shifts from operators to the network; operators face operational risk instead.

**Current L1 Ecosystem:**

| Metric | Value |
|--------|-------|
| Total Active L1s | 53 (14 modern, 39 legacy) |
| L1 Validators | ~1,600 |
| Dominant Category | Gaming (35%+) |
| Monthly Fee Burns | ~2,100 AVAX |

The gaming concentration creates both opportunity (proven product-market fit) and risk (exposure to gaming-specific volatility). Diversification into DeFi, enterprise, and social applications would reduce concentration risk.

L1 operators face concerns identified in the [MENS](/milestone4/MENS) around *fee volatility at validator saturation* (exponential fee increases near capacity) and *sovereignty creates liquidity isolation* (L1 native tokens may lack deep markets). The MENS also identifies *no incentive to contribute to Primary Network*—L1 success may not proportionally benefit the security infrastructure L1s depend on. See [MENS: L1 Creator and Operator Concerns](/milestone4/MENS#53-l1-creator-and-operator-concerns).

### 1.5 Dynamic Fee Mechanisms

Avalanche's fee system implements sophisticated control theory principles. The gas price adjustment uses an exponential function responding to congestion: at the minimum (1 nAVAX post-ACP-125), prices stay low during normal operation, but rise exponentially as utilization exceeds targets.

**Why Exponential Adjustment?**

- **Bounded behavior:** Prevents unbounded prices under sustained congestion
- **Symmetry:** Responds equally to under- and over-utilization
- **Smooth response:** More predictable than step-function auctions
- **Equilibrium-seeking:** Naturally drives utilization toward targets

**Multidimensional Resource Pricing:**

Avalanche separately prices different resource types with weights reflecting infrastructure costs: bandwidth (1 gas/byte), reads (1000 gas/read), writes (1000 gas/write), and compute (4 gas/unit). The high weight on reads and writes reflects that state access, not raw computation, is the typical bottleneck.

**Dynamic Gas Limits (ACP-176):**

The Octane upgrade introduced validator signaling for capacity preferences, stake-weighted aggregation to determine targets, and gradual adjustment to prevent destabilization. This enables market-discovered capacity rather than centrally-planned governance votes.

**ACP-125 Impact:** The 96% base fee reduction (25 nAVAX → 1 nAVAX) made simple transfers 25× cheaper, contributing to the 3× burn rate increase during 2025. This natural experiment provides validation data for our models.

---

## 2. Strategic Recommendations

### 2.1 Immediate Priorities (0-3 months)

**R1: Investigate Validator Decline** — CRITICAL

The 40.5% decline requires urgent analysis. We recommend developing a validator economics simulation module, calibrating against Q1-Q3 2025 data, running counterfactual simulations testing each hypothesis, and producing a diagnostic report ranking hypotheses by explanatory power. Success means achieving <15% MAPE on historical validator counts and identifying dominant drivers with evidence. Without analysis, governance operates on speculation.

**R2: Establish Real-Time Monitoring** — HIGH

The Q3 decline was identified retrospectively. We recommend deploying dashboards tracking validator count (<800 warning, <500 critical), staking ratio (<40% warning, <35% critical), burn rate trends, and L1 count trends. Implement automated alerting for threshold breaches and establish daily/weekly/monthly reporting cadence. Target <1 hour data latency with >99% uptime.

**R3: Establish cadCAD Framework Foundation** — HIGH

Our specifications remain theoretical without executable simulation. We recommend initializing a project repository with standard structure, implementing core state variables from all five subsystems, defining parameter spaces for sensitivity analysis, creating baseline policy functions, implementing state update functions encoding differential equations, and validating with conservation law and equilibrium tests. Target >90% test coverage.

### 2.2 Short-Term Goals (3-6 months)

**R4: Execute Priority Hypothesis Testing** — MEDIUM-HIGH

Priority order based on governance relevance:
1. H2-A (Optimal Staking Range): Simulate at 30-70% ratios to identify optimal range
2. H2-B (APR Efficiency): Simulate at 5-10% APR to find minimum sustainable level
3. H3-A (Continuous Fee Efficiency): Project L1 validator economics for sustainability assessment
4. H1-B (Deflation Threshold): Project burn rates at 5×-50× activity
5. H5-D (Base Fee Impact): Compare predictions to post-ACP-125 data for model validation

Target at least 5 hypotheses tested with documented results and statistical confidence levels.

**R5: Model L1 Ecosystem Growth** — MEDIUM

Model legacy-to-modern migration based on cost differentials, simulate category diversification scenarios, analyze cross-chain value flows, and project L1 count trajectories under baseline, optimistic, and pessimistic scenarios.

### 2.3 Medium-Term Objectives (6-12 months)

**R6: Develop Governance Decision Support** — MEDIUM

Create an ACP Impact Simulator (input proposed changes, output projected effects), Parameter Optimization Interface (define objectives, search for optimal configurations), Risk Scenario Analyzer (define stress scenarios, simulate behavior, identify vulnerabilities), and Historical ACP Analysis (compare predicted vs. actual outcomes). Target at least one ACP evaluated using simulation prior to implementation.

This recommendation directly addresses MENS-identified governance concerns: *slow parameter adaptation* (economic parameters change only through multi-week governance cycles) and *absence of real-time economic levers* (no mechanisms for continuous, market-driven adjustment). See [MENS: Governance Concerns](/milestone4/MENS#57-governance-concerns).

**R7: Build Agent-Based Model Extensions** — MEDIUM

Extend beyond differential equations to capture strategic interactions: multi-role agent framework (validators, delegators, developers, users), strategic interaction modeling, coalition dynamics, and emergent behavior analysis.

### 2.4 Long-Term Vision (12+ months)

**R8: Establish Digital Twin** — STRATEGIC

Create a continuously updated simulation that mirrors real network state with real-time data integration, continuous calibration using Bayesian methods with drift detection, predictive analytics for short/medium/long-term projections, and decision support integration with governance dashboards. Target <15% MAPE over rolling 90-day windows.

---

## 3. Future Research Roadmap

### Phase 1: Foundation (Months 1-3)

**Objective:** Establish technical infrastructure for all subsequent research.

**Weeks 1-4 (cadCAD Setup):** Create the project repository with standard structure, implement state variable classes for each subsystem, define parameter schema with defaults and ranges, write initial policy functions encoding stakeholder decision logic, and set up continuous integration. cadCAD separates state variables, parameters, policies, and state update functions—this separation makes models maintainable and experiments reproducible.

**Weeks 5-8 (Data Pipeline):** Implement P-Chain queries for validator information, C-Chain queries for transaction data, L1 metrics aggregation, and compile historical datasets for calibration going back to Q1 2024. Data collection must handle rate limiting, network errors, and schema changes gracefully.

**Weeks 9-12 (Model Calibration):** Fit behavioral parameters using historical data (e.g., estimate staking sensitivity by matching historical staking ratio changes to APR changes), validate conservation laws hold, test equilibrium conditions, and document methodology for reproducibility.

**Deliverables:** cadCAD repository with documentation, automated data collection scripts, calibrated baseline model achieving <20% MAPE, technical documentation.

### Phase 2: Experimentation (Months 4-6)

**Objective:** Conduct systematic experiments to test hypotheses and generate insights.

**Experiment Set 1 (Staking Dynamics):** APR sensitivity analysis (5-12% range), minimum stake threshold effects (500-5,000 AVAX), duration-based reward optimization, and validator profitability scenarios under varying costs and yields.

**Experiment Set 2 (Fee Dynamics):** Resource weight recalibration testing, dynamic gas limit convergence under demand scenarios, base fee floor optimization, and congestion response patterns under demand spikes.

**Experiment Set 3 (L1 Economics):** Continuous fee sustainability analysis, legacy-to-modern migration modeling, category diversification effects, and cross-chain value capture mechanisms.

**Deliverables:** Experiment design documents, simulation results database, statistical analysis reports with confidence intervals, parameter sensitivity maps.

### Phase 3: Validation (Months 7-9)

**Objective:** Establish confidence in model accuracy and methodology rigor.

**Verification** confirms the model is implemented correctly: unit testing of individual functions, integration testing of subsystem coupling, conservation law enforcement, and boundary condition handling.

**Validation** confirms the model matches reality: back-testing against historical data from 2024-2025, ACP impact comparison (predicted vs. actual for Etna, Octane, Granite), cross-validation with independent sources (Messari, DefiLlama), and uncertainty quantification through Monte Carlo simulation.

**External Review:** Peer review by qualified researchers (BlockScience, Token Engineering Commons, academia), community feedback integration, expert consultation on specific components, and documentation refinement.

**Deliverables:** Verification test suite with >90% coverage, validation reports with MAPE <15%, peer review responses, final methodology documentation.

### Phase 4: Deployment (Months 10-12)

**Objective:** Deliver operational tools creating ongoing value.

**Decision Support Tools:** Parameter optimization interface for exploring configurations, ACP impact simulator for pre-implementation analysis, risk scenario dashboard for stress testing, and governance recommendation engine.

**Continuous Monitoring:** Real-time calibration with automatic parameter updates, anomaly detection alerting when behavior diverges from predictions, automated trend analysis reports, and composite health index for quick assessment.

**Knowledge Transfer:** Training materials (tutorials, videos, exercises), comprehensive user documentation, live workshop sessions, and open-source release under permissive license.

**Deliverables:** Production tools deployed and operational, monitoring dashboards with <1 hour latency, training curriculum enabling self-learning, public GitHub repository with community engagement.

---

## 4. cadCAD Implementation Framework

### 4.1 Framework Overview

cadCAD (Complex Adaptive Dynamics Computer-Aided Design) is an open-source Python library developed by BlockScience for simulating complex systems, particularly token economies. It has been used to model Ethereum's transition to Proof-of-Stake, various DeFi protocols, and numerous blockchain tokenomics systems.

The choice of cadCAD is deliberate: it separates concerns (state, parameters, policies, mechanisms), supports Monte Carlo simulation for uncertainty quantification, and has a growing ecosystem of tools and practitioners. These patterns will enable collaboration with the broader token engineering community.

### 4.2 Core Concepts

**State Variables** are quantities that persist and evolve over time—total_staked, validator_count, gas_price, etc. They define what we're tracking.

**Parameters** are fixed values within a simulation run that control behavior—protocol parameters like MIN_GAS_PRICE and behavioral parameters like STAKING_SENSITIVITY. Parameters vary between runs but not within a run.

**Policies** are functions that take current state and parameters and produce signals representing stakeholder decision-making. For example, a staking policy calculates how much stake flows in based on current APR relative to opportunity cost.

**State Update Functions (SUFs)** take policy outputs and update state variables, implementing the differential equations governing system evolution.

**Partial State Update Blocks (PSUBs)** group policies and SUFs that execute together within a timestep, defining execution order.

### 4.3 Project Architecture

The recommended structure organizes code by function: core simulation code in model/ with subdirectories for state update functions (parts/), decision logic (policies/), and reusable calculations (mechanisms/); data assets in data/ with historical, snapshot, and calibration subdirectories; experiment configurations in experiments/; test suites in tests/ organized by type (unit, integration, validation); interactive notebooks in notebooks/; and documentation in docs/.

### 4.4 State Variables by Subsystem

**Staking Dynamics:** total_staked (189.2M AVAX currently), validator_staked (~80% of total), delegator_staked (~20%), staking_apr (8%), validator_count (855).

**Token Supply:** total_supply (460.6M AVAX), circulating_supply (429M), locked_supply (31.6M), cumulative_burned (4.8M), issuance_rate (49,000 AVAX/day).

**Fee Dynamics:** gas_price (1 nAVAX minimum), excess_gas (accumulated above target), gas_consumed (current rate), fee_burn_rate (1,500 AVAX/day), network_utilization (ratio to target).

**L1 Ecosystem:** l1_count (53 active), l1_validator_count (~1,600), l1_fee_burn_rate (~2,100 AVAX/month).

**Governance:** proposed_acp_count (~15 active), implementable_acp_count (5), activated_acp_count (88 historical), stale_acp_count (12).

Conservation laws must hold: circulating + staked + locked ≤ total_supply, and validator_staked + delegator_staked = total_staked.

### 4.5 Policy Functions

**Staking Decision Policy:** Models aggregate staking behavior based on APR relative to opportunity cost. When APR exceeds opportunity cost, tokens flow into staking; when below, tokens flow out. The response uses a bounded sigmoid function to prevent unrealistic extremes. Key parameters are staking sensitivity (base rate of flow), opportunity cost (external yield benchmark), and response scale (curve steepness).

**Validator Entry/Exit Policy:** Models validator population dynamics based on profitability. Validators enter when per-validator profit exceeds entry thresholds and exit when profit falls below exit thresholds. There's hysteresis—exit threshold is lower than entry threshold due to sunk costs. Key parameters are operational cost (monthly expense to run a validator), entry/exit thresholds, and base entry/exit rates.

### 4.6 State Update Functions

**Total Staked Update:** Implements the equation: change in total staked = staking inflow - unstaking outflow + restaked rewards. The restaking term captures validators who compound rewards rather than withdrawing.

**Validator Count Update:** Implements: change in validators = entry rate - exit rate. Since validator count is discrete, fractional changes are accumulated and applied when exceeding 1.

**Staking APR Update:** Computed from reward rate and stake distribution: annual rewards = daily issuance × 365; APR = annual rewards / total staked, adjusted for duration multipliers.

---

## 5. Experiment Design Methodology

### 5.1 The Scientific Method for Token Economics

Token economic modeling is fundamentally empirical science. The ultimate test of any model is whether it predicts real-world behavior. Our methodology follows the scientific method adapted for simulation-based research.

**Step 1 (Hypothesis Formulation):** Every experiment starts with a clear hypothesis from our Economic Hypotheses document, specific enough to generate testable quantitative predictions.

**Step 2 (Parameter Space Definition):** Identify control variables (what to vary) and response variables (what to measure). Ranges should span realistic values including current actuals.

**Step 3 (Scenario Specification):** Define baseline (current conditions), optimistic (favorable external conditions), and pessimistic (adverse conditions) scenarios to ensure robust results.

**Step 4 (Simulation Execution):** Run Monte Carlo simulations (100-1000 runs per combination) to account for stochastic variation. Store results in structured database.

**Step 5 (Statistical Analysis):** Apply appropriate tests—confidence intervals, sensitivity analysis, hypothesis testing—to distinguish signal from noise.

**Step 6 (Interpretation & Reporting):** Document findings with clear statements of conclusions, confidence levels, and limitations, accessible to non-statisticians.

### 5.2 Priority Experiments

**E1: Validator Decline Investigation**

Objective: Determine root causes of Q3 2025 validator decline. Tests Hypothesis H2-B (APR Efficiency Threshold). Control parameters: staking APR (5-12%), operational cost (\$500-2000/month), opportunity cost (3-8%). Response variables: validator count equilibrium, time to equilibrium, net stake change, profitability distribution. Expected outcome: Identify critical APR threshold below which exits accelerate. If near current APR (~8%), profitability is primary driver; if exits continue at high APR, ACP-77 migration hypothesis gains support.

**E2: Burn Rate Sustainability**

Objective: Quantify activity level for deflationary equilibrium. Tests Hypothesis H1-B (Deflation Threshold). Control parameters: transaction volume (1×-50× current), average gas price (1-100 nAVAX), L1 validator count (1,600-20,000). Response variables: daily burn rate, net inflation rate, time to supply cap, burn/issuance ratio. Expected outcome: Approximately 30-40× current activity needed for net deflation; L1 growth provides additional burn source that could reduce threshold.

**E3: L1 Migration Dynamics**

Objective: Model legacy-to-modern L1 migration trajectory. Tests Hypothesis H3-D (Migration Trajectory). Control parameters: legacy cost (\$70,000 fixed), modern cost (\$50-200/month), migration friction (0-1). Response variables: migration rate, ecosystem composition over time, total L1 fee burns, net cost to operators. Expected outcome: Migration accelerates as modern L1s demonstrate cost advantages; high friction may slow transition; results inform whether additional incentives are needed.

---

## 6. Data Collection Infrastructure

### 6.1 Data Sources

| Source | Data Type | Frequency | Role |
|--------|-----------|-----------|------|
| P-Chain RPC | Validators, stakes, delegations | Real-time | Staking subsystem calibration |
| C-Chain RPC | Transactions, gas, burns | Real-time | Fee dynamics calibration |
| Avascan API | Aggregated metrics | Daily | Cross-validation |
| DefiLlama API | TVL, protocol data | Hourly | DeFi activity metrics |
| Messari API | Market data, reports | Daily | External context |
| L1 RPCs | L1-specific metrics | Variable | L1 ecosystem calibration |

Using multiple sources provides redundancy (if one fails, others fill gaps), cross-validation (discrepancies reveal quality issues), complete coverage (no single source has everything), and independence (reduces single-provider bias).

### 6.2 Pipeline Architecture

The pipeline follows standard ETL patterns. The **Extraction Layer** handles rate limiting, error handling with retries and fallbacks, and deduplication. The **Transformation Layer** performs schema validation, unit conversion (e.g., wei to AVAX), and aggregation (block-level to daily). The **Storage Layer** uses time-series databases for metric tracking, snapshot stores for complete state at specific points, and cache layers for query acceleration. The **Analysis Layer** provides cadCAD integration for calibration data, dashboards for real-time visibility, and alerting for significant changes.

### 6.3 Key Metrics

**Real-Time (Block-by-Block):** Staking ratio (security monitoring), burn rate (activity indicator), gas price (fee market health), network utilization (capacity planning).

**Daily Aggregates (3-year retention):** Net inflation (monetary policy), validator count (decentralization), L1 activity (ecosystem growth), TVL by protocol (DeFi health).

---

## 7. Hypothesis Testing Framework

### 7.1 Statistical Methodology

| Hypothesis Type | Statistical Test | When to Use |
|-----------------|------------------|-------------|
| Equilibrium existence | Stationarity tests (ADF) | Testing convergence to stable values |
| Parameter sensitivity | Sobol indices | Identifying which parameters most affect outcomes |
| Threshold identification | Change point detection | Finding critical values where behavior changes |
| Trend analysis | Mann-Kendall test | Detecting gradual changes over time |
| Causal relationships | Granger causality | Testing whether one variable predicts another |
| Distribution comparison | Kolmogorov-Smirnov | Comparing simulation outputs to real distributions |

### 7.2 Hypothesis-Test Mapping

| Hypothesis | Test Approach | Data Required | Output |
|------------|---------------|---------------|--------|
| H1-A (Self-Reinforcing Value) | Granger causality | Price, burn rate, activity | Does burning cause price increase? |
| H1-B (Deflation Threshold) | Monte Carlo simulation | Burn, issuance projections | Activity multiplier for deflation |
| H2-A (Optimal Staking Range) | Equilibrium analysis | Historical staking data | Optimal staking ratio range |
| H2-B (APR Efficiency) | Sensitivity analysis | Validator entry/exit | Minimum sustainable APR |
| H3-A (Continuous Fee Efficiency) | Comparative analysis | Legacy vs modern L1 data | Cost-effectiveness comparison |
| H5-D (Base Fee Impact) | Before/after comparison | Pre/post ACP-125 data | Model validation |

### 7.3 Acceptance Criteria

**Model Validation:**
- MAPE < 15% (predictions within 15% of actuals)
- Directional accuracy > 70% (correctly predicts direction 70%+ of the time)
- Conservation law violation = 0% (token accounting always exact)
- Equilibrium stability (converges within 1000 steps)

**Hypothesis Acceptance:**
A hypothesis is "supported" if: statistical test rejects null at specified confidence level; effect size is practically (not just statistically) significant; results are robust across multiple scenarios; and results are consistent with independent validation data.

---

## 8. Verification and Validation

### 8.1 Verification Framework

**Verification** asks "Did we build the model right?" (Is the code correct?)

**Unit Verification** tests individual functions in isolation, ensuring each policy function and state update function behaves correctly for known inputs.

**Integration Verification** tests subsystem interactions, ensuring information flows correctly through coupling channels—for example, that staking rewards properly flow into token supply.

**Conservation Law Tests** verify tokens cannot appear or disappear except through defined minting and burning mechanisms.

**Boundary Condition Tests** verify the model handles extreme inputs gracefully—zero validators, 100% staking ratio, gas price at minimum.

### 8.2 Validation Framework

**Validation** asks "Did we build the right model?" (Does it match reality?)

**Historical Back-Testing** compares predictions to actual outcomes across multiple periods: 2024 Q1-Q2 (pre-Etna baseline), 2024 Q3-Q4 (Etna activation), 2025 Q1-Q2 (post-Etna L1 growth), 2025 Q3 (Octane/Granite effects).

**Cross-Validation Protocol:** Train on 80% of historical data, validate on 20% holdout, test on real-time data post-deployment, recalibrate quarterly.

### 8.3 Continuous Validation

Once deployed, the model must maintain accuracy as the network evolves. Real-time data feeds into model predictions, which are compared to actual states. Accuracy metrics are computed and checked against thresholds. If MAPE exceeds 15% over a 7-day rolling window, an alert triggers automatic recalibration. This ensures the model remains accurate even as conditions change.

---

## 9. Risk Assessment

### 9.1 Model Risks

| Risk | Likelihood | Impact | Mitigation |
|------|------------|--------|------------|
| Parameter mis-specification | Medium | High | Sensitivity analysis; regular recalibration |
| Structural model error | Low | Critical | Multiple modeling approaches; empirical validation |
| Data quality issues | Medium | Medium | Validation checks; multiple sources |
| Black swan events | Low | Critical | Stress testing; scenario analysis |

### 9.2 Protocol Risks Identified

| Risk | Status | Why It Matters | Monitoring |
|------|--------|----------------|------------|
| Validator centralization | Moderate (855 validators) | Concentrated power, single points of failure | Nakamoto coefficient |
| Staking ratio decline | Active (41%, down from 48%) | Reduced economic security | Weekly trend |
| L1 category concentration | Moderate (35%+ gaming) | Sector-specific vulnerability | Diversity index |
| Burn rate insufficient | Active (3% of issuance) | Continued inflation | Burn ratio trend |

### 9.3 Alert Thresholds

**Critical (Immediate Action):** Validator count <500, staking ratio <35%, net inflation >5%, single L1 category >50%.

**Warning (Investigation Required):** Validator count <800, staking ratio <40%, declining burn ratio trend, APR <6%.

---

## 10. Success Metrics and KPIs

### 10.1 Model Performance

| KPI | Target | Frequency |
|-----|--------|-----------|
| Prediction Accuracy (MAPE) | < 15% | Weekly |
| Model Uptime | > 99% | Continuous |
| Data Freshness | < 1 hour | Continuous |
| Calibration Drift | < 10% | Monthly |

### 10.2 Research Impact

| KPI | Target | Rationale |
|-----|--------|-----------|
| Hypotheses Tested | 20+ cumulative | Systematic question-answering |
| Governance Recommendations Adopted | 3+ annual | Real decision influence |
| Open-Source Contributions | 10+ cumulative | Community benefit |
| Publications/Presentations | 4+ annual | Peer review and sharing |

### 10.3 Ecosystem Health

| KPI | Target | Current | Status | Action if Below |
|-----|--------|---------|--------|-----------------|
| Staking Ratio | 50-60% | 41% | Below | Investigate; consider APR adjustments |
| Net Inflation | < 3% | 3.76% | Improving | Monitor burn rate growth |
| Validator Count | > 1,000 | 855 | Below | Analyze profitability; consider incentives |
| L1 Count | Growing | 53 | On Track | Continue monitoring |
| Burn/Issuance Ratio | > 50% | 3% | Needs Growth | Long-term; depends on activity growth |

---

## Conclusion

### What We Have Learned

Over the course of this research program, we have developed a comprehensive understanding of the Avalanche blockchain as an economic system. What began as an effort to catalog and classify economic mechanisms evolved into something more profound: a recognition that Avalanche's economy cannot be understood through reductionist analysis of individual components, but must instead be approached as an integrated system where behavior emerges from the interactions between subsystems.

The most important insight from our work is that Avalanche operates as a complex adaptive system. The five subsystems we identified—Staking Dynamics, Token Supply, Fee Dynamics, L1 Ecosystem, and Governance—are not independent modules that can be analyzed in isolation. They are deeply interconnected through feedback loops that amplify, dampen, and transform economic signals in ways that cannot be predicted from examining any single subsystem alone. When validators exit the network, this affects not only staking dynamics but also token supply (through reduced reward distribution), fee dynamics (through changed network capacity), the L1 ecosystem (through validator availability), and governance (through shifted voting power). These cascading effects mean that any intervention—whether a parameter change, a protocol upgrade, or an external market shock—will ripple through the entire system.

This systems perspective has practical implications. Traditional economic analysis might ask "what is the optimal staking APR?" and attempt to answer it by examining staking behavior in isolation. Our framework reveals that the answer depends on the state of all other subsystems: the current inflation rate, fee burning activity, L1 growth trajectory, and governance responsiveness. There is no single optimal APR—there are only configurations that achieve particular balances across multiple competing objectives under specific conditions.

### The Current State of the Avalanche Economy

Our research coincides with a pivotal moment in Avalanche's evolution. The Etna upgrade of December 2024 fundamentally restructured the economics of the L1 ecosystem, reducing entry costs by 99.9% and decoupling L1 validation from Primary Network validation. This architectural change has set in motion a transition whose ultimate outcome remains uncertain.

The data from Q3 2025 reveals both the opportunities and challenges of this transition. On one hand, the L1 ecosystem continues to grow, with 53 active L1s and increasing activity in gaming and other verticals. The fee burning rate has tripled during 2025, indicating growing network adoption. Total Value Locked in DeFi has increased to \$2.2 billion, suggesting healthy demand for Avalanche's application layer.

On the other hand, the Primary Network validator count has declined by 40.5%—the most significant contraction in Avalanche's history. The staking ratio has fallen from 48% to 41%, approaching levels that may affect security assumptions. These infrastructure-level metrics tell a different story than the application-level metrics, suggesting that the ecosystem is experiencing a structural adjustment whose dynamics we do not yet fully understand.

Our research has generated four hypotheses for the validator decline: migration effects from ACP-77, opportunity cost pressures, operational profitability concerns, and market sentiment cascades. These hypotheses are not mutually exclusive, and the truth likely involves some combination of all four. What we lack is the empirical analysis to determine their relative contributions. This is precisely why the simulation framework we have designed is so important—it will allow us to test these hypotheses quantitatively and identify the dominant drivers.

### The Path Forward

The roadmap we have outlined represents a deliberate progression from theoretical understanding to practical capability. Phase 1 establishes the technical foundation: the cadCAD simulation framework, data collection infrastructure, and calibrated baseline model. Without this foundation, all subsequent work would be speculation rather than analysis. Phase 2 uses this foundation to conduct systematic experiments, testing our hypotheses and generating insights that can inform governance decisions. Phase 3 validates our work through rigorous verification and external review, building the credibility needed for our recommendations to influence real decisions. Phase 4 deploys operational tools that create ongoing value for the Avalanche community.

This progression is not merely a project plan—it reflects our philosophy of evidence-based governance. Too often, blockchain governance operates on intuition, ideology, or the persuasive power of particular community members. Our goal is to provide an alternative: a framework for making decisions based on quantitative analysis of likely outcomes. This does not mean that simulation should replace human judgment—models are always simplifications of reality, and there will always be factors that escape formalization. But simulation can discipline our intuitions, reveal unintended consequences, and identify trade-offs that might otherwise remain hidden.

The ultimate vision is what we have termed a "digital twin" of the Avalanche economy: a continuously calibrated simulation that tracks real-time network state and can project future trajectories with quantified uncertainty. Such a system would serve multiple purposes. For governance participants, it would provide a tool for evaluating proposed changes before implementation. For the technical team, it would offer early warning of concerning trends. For the broader community, it would serve as an educational resource that makes complex economic dynamics accessible and understandable.

### Broader Significance

While this research focuses specifically on Avalanche, the methods and insights have broader applicability. Every blockchain faces similar challenges: balancing inflation and deflation, aligning stakeholder incentives, managing the transition from early-stage growth to mature operation. The systems-theoretic approach we have developed—decomposing complex economies into interacting subsystems, formalizing dynamics as differential equations, testing hypotheses through simulation—can be applied to any blockchain economic system.

More fundamentally, our work contributes to the emerging field of token engineering: the discipline of designing, analyzing, and optimizing token-based economic systems. This field is still in its early stages, lacking the established methodologies and accumulated knowledge that characterize mature engineering disciplines. By documenting our approach, sharing our tools, and publishing our findings, we hope to contribute to the development of token engineering as a rigorous practice.

The stakes are significant. Blockchain networks collectively secure hundreds of billions of dollars in value and serve millions of users. Poor economic design can lead to instability, exploitation, or collapse. Good economic design can create sustainable systems that generate value for all participants. The difference often lies in the quality of analysis that informs design decisions. Our work aims to raise that quality—for Avalanche specifically, and for the blockchain ecosystem more broadly.

### Final Thoughts

The Avalanche economic system is remarkable in its sophistication. The multi-chain architecture, the dynamic fee mechanisms, the flexible L1 framework, the governance-driven evolution through ACPs—these represent some of the most advanced economic engineering in the blockchain space. But sophistication creates complexity, and complexity creates the potential for unexpected behavior. Our role as researchers is to make this complexity comprehensible: to build models that capture essential dynamics, to identify risks before they materialize, and to provide tools that enable informed decision-making.

The validator decline of Q3 2025 is a reminder that even well-designed systems can exhibit surprising behavior. The question is not whether surprises will occur—they will—but whether the community has the analytical capabilities to understand and respond to them effectively. Building those capabilities is the purpose of this research program. We have laid the theoretical foundation. The work of building, validating, and deploying operational tools lies ahead. The Avalanche community's engagement with this work will determine whether economic modeling becomes a core competency of Avalanche governance or remains an academic exercise.

We believe the former is both possible and necessary. The tools exist. The methodology is proven. The data is available. What remains is the commitment to invest in analytical capabilities that match the sophistication of the system being analyzed. This document represents our contribution to that effort—a synthesis of what we have learned and a roadmap for what comes next.

---

## References

### Internal Documentation

1. [Economic Taxonomy](/milestone1/Economic-Taxonomy) — Foundational economic concepts
2. [Mechanism Taxonomy](/milestone1/Mechanism-Taxonomy) — Protocol mechanisms
3. [Participant Roles Taxonomy](/milestone1/Participant-Roles-Taxonomy) — Stakeholder analysis
4. [Avalanche Economy relative to the Open Economy](/milestone1/Avalanche-Economy-relative-to-the-Open-Economy) — Macroeconomic framework
5. [ACP Summaries](/milestone2/ACP-Summaries) — Protocol evolution
6. [Systems Engineering Perspective](/milestone2/Avalanche-Economic-Model-A-Systems-Engineering-Perspective) — MBSE approach
7. [Subsystem Analysis and MultiGraph](/milestone2/Subsystem_Analysis_and_MultiGraph) — Technical specification
8. [Differential Specification](/milestone3/Differential_Specification) — Mathematical framework
9. [Mission Elements Need Statement (MENS)](/milestone4/MENS) — Stakeholder concerns and system needs
10. [Economic Hypotheses](/milestone4/economic_hypotheses) — Testable predictions
11. [Data Snapshot](/data/snapshot-2025-11-28) — Current network metrics

### External Sources

12. [cadCAD Masterclass](https://www.cadcad.education/course/masterclass-ethereum) — Economic modeling best practices
13. [BlockScience cadCAD Introduction](https://medium.com/block-science/introducing-complex-adaptive-dynamics-computer-aided-design-cadcad-38b63b541eb8) — Framework philosophy
14. [Formal Verification of Token Economy Models](https://link.springer.com/chapter/10.1007/978-3-030-39459-2_16) — Academic methodology
15. [Blockchain Verification and Validation](https://www.sciencedirect.com/science/article/pii/S1574013722000314) — V&V techniques
16. [Messari State of Avalanche Q3 2025](https://messari.io/report/state-of-avalanche-q3-2025) — Market data
17. [DefiLlama Avalanche](https://defillama.com/chain/avalanche) — TVL tracking

### Avalanche Foundation Resources

18. Avalanche Foundation. *Avalanche Community Proposals*. https://github.com/avalanche-foundation/ACPs
19. Ava Labs. *Avalanche Platform Whitepaper*. https://www.avalabs.org/whitepapers
20. Avalanche. *Network Statistics*. https://stats.avax.network
21. Avascan. *Validator Explorer*. https://avascan.info/validators

---

*Document prepared by the Bonding Curve Research Group (BCRG) as part of the Avalanche Economic Research Project. This document synthesizes four milestones of comprehensive research and provides the roadmap for future development of the Avalanche economic modeling framework.*
