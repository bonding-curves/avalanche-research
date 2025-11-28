---
title: ACP Summaries
---

**Last Updated:** November 28, 2025
**Draft Stage:** 3rd Draft

# ACP Summaries

This document catalogs Avalanche Community Proposals (ACPs)—the formal mechanism through which the Avalanche protocol evolves. Each ACP represents a specific technical change, best practice, or process improvement that has been proposed, discussed, and in many cases activated on the network.

For the economic primitives these ACPs modify, see [Economic Taxonomy](/milestone1/Economic-Taxonomy). For the technical mechanisms they govern, see [Mechanism Taxonomy](/milestone1/Mechanism-Taxonomy). For systems-level analysis of how ACPs interact with the economic model, see [Subsystem Analysis and MultiGraph](/milestone2/Subsystem_Analysis_and_MultiGraph) and [Systems Engineering Perspective](/milestone2/Avalanche-Economic-Model-A-Systems-Engineering-Perspective).

---

## Table of Contents

- [Overview](#overview)
- [ACP Index](#acp-index)
- [Major Upgrade Timeline](#major-upgrade-timeline)
- [Detailed ACP Descriptions](#detailed-acp-descriptions)
- [Future Enhancements](#future-enhancements)
- [References](#references)

---

## Overview

### What Are ACPs?

Avalanche Community Proposals (ACPs) are the primary framework for protocol evolution on Avalanche. They follow a structured multi-stage process from initial idea to network activation, ensuring changes are thoroughly vetted before implementation.

### ACP Tracks

| Track | Purpose | Example |
|-------|---------|---------|
| **Standards Track** | Protocol-level changes requiring network upgrades | ACP-77, ACP-103, ACP-176 |
| **Best Practices Track** | Recommended approaches for builders | ACP-99, ACP-108 |
| **Meta Track** | Changes to the ACP process itself | ACP-84 |

### ACP Status Definitions

| Status | Meaning |
|--------|---------|
| **Proposed** | Under active discussion; not yet ready for implementation |
| **Implementable** | Specification complete; ready for client implementation |
| **Activated** | Deployed to mainnet through a coordinated network upgrade |
| **Superseded** | Replaced by a newer proposal addressing the same problem |
| **Stale** | Inactive; either withdrawn or abandoned due to issues |

For complete details on any ACP, see the [official ACP repository](https://github.com/avalanche-foundation/ACPs).

---

## ACP Index

| ACP | Title | Status | Upgrade |
|:----|:------|:-------|:--------|
| [ACP-13](#acp-13) | Subnet-Only Validators (SOVs) | Superseded | — |
| [ACP-20](#acp-20) | Ed25519 p2p | Activated | Etna (Dec 2024) |
| [ACP-23](#acp-23) | P-Chain Native Transfers | Activated | Durango (Mar 2024) |
| [ACP-24](#acp-24) | Shanghai EIPs on C-Chain | Activated | Durango (Mar 2024) |
| [ACP-25](#acp-25) | Virtual Machine Application Errors | Activated | Durango (Mar 2024) |
| [ACP-30](#acp-30) | Integrate AWM into the EVM | Activated | Durango (Mar 2024) |
| [ACP-31](#acp-31) | Enable L1 Ownership Transfer | Activated | Durango (Mar 2024) |
| [ACP-41](#acp-41) | Remove Pending Stakers | Activated | Durango (Mar 2024) |
| [ACP-62](#acp-62) | Disable AddValidatorTx and AddDelegatorTx | Activated | Durango (Mar 2024) |
| [ACP-75](#acp-75) | Acceptance Proofs | Proposed | — |
| [ACP-77](#acp-77) | Reinventing Subnets | Activated | Etna (Dec 2024) |
| [ACP-83](#acp-83) | Dynamic Multidimensional Fees | Superseded | — |
| [ACP-84](#acp-84) | Table Preamble for ACPs | Activated | 2024 |
| [ACP-99](#acp-99) | Validator Manager Solidity Standard | Proposed | — |
| [ACP-103](#acp-103) | Dynamic Fees for X-Chain and P-Chain | Activated | Etna (Dec 2024) |
| [ACP-108](#acp-108) | EVM Event Importing | Proposed | — |
| [ACP-113](#acp-113) | Provable VM Randomness | Stale | — |
| [ACP-118](#acp-118) | Warp Signature Request Interface | Activated | Etna (Dec 2024) |
| [ACP-125](#acp-125) | Reduce C-Chain Min Base Fee to 1 nAVAX | Activated | Etna (Dec 2024) |
| [ACP-131](#acp-131) | Activate Cancun EIPs | Activated | Etna (Dec 2024) |
| [ACP-151](#acp-151) | P-Chain Height for State Verification | Activated | Etna (Dec 2024) |
| [ACP-176](#acp-176) | Dynamic EVM Gas Limits | Activated | Octane (Apr 2025) |
| [ACP-181](#acp-181) | P-Chain Epoched Views | Activated | Granite (Nov 2025) |
| [ACP-191](#acp-191) | Seamless L1 Creation | Proposed | — |
| [ACP-194](#acp-194) | Streaming Asynchronous Execution | Proposed | — |
| [ACP-204](#acp-204) | Precompile secp256r1 | Activated | Granite (Nov 2025) |
| [ACP-209](#acp-209) | EIP-7702 Style Account Abstraction | Proposed | — |
| [ACP-224](#acp-224) | Dynamic Gas Limit in Subnet-EVM | Proposed | — |
| [ACP-226](#acp-226) | Dynamic Minimum Block Times | Activated | Granite (Nov 2025) |

Some ACPs have been superseded by newer proposals addressing the same problem space (e.g., [ACP-77](#acp-77) supersedes [ACP-13](#acp-13), and [ACP-103](#acp-103) supersedes [ACP-83](#acp-83)).

---

## Major Upgrade Timeline

### Durango (March 6, 2024)

**Activated ACPs:** 23, 24, 25, 30, 31, 41, 62

The Durango upgrade brought Avalanche Warp Messaging to the C-Chain and Subnet-EVM, enabling native cross-chain communication. It also introduced P-Chain native transfers, removed pending stakers, and incorporated Ethereum's Shanghai upgrade features.

### Etna / Avalanche9000 (December 16, 2024)

**Activated ACPs:** 20, 77, 103, 118, 125, 131, 151

The largest network upgrade since mainnet launch, Etna (also called Avalanche9000) fundamentally changed how L1s operate. Key changes:
- Eliminated the 2,000 AVAX staking requirement for L1 validators
- Replaced upfront staking with continuous dynamic fees (~1.33 AVAX/month per validator)
- Reduced C-Chain base fees by 96% (25 nAVAX → 1 nAVAX)
- Added dynamic fees to the P-Chain and X-Chain

### Octane (April 8, 2025)

**Activated ACP:** 176

The Octane upgrade introduced dynamic gas limits and enhanced price discovery mechanisms for the C-Chain and Subnet-EVM chains. Validators can now adjust target gas consumption without hard forks. Following activation, validators increased the C-Chain target gas from 1.6M to 2.1M gas/second (30% increase), and average fees dropped approximately 77%.

### Granite (November 2025)

**Activated ACPs:** 181, 204, 226

The Granite upgrade focused on cross-chain reliability and user experience:
- **P-Chain epoched views** ([ACP-181](#acp-181)): Enables more reliable cross-chain message verification by organizing validator sets into discrete epochs
- **secp256r1 precompile** ([ACP-204](#acp-204)): Native verification of P-256 signatures enabling biometric authentication (fingerprint, Face ID, WebAuthn)
- **Dynamic minimum block times** ([ACP-226](#acp-226)): Adaptive block timing for optimized latency under varying network conditions

For systems-level analysis of how these ACPs interact with the Avalanche economic model, see [Systems Engineering Perspective](/milestone2/Avalanche-Economic-Model-A-Systems-Engineering-Perspective) and [Subsystem Analysis](/milestone2/Subsystem_Analysis_and_MultiGraph).

---

## Detailed ACP Descriptions

### ACP-13

**[Subnet-Only Validators (SOVs)](https://github.com/avalanche-foundation/ACPs/blob/main/ACPs/13-subnet-only-validators.md)** | Superseded by [ACP-77](#acp-77)

This proposal aimed to introduce a new validator type that could validate Avalanche L1s without validating the Primary Network. It would have required nodes to pay a refundable 500 AVAX fee instead of staking 2,000+ AVAX. The goal was to lower the barrier to entry for L1 validation, especially for regulated entities prohibited from validating permissionless chains. SOVs would only need to sync the P-Chain (not X/C-Chain), reducing hardware requirements. This ACP was superseded by [ACP-77](#acp-77), which took a more comprehensive approach to the same problem. For more on L1 economics, see [L1 Ecosystem analysis](/milestone2/Subsystem_Analysis_and_MultiGraph#4-l1-ecosystem-subsystem).

### ACP-20

**[Ed25519 p2p](https://github.com/avalanche-foundation/ACPs/blob/main/ACPs/20-ed25519-p2p.md)** | Activated: Etna (Dec 2024)

Adds support for Ed25519 TLS certificates for peer-to-peer communications. Key benefits include smaller key sizes (32-byte public key, 64-byte private key, 64-byte signature) compared to RSA/ECDSA, simplified node maintenance by generating TLS certificates in-memory on startup, and broader crypto industry adoption. This cryptographic improvement enhances network efficiency and security across all subsystems.

### ACP-23

**[P-Chain Native Transfers](https://github.com/avalanche-foundation/ACPs/blob/main/ACPs/23-p-chain-native-transfers.md)** | Activated: Durango (Mar 2024)

Added support for native transfers on the P-Chain, enabling users to transfer assets without leaving the P-Chain or abusing other transaction types. Registered the BaseTx transaction type with ID `0x22`, providing a cheaper option for simple transfers as L1 adoption grows. See [Fee Dynamics analysis](/milestone2/Subsystem_Analysis_and_MultiGraph#3-fee-dynamics-subsystem).

### ACP-24

**[Shanghai EIPs on C-Chain](https://github.com/avalanche-foundation/ACPs/blob/main/ACPs/24-shanghai-eips.md)** | Activated: Durango (Mar 2024)

Adopted Ethereum Shanghai upgrade EIPs to the C-Chain: EIP-3651 (Warm COINBASE), EIP-3855 (PUSH0 instruction), EIP-3860 (Limit and meter initcode), and EIP-6049 (Deprecate SELFDESTRUCT). Maintains compatibility with upstream EVM tooling and developer experience.

### ACP-25

**[Virtual Machine Application Errors](https://github.com/avalanche-foundation/ACPs/blob/main/ACPs/25-vm-application-errors.md)** | Activated: Durango (Mar 2024)

Introduced a way for Virtual Machines to signal application-defined error conditions to another VM. Added a new AppError message type to the p2p protocol, allowing peers to communicate error conditions instead of relying on timeouts. Enables peer scoring based on perceived errors and decreases latency in failure scenarios.

### ACP-30

**[Integrate Avalanche Warp Messaging into the EVM](https://github.com/avalanche-foundation/ACPs/blob/main/ACPs/30-avalanche-warp-messaging.md)** | Activated: Durango (Mar 2024)

Integrated Avalanche Warp Messaging (AWM) into the C-Chain and Subnet-EVM to enable cross-L1 communication. Introduced a Warp Precompile at address `0x0200000000000000000000000000000000000005` with functions for sending and verifying warp messages. Fundamental to the [L1 Ecosystem](/milestone2/Subsystem_Analysis_and_MultiGraph#4-l1-ecosystem-subsystem) by enabling interoperability between chains. See also [Mechanism Taxonomy: AWM](/milestone1/Mechanism-Taxonomy#avalanche-warp-messaging-awm).

### ACP-31

**[Enable L1 Ownership Transfer](https://github.com/avalanche-foundation/ACPs/blob/main/ACPs/31-enable-subnet-ownership-transfer.md)** | Activated: Durango (Mar 2024)

Allows the current owner of an L1 to transfer ownership to a new owner. Introduced TransferSubnetOwnershipTx that takes an L1 ID, verifies authorization against the current owner, and assigns a new owner. Enables L1 operators to rotate control keys periodically or transfer L1 control to new entities (fee: 0.001 AVAX).

### ACP-41

**[Remove Pending Stakers](https://github.com/avalanche-foundation/ACPs/blob/main/ACPs/41-remove-pending-stakers.md)** | Activated: Durango (Mar 2024)

Removed user-specified StartTime for stakers, instead starting the staking period immediately when a staking transaction is accepted. Improved P-Chain efficiency by eliminating the pending staker set, making MaxValidatorStake verification O(1), and reducing computational load on validators. See [Staking Dynamics](/milestone2/Subsystem_Analysis_and_MultiGraph#1-staking-dynamics-subsystem).

### ACP-62

**[Disable AddValidatorTx and AddDelegatorTx](https://github.com/avalanche-foundation/ACPs/blob/main/ACPs/62-disable-addvalidatortx-and-adddelegatortx.md)** | Activated: Durango (Mar 2024)

Disabled legacy AddValidatorTx and AddDelegatorTx transaction types, requiring all new stakers to use AddPermissionlessValidatorTx and AddPermissionlessDelegatorTx. Ensures all new validators register a BLS key, accelerating the timeline for future P-Chain upgrades and simplifying validator onboarding.

### ACP-75

**[Acceptance Proofs](https://github.com/avalanche-foundation/ACPs/blob/main/ACPs/75-acceptance-proofs.md)** | Proposed

Introduces support for proving a block's acceptance in consensus. Allows peers to verify any block accepted by consensus even if they haven't synced that part of the chain. Enhances fault isolation between the Primary Network and L1s, addressing a potential liveness concern where P-Chain stalling could prevent L1 block verification.

### ACP-77

**[Reinventing Subnets](https://github.com/avalanche-foundation/ACPs/blob/main/ACPs/77-reinventing-subnets.md)** | Activated: Etna (Dec 2024)

The landmark proposal that overhauled L1 creation and management, formally renaming "Subnets" to "L1s." Key changes:
- Separated L1 validators from Primary Network validators
- Moved validator set management from P-Chain to L1s themselves
- Introduced continuous P-Chain fee mechanism (~1.33 AVAX/month per validator)
- Enabled sovereign staking mechanisms (ERC-20, ERC-721, arbitrary tokens)

This fundamentally restructured the [L1 Ecosystem](/milestone2/Subsystem_Analysis_and_MultiGraph#4-l1-ecosystem-subsystem) and introduced new dynamics in both [Staking](/milestone2/Subsystem_Analysis_and_MultiGraph#1-staking-dynamics-subsystem) and [Fee Dynamics](/milestone2/Subsystem_Analysis_and_MultiGraph#3-fee-dynamics-subsystem). See also [Economic Taxonomy: L1 Economics](/milestone1/Economic-Taxonomy#l1-economics).

### ACP-83

**[Dynamic Multidimensional Fees](https://github.com/avalanche-foundation/ACPs/blob/main/ACPs/83-dynamic-fees.md)** | Superseded by [ACP-103](#acp-103)

Aimed to introduce multidimensional fees measuring transaction complexity across four dimensions (Bandwidth, Reads, Writes, Compute). Superseded by [ACP-103](#acp-103), which took a simpler single-dimension approach. See [Fee Dynamics analysis](/milestone2/Subsystem_Analysis_and_MultiGraph#3-fee-dynamics-subsystem).

### ACP-84

**[Table Preamble for ACPs](https://github.com/avalanche-foundation/ACPs/blob/main/ACPs/84-table-preamble.md)** | Activated: 2024

Meta-proposal that replaced plain-text code block preambles with readable Markdown tables. Improved documentation by making links clickable and information more clearly organized, similar to Ethereum EIPs.

### ACP-99

**[Validator Manager Solidity Standard](https://github.com/avalanche-foundation/ACPs/blob/main/ACPs/99-validator-manager.md)** | Proposed (Best Practices)

Defines a standard Validator Manager Solidity smart contract interface for Avalanche EVM chains. Provides a specification for contracts managing L1 validator sets (as introduced in [ACP-77](#acp-77)) through standard methods for validator registration, weight updates, and removal. Aims to lower L1 launch costs and complexity.

### ACP-103

**[Add Dynamic Fees to the X-Chain and P-Chain](https://github.com/avalanche-foundation/ACPs/blob/main/ACPs/103-dynamic-fees.md)** | Activated: Etna (Dec 2024)

Introduced dynamic fee mechanism to P-Chain and X-Chain (superseding [ACP-83](#acp-83)). Defines a single dimension of gas consumption incorporating bandwidth, reads, writes, and compute costs. Adjusts fees based on excess gas consumption to maintain target rates, similar to EIP-1559. Core component of the [Fee Dynamics subsystem](/milestone2/Subsystem_Analysis_and_MultiGraph#3-fee-dynamics-subsystem); affects [Token Supply](/milestone2/Subsystem_Analysis_and_MultiGraph#2-token-supply-subsystem) through fee burning.

### ACP-108

**[EVM Event Importing](https://github.com/avalanche-foundation/ACPs/blob/main/ACPs/108-evm-event-importing.md)** | Proposed (Best Practices)

Defines a standard smart contract interface for importing EVM events from other Avalanche blockchains using AWM. Specifies methods for authenticating block hashes and verifying Merkle proofs of events, enabling cross-chain applications without requiring direct interaction on the source chain. Builds on [ACP-30](#acp-30).

### ACP-113

**[Provable Virtual Machine Randomness](https://github.com/avalanche-foundation/ACPs/blob/main/ACPs/113-provable-vm-randomness.md)** | Stale

Aimed to introduce verifiable random number seed generation using BLS-based VRF where block proposers recursively sign previous signatures. Marked stale due to security concerns: malicious block producers could bias randomness, requiring mitigation strategies deemed too costly for the Primary Network.

### ACP-118

**[Warp Signature Request Interface Standard](https://github.com/avalanche-foundation/ACPs/blob/main/ACPs/118-warp-signature-request.md)** | Activated: Etna (Dec 2024)

Standardizes the format for requesting Warp signatures through the AppRequest protocol. Defines SignatureRequest and SignatureResponse message types that VMs can use to request and provide signatures in a VM-agnostic manner. Simplifies signature aggregator implementations and supports cross-VM functionality, complementing [ACP-30](#acp-30) and [ACP-108](#acp-108).

### ACP-125

**[Reduce C-Chain Minimum Base Fee](https://github.com/avalanche-foundation/ACPs/blob/main/ACPs/125-reduce-c-chain-minimum-base-fee.md)** | Activated: Etna (Dec 2024)

Reduced the minimum base fee on the C-Chain from 25 nAVAX to 1 nAVAX—a 96% reduction. The previous minimum was artificially constraining network usage above market demand. Post-activation, average transaction fees dropped from ~$0.25 to ~$0.01. See [Fee Dynamics analysis](/milestone2/Subsystem_Analysis_and_MultiGraph#3-fee-dynamics-subsystem).

### ACP-131

**[Activate Cancun EIPs](https://github.com/avalanche-foundation/ACPs/blob/main/ACPs/131-activate-cancun-eips.md)** | Activated: Etna (Dec 2024)

Enabled Ethereum Cancun upgrade features on C-Chain and L1-EVM chains:
- EIP-4844 (BLOBHASH opcode, excluding blob transactions)
- EIP-7516 (BLOBBASEFEE opcode)
- EIP-1153 (Transient storage)
- EIP-5656 (MCOPY opcode)
- EIP-6780 (SELFDESTRUCT only in same transaction)

Maintains EVM compatibility for developer tooling.

### ACP-151

**[P-Chain Height for State Verification](https://github.com/avalanche-foundation/ACPs/blob/main/ACPs/151-p-chain-height-for-state-verification.md)** | Activated: Etna (Dec 2024)

Modified the ProposerVM to pass inner VMs the P-Chain block height of the current block being built rather than the parent block's height. Enables more reliable verification of ICM (Interchain Message) aggregated signatures, making operations that modify validator sets verifiable sooner and more reliably.

### ACP-176

**[Dynamic EVM Gas Limits](https://github.com/avalanche-foundation/ACPs/blob/main/ACPs/176-dynamic-gas-limits.md)** | Activated: Octane (Apr 2025)

Introduced dynamic gas limits allowing validators to adjust target gas consumption without hard forks. Validators can incrementally increase or decrease the target rate in blocks they produce, converging to a point where 50% of voting stake weight wants it increased and 50% wants it decreased.

Following activation, validators increased C-Chain target gas from 1.6M to 2.1M gas/second (30% increase), and fees dropped ~77%. Represents a shift toward self-tuning network parameters. See [Fee Dynamics](/milestone2/Subsystem_Analysis_and_MultiGraph#3-fee-dynamics-subsystem) and [Governance](/milestone2/Subsystem_Analysis_and_MultiGraph#5-governance-subsystem) analysis.

### ACP-181

**[P-Chain Epoched Views](https://github.com/avalanche-foundation/ACPs/blob/main/ACPs/181-p-chain-epoched-views.md)** | Activated: Granite (Nov 2025)

Introduces epoched views for the P-Chain, organizing validator sets and state transitions into discrete epochs. Enables more reliable cross-chain message verification by providing stable validator set snapshots for AWM signature validation. Improves synchronization and verification mechanisms for validators joining the network or catching up after downtime. See [Staking Dynamics](/milestone2/Subsystem_Analysis_and_MultiGraph#1-staking-dynamics-subsystem).

### ACP-191

**[Seamless L1 Creation](https://github.com/avalanche-foundation/ACPs/blob/main/ACPs/191-seamless-l1-creation.md)** | Proposed

Introduces CreateL1Tx transaction type to streamline L1 creation. Building on [ACP-77](#acp-77), aims to further reduce friction by simplifying required steps and reducing operational overhead for launching customized blockchain solutions.

### ACP-194

**[Streaming Asynchronous Execution](https://github.com/avalanche-foundation/ACPs/blob/main/ACPs/194-streaming-asynchronous-execution.md)** | Proposed

Introduces Streaming Asynchronous Execution (SAE), separating block execution from consensus. By decoupling these previously synchronous operations, SAE allows continuous execution threads that operate independently of consensus, enabling gas targets to align with average-case rather than worst-case execution times. Expected to significantly improve C-Chain and L1-EVM scalability.

### ACP-204

**[Precompile secp256r1](https://github.com/avalanche-foundation/ACPs/blob/main/ACPs/204-precompile-secp256r1.md)** | Activated: Granite (Nov 2025)

Implements EIP-7951 for secp256r1 (P-256) signature verification on the C-Chain. Provides a precompiled contract at address `0x0000000000000000000000000000000000000100` performing native P-256 signature verification at 6,900 gas—dramatically cheaper than Solidity-based verification (200k-330k gas).

The secp256r1 curve is used by modern device security systems including Apple's Secure Enclave, Android Keystore, WebAuthn, and Passkeys. Enables biometric authentication (fingerprint, Face ID) for Avalanche applications.

### ACP-209

**[EIP-7702 Style Account Abstraction](https://github.com/avalanche-foundation/ACPs/blob/main/ACPs/209-eip7702-style-account-abstraction.md)** | Proposed

Introduces EIP-7702-style account abstraction to C-Chain and L1-EVM chains. Allows Externally Owned Accounts (EOAs) to temporarily delegate control to smart contract code during a transaction, enabling batched operations, sponsored transactions, and custom authorization logic without requiring migration to smart contract wallets.

### ACP-224

**[Dynamic Gas Limit in Subnet-EVM](https://github.com/avalanche-foundation/ACPs/blob/main/ACPs/224-dynamic-gas-limit-in-subnet-evm.md)** | Proposed

Extends [ACP-176](#acp-176) dynamic gas limits to Subnet-EVM chains via a Fee Manager Precompile. Allows L1 operators to configure their own gas targets, bounds, and adjustment rates based on specific use cases. Enhances the sovereignty established by [ACP-77](#acp-77).

### ACP-226

**[Dynamic Minimum Block Times](https://github.com/avalanche-foundation/ACPs/blob/main/ACPs/226-dynamic-minimum-block-times.md)** | Activated: Granite (Nov 2025)

Enables dynamic adjustment of minimum block times based on network conditions and validator consensus. Validators signal preferences for block time adjustments, similar to [ACP-176](#acp-176) gas limits. Allows the network to optimize for latency when conditions allow while maintaining stability during high load periods—another step toward adaptive, self-tuning network parameters.

---

## Future Enhancements

Several additional improvements are under development or proposed for the Avalanche network:

| Enhancement | Description | Status |
|-------------|-------------|--------|
| **Firewood Database** | Optimized state storage reducing validator requirements through improved data layout and state pruning | In Development |
| **Streaming Async Execution** | Decouples block execution from consensus for higher throughput ([ACP-194](#acp-194)) | Proposed |
| **Account Abstraction** | EIP-7702 style account features without smart contract wallet migration ([ACP-209](#acp-209)) | Proposed |
| **L1-EVM Dynamic Gas** | Extends dynamic gas limits to L1 chains ([ACP-224](#acp-224)) | Proposed |

---

## References

1. Avalanche Foundation. *Avalanche Community Proposals (ACPs)*. GitHub Repository. https://github.com/avalanche-foundation/ACPs

2. Avalanche Foundation. *ACP Tracker*. GitHub Projects. https://github.com/orgs/avalanche-foundation/projects/1/views/1

3. Avalanche. *Protocol Upgrades*. Avalanche Builder Hub. https://build.avax.network/docs/protocol-upgrades

4. Ava Labs. *AvalancheGo Releases*. GitHub. https://github.com/ava-labs/avalanchego/releases

5. Avalanche. *Granite Upgrade*. Avalanche Builder Hub. 2025. https://build.avax.network/blog/granite-upgrade

6. Avalanche Foundation. *ACP-77: Reinventing Subnets*. 2024. https://github.com/avalanche-foundation/ACPs/tree/main/ACPs/77-reinventing-subnets

7. Avalanche Foundation. *ACP-103: Dynamic Fees*. 2024. https://github.com/avalanche-foundation/ACPs/tree/main/ACPs/103-dynamic-fees

8. Avalanche Foundation. *ACP-176: Dynamic EVM Gas Limits*. 2025. https://github.com/avalanche-foundation/ACPs/tree/main/ACPs/176-dynamic-evm-gas-limit-and-price-discovery-updates
