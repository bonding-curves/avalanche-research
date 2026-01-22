---
title: "Phase II Proposal: Parameter Selection Under Uncertainty"
---

# Avalanche Staking Economics: Phase II Proposal

**Project:** Parameter Selection Under Uncertainty for Avalanche Staking

**Team:** Bonding Curve Research Group (BCRG)

**Duration:** 6 Months

**Date:** January 21, 2026

---

## Executive Summary

Following the successful completion of [Phase I](https://bonding-curves.github.io/avalanche-research/)—which delivered foundational taxonomies, systems analysis, and a comprehensive differential specification—this proposal outlines Phase II: a focused investigation of the Avalanche staking subsystem using the Parameter Selection Under Uncertainty (PSUU) methodology.

Phase II will produce **validated, actionable parameter recommendations** for staking incentives, enabling the Avalanche Foundation to make data-driven decisions about validator rewards, staking duration, and yield structures.

Staking economics represents a top priority for the Foundation, with multiple community-initiated ACPs addressing validator and delegation mechanisms. This work delivers the analytical foundation for evidence-based governance decisions for staking, validating, and delegation mechanism parameterization for the Avalanche Network.

**Key deliverables:**
- Calibrated staking model validated against 2024-2025 historical data
- Sensitivity analysis revealing which governance levers most affect staking outcomes
- Parameter recommendation report with decision trees and correlation analysis
- Open source model and knowledge transfer workshops
- Analytic support for ACP development regarding staking incentives and parameterization

---

## Part I: Scope

### Focus: The Staking Subsystem

Phase II narrows scope to the staking subsystem specifically, abstracting away other components of the full differential specification. This focused model will capture:

- Validator staking behavior
- Delegator staking behavior
- Reward mechanics and yield determination
- Duration-dependent incentive structures

Other subsystems (L1 ecosystem dynamics, fee markets) are treated as environmental inputs rather than endogenous components.

### The Core Question

> Under what governance configurations do Avalanche's staking incentives sustain validator and delegator participation across bull markets, bear markets, and competing DeFi yields—while maintaining the security guarantees required by a multi-billion dollar network?

---

## Part II: Methodology

### Parameter Selection Under Uncertainty (PSUU)

PSUU is a computational methodology developed by complex systems engineering firm [Block Science](https://medium.com/block-science/how-to-perform-parameter-selection-under-uncertainty-976931ba7e5d) for selecting robust parameters when system behavior is uncertain. Successfully applied to [Subspace Network tokenomics](https://github.com/BlockScience/subspace), it systematically explores the relationship between governance decisions and system outcomes.

![PSUU Pipeline Overview](./img-psuu-pipeline-overview-white.png)
*Fig 1: The PSUU pipeline—from environmental scenarios through simulation to ML-based parameter recommendations*

### How PSUU Works

**Step 1: Define the Design Space**
- Identify controllable parameters (governance levers)
- Identify environmental scenarios (external uncertainty)
- Define KPIs and success thresholds

**Step 2: Generate Simulations**
- Cartesian product of all parameter combinations
- Multiple Monte Carlo runs per combination
- Result: thousands of simulation trajectories

**Step 3: Aggregate and Analyze**
- Compute KPIs for each trajectory
- Convert KPIs to binary utility outcomes (threshold met / not met)
- Apply machine learning to identify parameter-outcome relationships

**Step 4: Produce Recommendations**
- Decision trees showing parameter importance
- Correlation matrices linking levers to outcomes
- Parameter ranges optimized for single or multiple goals

### Example Output: Decision Tree

![PSUU Decision Tree](./img-psuu-decision-tree.png)
*Fig 2: Decision tree for goal optimization, with feature importance analysis*

### Example Output: Parameter Influence

![PSUU Parameter Influence](./img-psuu-parameter-influence.png)
*Fig 3: Parameter influence on KPIs across simulation results*

---

## Part III: The Design Space

*The following represents an illustrative design space based on preliminary discussions. The actual design space, including specific parameters, ranges, scenarios, and KPIs, will be discovered collaboratively between BCRG and the Avalanche team and validated against real data during Milestone 1.*

### Controllable Parameters (Governance Surface)

These are policy levers the Avalanche Foundation can adjust:

| Parameter | Description | Current | Exploration Range |
|-----------|-------------|---------|-------------------|
| `MIN_STAKE_DURATION` | Minimum lockup period | 2 weeks | 1 week – 3 months |
| `MAX_STAKE_DURATION` | Maximum lockup period | 1 year | 6 months – 2 years |
| `MIN_DURATION_YIELD` | APR for minimum duration | ~6% | 4% – 8% |
| `MAX_DURATION_YIELD` | APR for maximum duration | ~8% | 6% – 12% |
| `CONSUMPTION_RATE_BOUNDS` | Reward distribution parameters | Current | ±20% variations |
| `VALIDATOR_REWARD_SHARE` | Split between validators/delegators | Current | 60% – 90% |

### Environmental Scenarios (External Uncertainty)

Conditions beyond the protocol's control that the system must be robust against:

| Scenario | Description | Values |
|----------|-------------|--------|
| `EXTERNAL_YIELD` | Competing DeFi/TradFi yields | 3%, 5%, 7%, 10% |
| `MARKET_CONDITION` | Crypto market sentiment | Bull, Neutral, Bear |
| `NETWORK_GROWTH` | L1 adoption rate | Low, Medium, High |

**Scenario Groups:**
- **Baseline:** Expected conditions over simulation horizon
- **Sustained Stress:** Prolonged adverse conditions (bear market, high competing yields)
- **Shock Events:** Temporary disruptions (market crash, yield spike)

### Behavioral Dynamics (Response Functions Calibrated from Data)

A key methodological advancement: behavioral parameters should be modeled as **state variables that evolve endogenously**, not fixed constants. Rather than calibrating fixed values, we calibrate the *response functions* that govern how these parameters change based on system conditions.

| Parameter | Phase I Treatment | Phase II Treatment |
|-----------|-------------------|-------------------|
| `STAKE_RATE` | Fixed constant | State variable: f(APR, duration, market) |
| `UNSTAKE_RATE` | Fixed constant | State variable: f(APR spread, opportunity cost) |
| `RESTAKE_RATE` | Fixed constant | State variable: f(compounding incentive, liquidity needs) |

**Calibration approach:**
1. Ingest Avalanche-provided historical data (2024-2025)
2. Fit the *response functions* (f) to observed stake/unstake patterns—these functions define how behavioral parameters evolve during simulation
3. Validate fitted functions against held-out data
4. Apply uncertainty bounds to function parameters for PSUU exploration

### Key Performance Indicators

| KPI | Description | Target Direction |
|-----|-------------|------------------|
| `STAKING_RATIO` | Total staked / circulating supply | Higher is better (security) |
| `VALIDATOR_RATIO` | Validator stake / total stake | Monitor for decentralization |
| `DELEGATOR_RATIO` | Delegator stake / total stake | Monitor for participation |
| `WEIGHTED_AVG_DURATION` | Stake-weighted average lockup | Higher may indicate commitment |
| `STAKING_VOLATILITY` | Variance in staking ratio | Lower is better (stability) |
| `INCENTIVE_EFFICIENCY` | Staking ratio / inflation cost | Higher is better (efficiency) |

---

## Part IV: Model Validation

A critical methodological question: how do we evaluate whether the model matches reality?

### Goodness-of-Fit Protocol

**Approach:**
1. Initialize model with actual state variables from January 2025
2. Run simulation forward through December 2025
3. Compare simulated trajectories to observed historical values
4. Compute goodness-of-fit metrics

**Metrics:**
| Metric | Description | Target |
|--------|-------------|--------|
| Trajectory correlation | Pearson r between simulated and actual | > 0.90 |
| RMSE (staking ratio) | Root mean squared error | < 2 percentage points |
| Direction accuracy | % of time trends match | > 85% |
| Turning point detection | Captures major inflections | Qualitative assessment |

**If validation fails:** Iterate on behavioral parameter calibration until acceptable fit is achieved. This ensures the model's sensitivity analysis reflects reality, not artifacts.

---

## Part V: Milestones & Deliverables

### Milestone 1: Foundation (Months 1-2)

**Focus:** Data ingestion, model definition, behavioral calibration

**Deliverables:**

| ID | Deliverable | Description |
|----|-------------|-------------|
| 1.1 | Data Ingestion | Ingest Avalanche-provided historical data (validator/delegator flows, rewards, durations) |
| 1.2 | Data Manifest | Documentation of sources, transformations, quality metrics |
| 1.3 | Staking Model Spec | Simplified model focused on staking subsystem with behavioral state variables |
| 1.4 | Behavioral Calibration | Fitted response functions for stake/unstake/restake with confidence intervals |
| 1.5 | Preliminary Validation | Initial goodness-of-fit assessment against 2024-2025 data |

**Success Criterion:** Model achieves >85% correlation with historical staking ratio trajectory


---

### Milestone 2: Simulation & Analysis (Months 3-4)

**Focus:** PSUU implementation, Monte Carlo sweeps, sensitivity analysis

**Deliverables:**

| ID | Deliverable | Description |
|----|-------------|-------------|
| 2.1 | PSUU Infrastructure | Full parameter sweep pipeline with cloud compute |
| 2.2 | Simulation Execution | 50,000+ trajectories across governance × environment space |
| 2.3 | KPI Computation | Automated computation of all KPIs per trajectory |
| 2.4 | Validation Confirmation | Final goodness-of-fit achieving >90% correlation |
| 2.5 | Sensitivity Analysis | Decision trees and correlation matrices for all KPIs |
| 2.6 | Risk Surface Map | Parameter regions where staking incentives fail |

**Success Criterion:** Complete sensitivity analysis with statistically significant results across all KPIs


---

### Milestone 3: Delivery & Transfer (Months 5-6)

**Focus:** Recommendations, documentation, knowledge transfer

**Deliverables:**

| ID | Deliverable | Description |
|----|-------------|-------------|
| 3.1 | Parameter Recommendation Report | Actionable guidance with decision framework |
| 3.2 | Scenario Playbook | "If X market condition, then Y parameter adjustment" |
| 3.3 | Open Source Release | Full model code with documentation |
| 3.4 | Workshop #1 | Model walkthrough for Avalanche team |
| 3.5 | Workshop #2 | How to run scenarios and interpret results |
| 3.6 | ACP Development Support | Simulation-backed evaluation framework for community proposals |
| 3.7 | Integration Guide | How model outputs connect to the Foundation's equilibrium price model |

**Success Criterion:** Avalanche team can independently run and interpret model scenarios


---


## Part VII: Timeline

```
         M1: Foundation          M2: Simulation         M3: Delivery
    ┌─────────────────────┬─────────────────────┬─────────────────────┐
    │                     │                     │                     │
Feb │ Data ingestion      │                     │                     │
    │ Model specification │                     │                     │
    │                     │                     │                     │
Mar │ Behavioral calib.   │                     │                     │
    │ Preliminary valid.  │                     │                     │
    ├─────────────────────┤                     │                     │
Apr │                     │ PSUU infrastructure │                     │
    │                     │ Simulation runs     │                     │
    │                     │                     │                     │
May │                     │ Sensitivity analysis│                     │
    │                     │ Final validation    │                     │
    ├─────────────────────┴─────────────────────┤                     │
Jun │                                           │ Recommendations     │
    │                                           │ Open source release │
    │                                           │                     │
Jul │                                           │ Workshops           │
    │                                           │ Knowledge transfer  │
    └───────────────────────────────────────────┴─────────────────────┘

    Feb        Mar        Apr        May        Jun        Jul
```

**Milestone Checkpoints:**
- **End of March (M1):** Data ingested, behavioral parameters calibrated, model specification complete. Deliverable: Design space documentation and preliminary validation report.
- **End of May (M2):** 50,000+ trajectories simulated, sensitivity analysis complete, model validated against historical data. Deliverable: Sensitivity analysis outputs and risk surface mapping.
- **End of July (M3):** Recommendations delivered, workshops conducted, code released. Deliverable: Parameter recommendation report, open source repository, integration guide.

---

## Part VIII: Team

| Role | Name | Responsibility |
|------|------|----------------|
| Project Lead | Hash Nabir | Stakeholder coordination, milestone management |
| Principal Researcher | Shawn Anderson | Model architecture, PSUU implementation, analysis |
| Data Engineer | Rex | Data analysis, simulation infrastructure |
| Domain Advisor | Jeff Emmett | Token economics, mechanism design, model review |
| Operations Support | Jessica Zartler | Coordination, documentation, publishing |

---

## Part IX: Success Criteria

| Criterion | Measurement | Target |
|-----------|-------------|--------|
| Model validity | Goodness-of-fit vs. historical data | >90% correlation |
| Analysis coverage | KPIs with significant sensitivity results | All defined KPIs |
| Recommendation clarity | Actionable parameter ranges delivered | Yes |
| Knowledge transfer | Avalanche team can run scenarios independently | Verified in workshop |
| Code quality | Open source, documented, reproducible | GitHub release |

---

## Appendix A: Connection to the Equilibrium Price Model

The Foundation's continuous-time asset pricing model takes the staking ratio Θ_t as an input to derive price dynamics:

$$P_t = \frac{(1-\Theta_t) S_t A_t}{Q^*_t} \left( \frac{1-\alpha}{r^f - \mu_t - \Gamma_t} \right)^\alpha$$

**BCRG's contribution:** We compute how Θ_t evolves under different governance configurations and market conditions. Our validated Θ_t trajectories can be plugged directly into the equilibrium framework.

**The bridge:**
```
┌─────────────────────────────────────────────────────────────────┐
│  BCRG BEHAVIORAL MODEL                                          │
│  • Simulates staking behavior                                   │
│  • Outputs: Θ_t trajectories under various scenarios            │
└─────────────────────────────────────────────────────────────────┘
                              │
                         Θ_t trajectories
                              ▼
┌─────────────────────────────────────────────────────────────────┐
│  EQUILIBRIUM PRICE MODEL                                        │
│  • Takes Θ_t as input                                           │
│  • Derives equilibrium price P_t                                │
└─────────────────────────────────────────────────────────────────┘
```

---

## Appendix B: Phase III Horizon

Beyond Phase II, opportunities exist for continued collaboration:

- **ACP Advisory:** Support community proposal development with simulation-backed analysis
- **Ongoing Monitoring:** Periodic model updates as network evolves
- **Extended Scope:** Apply PSUU to other subsystems (fee markets, L1 incentives)

These possibilities can be scoped after Phase II completion based on Foundation priorities.

---

## Appendix C: Reference Materials

- [Subspace PSUU Repository](https://github.com/BlockScience/subspace)
- [How to Perform Parameter Selection Under Uncertainty](https://medium.com/block-science/how-to-perform-parameter-selection-under-uncertainty-976931ba7e5d)
- [Phase I Research](https://bonding-curves.github.io/avalanche-research/)

---

*Proposal prepared by Bonding Curve Research Group*

*January 21, 2026*
