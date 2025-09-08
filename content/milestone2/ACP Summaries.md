# ACP Summaries

Avalanche Community Proposals (ACPs) by number and title:

| ACP | Title |  
|:-------|:------|  
|13|Subnet-Only Validators (SOVs)|  
|20|Ed25519 p2p|  
|23|P-Chain Native Transfers|  
|24|Shanghai EIPs on C-Chain|  
|25|Virtual Machine Application Errors|  
|30|Integrate Avalanche Warp Messaging into the EVM|  
|31|Enable Subnet Ownership Transfer|  
|41|Remove Pending Stakers|  
|62|Disable AddValidatorTx and AddDelegatorTx|  
|75|Acceptance Proofs|  
|77|Reinventing Subnets|  
|83|Dynamic Multidimensional Fees for P-Chain and X-Chain|  
|84|Table Preamble for ACPs|  
|99|Validator Manager Solidity Standard|  
|103|Add Dynamic Fees to the X-Chain and P-Chain|  
|108|EVM Event Importing|  
|113|Provable Virtual Machine Randomness|  
|118|Warp Signature Request Interface Standard|  
|125|Reduce C-Chain minimum base fee from 25 nAVAX to 1 nAVAX|  
|131|Activate Cancun EIPs on C-Chain and Subnet-EVM chains|  
|151|Use current block P-Chain height as context for state verification|  
|176|Dynamic EVM Gas Limits and Price Discovery Updates|

This list reflects all ACPs documented in the provided repository. Some have been activated, while others remain in proposed or implementable states. A few have been superseded by newer proposals (e.g., ACP-77 supersedes ACP-13, and ACP-103 supersedes ACP-83).

**ACP-13: Subnet-Only Validators (SOVs)**   
This proposal aimed to introduce a new validator type that could validate Avalanche Subnets without validating the Primary Network. It would have required nodes to pay a refundable 500 AVAX fee instead of staking 2000+ AVAX. The goal was to lower the barrier to entry for Subnet validation, especially for regulated entities prohibited from validating permissionless chains. SOVs would only need to sync the P-Chain (not X/C-Chain), reducing hardware requirements. This ACP was later superseded by ACP-77 (Reinventing Subnets), which took a more comprehensive approach to the same problem space.

**ACP-20: Ed25519 p2p**  
This proposal aims to support Ed25519 TLS certificates for p2p communications on the Avalanche network. It would allow the use of Ed25519 public keys for Avalanche Network Client NodeIDs and support Ed25519 signatures in the ProposerVM. The key benefits include smaller key sizes (32-byte public key, 64-byte private key, 64-byte signature) compared to RSA/ECDSA, simplified node maintenance by generating TLS certificates in-memory on startup, and wider crypto industry adoption.

**ACP-23: P-Chain Native Transfers**  
This activated proposal added support for native transfers on the P-chain, enabling users to transfer P-chain assets without leaving the P-chain or abusing other transaction types. It registered the BaseTx transaction type with ID 0x22 in codec version 0x00, providing a cheaper option for both validators and end-users to perform simple transfers as Subnet adoption grows.

**ACP-24: Shanghai EIPs on C-Chain**  
This activated proposal adopted several Ethereum Improvement Proposals (EIPs) from Ethereum's Shanghai upgrade to the Avalanche C-Chain: EIP-3651 (Warm COINBASE), EIP-3855 (PUSH0 instruction), EIP-3860 (Limit and meter initcode), and EIP-6049 (Deprecate SELFDESTRUCT). This maintained compatibility with upstream EVM tooling, infrastructure, and developer experience.

**ACP-25: Virtual Machine Application Errors**  
This activated proposal introduced a way for Virtual Machines (VMs) to signal application-defined error conditions to another VM. It added a new AppError message type to the p2p protocol, allowing peers to communicate error conditions instead of relying on timeouts. This enables Avalanche nodes to score peers based on perceived errors and decreases latency in failure scenarios.

**ACP-30: Integrate Avalanche Warp Messaging into the EVM**  
This activated proposal integrated Avalanche Warp Messaging (AWM) into the C-Chain and Subnet-EVM to enable cross-subnet communication. It introduced a Warp Precompile at address 0x0200000000000000000000000000000000000005 with functions for sending and verifying warp messages, creating a standard implementation of AWM in production on the Avalanche Network.

**ACP-31: Enable Subnet Ownership Transfer**  
This activated proposal allows the current owner of a Subnet to transfer ownership to a new owner. It introduced a new transaction type (TransferSubnetOwnershipTx) that takes a Subnet ID, verifies the SubnetAuth against the current Owner, and assigns a new Owner to the Subnet. This enables Subnet operators to rotate their control keys periodically or transfer Subnet control to new entities, with a fee of 0.001 AVAX.

**ACP-41: Remove Pending Stakers**  
This activated proposal removed user-specified StartTime for stakers, instead starting the staking period immediately when a staking transaction is accepted. This significantly improved P-chain efficiency by eliminating the need to maintain a pending set of stakers, making MaxValidatorStake verification an O(1) operation, and reducing computational load on validators.

**ACP-62: Disable AddValidatorTx and AddDelegatorTx**  
This activated proposal disabled the legacy AddValidatorTx and AddDelegatorTx transaction types, pushing all new stakers to use AddPermissionlessValidatorTx and AddPermissionlessDelegatorTx instead. This ensured all new validators register a BLS key, accelerating the timeline for future P-Chain upgrades and reducing the number of ways to participate in Primary Network validation from two to one.

**ACP-75: Acceptance Proofs**  
This proposed feature introduces support for proving a block's acceptance in consensus. It allows peers to verify any block accepted by consensus even if they haven't synced that part of the chain. This enhances fault isolation between the Primary Network and Subnets, addressing a potential liveness concern where P-Chain stalling could prevent Subnet block verification.

**ACP-77: Reinventing Subnets**  
This activated proposal completely overhauled Subnet creation and management. It separated Subnet validators from Primary Network validators, moved ownership of Subnet validator set management from the P-Chain to Subnets, and introduced a continuous P-Chain fee mechanism for Subnet validators. This enabled Avalanche Layer 1s (L1s) with greater flexibility and sovereignty, allowing for ERC-20/ERC-721/arbitrary staking mechanisms.

**ACP-83: Dynamic Multidimensional Fees for P-Chain and X-Chain**  
This stale proposal aimed to introduce a dynamic and multidimensional fee scheme for the P-chain and X-chain. It would have measured transaction complexity along four dimensions (Bandwidth, Reads, Writes, Compute) and dynamically adjusted fees based on network congestion. This proposal was superseded by ACP-103, which took a simpler approach to dynamic fees.

**ACP-84: Table Preamble for ACPs**  
This activated meta-proposal replaced the plain-text code block in ACP preambles with a more readable Markdown table format. This improved readability and user experience by making links clickable and information more clearly organized, similar to the format used in Ethereum EIPs.

**ACP-99: Validator Manager Solidity Standard**  
This proposed best practice defines a standard Validator Manager Solidity smart contract interface for Avalanche EVM chains. It provides a specification for contracts that can manage an L1 validator set (as introduced in ACP-77) through standard methods for validator registration, weight updates, and removal. This standardization aims to lower the cost of launching L1s on Avalanche.

**ACP-103: Add Dynamic Fees to the X-Chain and P-Chain**  
This activated proposal introduced a dynamic fee mechanism to the P-Chain (superseding ACP-83). It defines a single dimension of gas consumption that incorporates bandwidth, reads, writes, and compute costs. The mechanism adjusts fees based on excess gas consumption to maintain a target gas consumption rate, similar to EIP-1559 in Ethereum.

**ACP-108: EVM Event Importing**  
This proposed best practice defines a standard smart contract interface for importing EVM events from other blockchains within Avalanche using Avalanche Warp Messaging. It specifies methods for authenticating block hashes and verifying Merkle proofs of events, enabling cross-chain applications without requiring direct interaction on the source chain.

**ACP-113: Provable Virtual Machine Randomness**  
This stale proposal aimed to introduce a mechanism for generating verifiable, non-cryptographic random number seeds on the Avalanche platform. It would have used a BLS-based VRF implementation where block proposers recursively sign previous signatures. The proposal was marked stale due to documented security concerns, particularly the ability for malicious block producers to bias randomness, requiring complex mitigation strategies that were deemed too costly for the Primary Network.

**ACP-118: Warp Signature Request Interface Standard**  
This implementable best practice proposes a standard format for requesting Warp signatures through the AppRequest protocol. It defines SignatureRequest and SignatureResponse message types that VMs can use to request and provide signatures for Warp messages in a VM-agnostic manner. This standardization simplifies signature aggregator implementations and supports cross-VM functionality.

**ACP-125: Reduce C-Chain minimum base fee from 25 nAVAX to 1 nAVAX**  
This activated proposal reduced the minimum base fee on the Avalanche C-Chain from 25 nAVAX to 1 nAVAX. The change was made because the previous minimum was observed to be higher than market demand, artificially reducing network usage. The dynamic fee algorithm had proven capable of responding appropriately during high-use periods, making the higher minimum unnecessary.

**ACP-131: Activate Cancun EIPs on C-Chain and Subnet-EVM chains**  
This activated proposal enabled new EVM opcodes and changes from Ethereum's Cancun upgrade on the Avalanche C-Chain and Subnet-EVM chains. It included EIP-4844 (BLOBHASH opcode), EIP-7516 (BLOBBASEFEE opcode), EIP-1153 (Transient storage), EIP-5656 (MCOPY opcode), and EIP-6780 (SELFDESTRUCT only in same transaction). Notably, it excluded blob transactions from EIP-4844.

**ACP-151: Use current block P-Chain height as context for state verification**  
This activated proposal modified the ProposerVM to pass inner VMs the P-Chain block height of the current block being built rather than the parent block's height. This allows for more reliable verification of ICM (Interchain Message) aggregated signatures, making operations that modify validator sets verifiable sooner and more reliably.

**ACP-176: Dynamic EVM Gas Limits and Price Discovery Updates**   
This proposed standards change would modify the C-Chain and Subnet-EVM chains to adopt a dynamic fee mechanism similar to the one introduced on the P-Chain in ACP-103, but with modifications allowing block proposers (validators) to dynamically adjust the target gas consumption rate. The proposal defines a mechanism where validators can incrementally increase or decrease the target gas consumption rate in blocks they produce, causing the effective rate to converge to a point where 50% of voting stake weight wants it increased and 50% wants it decreased. This removes the need for network upgrades to adjust gas limits as the network's capacity evolves.