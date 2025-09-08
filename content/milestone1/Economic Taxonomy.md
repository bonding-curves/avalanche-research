**Avalanche Economic Primitives**

**Token Issuance**  
AVAX has a hard cap of 720M tokens, with 360M available at mainnet launch. The remaining tokens are released through staking rewards over time. This fixed supply model creates scarcity while ensuring sufficient tokens for network security through the staking mechanism. All tokens were pre-mined at genesis, with no additional mining or inflation mechanisms beyond the initial allocation.

 **Validator Incentives**  
Validators earn rewards proportional to their stake amount and lockup duration. Current reward rates average \~8% APR but may fluctuate based on network participation. The system employs proof-of-uptime and proof-of-correctness rather than slashing penalties, creating positive reinforcement for proper validation. Rewards continue until approximately 2030 when the maximum supply cap is projected to be reached.

 **Staking Mechanism**  
The minimum requirement to become a validator is 2,000 AVAX. Staking lockup periods range from 2 weeks to 52 weeks, with longer commitments receiving higher rewards. Delegation is supported, allowing token holders to participate in network security without running validator infrastructure. Unlike other PoS networks, Avalanche does not implement slashing, reducing validator risk while maintaining security through its consensus mechanism.

 **Fee Structure**  
All transaction fees across P-Chain, X-Chain, and C-Chain are burned completely rather than redistributed to validators. This creates a direct relationship between network usage and token scarcity \- higher activity leads to increased token burning and reduced circulating supply. Gas fees on the C-Chain follow similar mechanics to Ethereum but with the key difference that fees are burned rather than partially distributed to validators.

 **L1 Economics**  
L1 can implement custom token models and fee structures while leveraging Avalanche's security and interoperability. L1 creators can define validator requirements, reward mechanisms, and governance parameters specific to their application needs. L1s may require validators to stake both AVAX and subnest-specific tokens, creating a dual-token economic model that benefits both the primary network and the L1.

 **Governance Parameters**  
Key economic variables including minimum stake requirements, reward rates, fee structures, and staking periods are subject to governance within predetermined boundaries. Changes to these parameters require network-wide voting with time and range limitations to prevent rapid or extreme modifications. Governance includes hysteresis mechanisms that limit how frequently parameters can be adjusted, preventing market manipulation through frequent economic policy changes.
