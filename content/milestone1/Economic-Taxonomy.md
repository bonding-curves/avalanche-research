**Avalanche Economic Primitives**

**Token Issuance**  AVAX has a hard cap of 720M tokens, with 360M available at
mainnet launch. The remaining tokens are released through staking rewards over
time. This fixed supply model creates scarcity while ensuring sufficient tokens
for network security through the staking mechanism. All tokens were pre-mined
at genesis, with no additional mining or inflation mechanisms beyond the
initial allocation. Notably, the community retains governance rights over the
token's long-term monetary policy, including the ability to determine whether
AVAX remains capped or adopts deflationary mechanisms through transaction fee
burning.

**Validator Incentives**  Validators earn rewards proportional to their stake
amount and lockup duration. Current reward rates average ~8% APR but fluctuate
based on network participation and governance decisions. The system employs
proof-of-uptime (minimum 80% online) and proof-of-correctness rather than
slashing penalties, creating positive reinforcement for proper validation.
Validators must maintain responsiveness to receive rewards—underperforming
validators simply forfeit rewards rather than face penalties. Maximum validator
weight is capped at the minimum of 3 million AVAX or 5x the validator's staked
amount, preventing excessive centralization. Rewards continue until the maximum
supply is reached, which depends on governance-controlled emission rates and
could extend several decades.

**Staking Mechanism**  The minimum requirement to become a validator is 2,000
AVAX. Staking lockup periods range from 2 weeks to 52 weeks, with longer
commitments receiving higher rewards. Delegation is supported with a 25 AVAX
minimum, allowing token holders to participate in network security without
running validator infrastructure. Unlike other PoS networks, Avalanche does not
implement slashing, reducing validator risk while maintaining security through
its consensus mechanism and positive incentive structures.

**Liquid Staking Infrastructure**  Avalanche supports liquid staking through
multiple providers including GoGoPool (ggAVAX), BenQi (sAVAX), and Ankr
(ankrAVAX), enabling stakers to maintain liquidity while earning rewards.
Liquid staking tokens (LSTs) represent staked positions and can be deployed in
DeFi protocols for lending, borrowing, liquidity provision, and yield
farming—enabling dual reward streams from both staking and DeFi activities. The
Avalanche Foundation's Icebreaker Program actively supports LST adoption by
deploying AVAX to bootstrap liquidity and utility across the ecosystem. Liquid
staking significantly lowers participation barriers, with minimums as low as 1
AVAX compared to 2,000 AVAX for validators or 25 AVAX for direct delegation.
While redemption of underlying AVAX may take up to 4 weeks, LSTs themselves
trade freely on secondary markets. However, liquid staking introduces smart
contract risk and potential recursive leverage concerns that governance
mechanisms must monitor to prevent excessive influence over consensus.

**Fee Structure**  All transaction fees across P-Chain, X-Chain, and C-Chain
are burned completely rather than redistributed to validators. This creates a
direct relationship between network usage and token scarcity—higher activity
leads to increased token burning and reduced circulating supply. Gas fees on
the C-Chain follow similar mechanics to Ethereum but with the key difference
that fees are burned rather than partially distributed to validators. The fee
burning mechanism introduces deflationary pressure during periods of high
network activity, creating an organic scarcity mechanism beyond the hard cap.

**L1 Economics**  L1s (formerly known as Subnets) can implement custom token
models and fee structures while leveraging Avalanche's security and
interoperability. Following ACP-77's activation, L1 validators are no longer
required to validate the Primary Network, significantly reducing the barrier to
entry and costs for custom blockchain deployment. L1 creators can define
validator requirements, reward mechanisms, and governance parameters specific
to their application needs. L1s may require validators to stake custom tokens
rather than AVAX, enabling fully sovereign economic models. The P-Chain charges
L1 validators a continuous dynamic fee for every discrete unit of time they
remain active, properly metering the persistent computational load each
validator adds to the network. This fee mechanism addresses the "state rent"
problem common in blockchain systems while maintaining economic sustainability
for L1 deployment.

**Governance Architecture**  Avalanche employs a hybrid governance model
combining limited on-chain voting with community-driven improvement proposals.
On-chain governance mechanisms enable direct voting on critical network
parameters including minimum stake requirements, staking durations, reward
emission rates, and transaction fee structures. However, unlike fully
permissionless governance systems, Avalanche restricts governance to
predetermined parameters rather than allowing arbitrary system modifications,
prioritizing network stability and predictability.

The primary governance framework operates through Avalanche Community Proposals
(ACPs), which follow a structured multi-stage process: (1) Idea vetting through
public GitHub Discussions, (2) Formal proposal drafting and submission via pull
request, (3) Proposed status with active community discussion and iteration,
(4) Implementable status when ready for deployment, and (5) Activated status
following coordinated network upgrade. Throughout this process, the community
voices support or objection through "Straw Polls," though final activation
requires coordinated adoption by validators and node operators rather than
token-weighted voting.

ACPs are categorized into three tracks: Standards Track (protocol-level changes
and network upgrades like ACP-77's L1 reformation), Best Practices Track
(recommended approaches for builders and developers), and Meta Track
(modifications to the ACP process itself). The Avalanche Foundation may provide
non-binding recommendations on certain ACPs, but implementation remains a
community-driven decision.

**Governance Safeguards**  Economic parameters include built-in hysteresis
mechanisms that prevent rapid manipulation. Once a parameter changes through
governance, it becomes increasingly difficult to modify the same parameter by
large amounts in subsequent votes, with this difficulty decreasing gradually
over time. This design enables long-term flexibility while preventing
short-term volatility or adversarial manipulation through frequent parameter
changes. Time delays between governance proposals and their activation provide
the community adequate review periods, while range limitations ensure changes
occur within economically sustainable bounds. These mechanisms balance
decentralized governance with economic stability, protecting both network
security and stakeholder interests.
