---
title: Avalanche Economic Primitives

---

***

# Avalanche Economic Primitives

## Token Issuance

AVAX has a hard supply cap of **720 million tokens**. Of this, **360 million** were available at the mainnet launch, with the remainder released over time through **staking rewards**. This fixed-supply model creates scarcity while ensuring sufficient tokens are available to secure the network via staking.

- All tokens were pre-mined at genesis; there are no inflationary or mining mechanisms beyond this initial allocation and staking rewards.  
- The community holds governance rights over the token’s long-term monetary policy, including future decisions on maintaining the supply cap or implementing deflationary measures.

***

## Validator Incentives (Primary Network)

Validators earn rewards based on their **staked amount** and **staking duration**. Current reward rates average **8–9% APR**, varying with network participation and governance outcomes.

Avalanche uses **proof-of-uptime** (minimum 80% online) and **proof-of-correctness** instead of slashing:

- Validators must remain responsive to receive rewards.  
- Underperforming or offline validators forfeit potential rewards rather than face penalties.  
- To discourage centralization, a validator’s maximum weight (self-stake + delegated stake) is limited to the **minimum of 3 million AVAX or 5× the validator’s own stake**.

***

## Staking Mechanism (Primary Network)

Several recent **Avalanche Community Proposals (ACPs)** have refined how staking works on the Primary Network.

- **Validator Minimum:** 2,000 AVAX  
- **Delegator Minimum:** 25 AVAX  
- **Lockup Periods:** 2 weeks to 52 weeks  

### Key ACP Updates

- **ACP-41: Immediate Staking**  
  The user-specified StartTime field has been removed. Staking periods begin immediately when transactions are accepted. This eliminates the “pending staker set,” reducing P-Chain computation overhead.

- **ACP-62: BLS Key Requirement**  
  Legacy `AddValidatorTx` and `AddDelegatorTx` are disabled. All new stakers must use `AddPermissionlessValidatorTx` or `AddPermissionlessDelegatorTx`, which require BLS key registration for upcoming protocol features.

- **ACP-236: Continuous Staking (Proposed)**  
  Introduces “continuous staking,” allowing validators to stake indefinitely and auto-compound rewards each cycle. Applies only to Primary Network validators (not delegators or L1 validators).

***

## Liquid Staking Infrastructure

Avalanche supports a diverse **liquid staking ecosystem** through providers such as:

- **Hypha (formerly GoGoPool):** Offers ggAVAX and stAVAX  
- **BenQi:** Offers sAVAX  

Liquid staking tokens (LSTs) represent staked positions that maintain liquidity. They can be used across DeFi protocols for **lending**, **borrowing**, and **liquidity provision**, generating dual yield streams (staking + DeFi rewards).  
Minimum staking through liquid protocols can be as low as **1 AVAX**.

***

## Fee Structure

All **transaction fees** on the **P-Chain**, **X-Chain**, and **C-Chain** are **burned**, introducing **deflationary pressure** proportional to network usage.

### P-Chain (Dynamic Fees)
Introduced by **ACP-103**, replacing fixed fees with a **multi-dimensional dynamic model** that accounts for:

- Bandwidth (transaction size)  
- Reads (database queries)  
- Writes (database updates)  
- Compute (signature verification, etc.)

Each resource’s cost adjusts dynamically based on usage relative to target levels.

### C-Chain (Dynamic Fees)
Under **ACP-176**, the target gas consumption rate can now adjust dynamically based on validator preferences, enhancing scalability.  
**ACP-125** also lowered the minimum base fee from 25 nAVAX to **1 nAVAX**.

### X-Chain (Fixed Fees)
Still uses a **fixed-fee** model. Migration to dynamic fees was deferred under **ACP-103** due to low current usage.

***

## L1 Economics (Formerly Subnets)

**ACP-77** redefined Subnets as **Layer-1 (L1)** environments with **sovereign economics** and reduced participation barriers.

### Key Features

- **Validator Independence:**  
  L1 validators no longer need to validate the Primary Network. The 2,000 AVAX staking requirement is removed. Validators only need to sync the P-Chain, simplifying regulated or enterprise L1 setups.

- **Sovereign Validator Sets:**  
  L1s define their own validation logic and tokens using a **validator manager smart contract** deployed on an EVM chain.  
  The **ACP-99** standard (`ACP99Manager`) provides a standard Solidity interface for interoperability.

- **Continuous Fee Model:**  
  Validators pay a **dynamic continuous fee** in AVAX to the P-Chain while validating.  
  The system targets ~10,000 L1 validators, with a **minimum fee of 512 nAVAX/sec (~1.33 AVAX/month)**, enabling broader access.

- **Streamlined Creation (ACP-191):**  
  Consolidates the three-step creation process (`CreateSubnetTx`, `CreateChainTx`, `ConvertSubnetToL1Tx`) into a single atomic transaction: `CreateL1Tx`.

***

## Governance Architecture

Avalanche employs a **hybrid governance model** combining limited on-chain voting for key parameters with **off-chain community coordination**.

### Avalanche Community Proposals (ACPs)

ACPs serve as the core framework for protocol development and standardization.

#### Tracks
- **Standards Track:** Protocol-level modifications  
- **Best Practices Track:** Interface and design patterns (e.g., ACP-99)  
- **Meta Track:** Changes to the ACP process  
- **Subnet Track:** L1-specific improvements  

#### Workflow
1. **Idea:** Discussed openly on GitHub Discussions  
2. **Proposed:** Drafted and merged via pull request  
3. **Implementable:** Approved by authors for deployment  
4. **Activated:** Adopted through a coordinated network upgrade

***

## Governance Safeguards

Avalanche governance includes **hysteresis mechanisms** to mitigate rapid manipulation of network parameters.  
When a parameter (e.g., staking rate) is adjusted, subsequent changes to that same parameter face progressively higher thresholds.  
Over time, these thresholds relax, preserving long-term flexibility while reducing short-term volatility.

***

## Key Proposed Protocol Changes

### ACP-194: Streaming Asynchronous Execution
Separates **consensus** from **execution** so blocks are accepted before being asynchronously executed. This design:

- Increases throughput  
- Enables novel features like encrypted mempools  

### ACP-226: Dynamic Minimum Block Times
Replaces static target block intervals with a **dynamic minimum block delay** (in milliseconds), determined collectively by validators.  
This allows **sub-second block times** as the network’s performance improves.

***