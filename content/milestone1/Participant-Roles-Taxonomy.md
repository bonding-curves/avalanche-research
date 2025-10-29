**Last Update:** October 29th, 2025  **Draft Stage:** 3rd Draft

# **Role Taxonomy Overview**

The proposed taxonomy below is intended to reflect the core roles within The
Avalanche Network as they relate to the current and future state of the
ecosystem. Roles specify the incentives and behaviors of sets of network
actors, as well as the actions those actors can execute, and the value flows to
and from those actors. Furthermore, the taxanomy explores the relationships
between roles, and example entities that would take on such roles. The result
is a taxanomy of roles and relationships in the Avalanche Economic Network.
Please note that these roles are not mutually exclusive; thus an entity can
play more than one role.

## ![][image1]

## Public Actors in the Avax Network:

### Network Participants

* Primary Network Validators  
* L1 Validators  
* Delegators  
* Token Holders

### Development Organizations

* Ava Labs  
* Avalanche Foundation  
* Infrastructure Providers

### Community Members

* App Users  
* Developers  
* Investors  
* Traders

* ## Network Participants

  * ### Primary Network Validator (PNV)

    * **Definition**  
      * Primary Network Validators are the core validators responsible for
      securing the main Avalanche network. They serve as the foundation of
      network security and
      [consensus](Mechanism%20Taxonomy.md#consensus-layer-implementation).  
    * **Parameters**  
      * Minimum [stake](Economic%20Taxonomy.md#staking-mechanism) 2000 AVAX  
      * Minimum delegation amount: 25 AVAX
      * Minimum staking duration: 2 weeks
      * Maximum staking duration: 1 year
      * Maximum validator weight: 3 million AVAX (or 5x the validator's own stake, whichever is less)
    * **Eligibility**  
      * Need to run a node meeting hardware requirements  
      * Must maintain high uptime (\>80%)  
      * Failing this threshold results in NO rewards for the validation period  
      * This affects both validator and delegator rewards  
      * Uptime is measured over each staking period (2 weeks \- 1 year)  
    * **Actions Performed**  
      * Participate in
      [Consensus](Mechanism%20Taxonomy.md#consensus-layer-implementation)  
        * Process
        [Transactions](Mechanism%20Taxonomy.md#three-chain-architecture)  
        * Maintain Network Security  
        * Validate L1s  (Optional)  
    * **Value Flows**  
      * PNVs earn [staking
      rewards](Economic%20Taxonomy.md#validator-incentives) from network
      inflation, collect [transaction
      fees](Economic%20Taxonomy.md#fee-structure) from processed operations,
      and can receive additional fees from L1 validation services.  
    * **Preferences**  
      * These validators typically align with long-term network growth,
      prioritize stable and reliable infrastructure, and focus on maintaining
      high uptime.  
    * **Considerations**  
      * Must account for high capital requirements, possess significant
      technical expertise, and manage substantial infrastructure costs.  
      * Validators are a very important stakeholder group in the network as
      they are committed (through their stake) and will be involved for at
      least the duration of the staking validation period  
    * **Delegation Mechanics**  
      * Can accept [delegated stake](Economic%20Taxonomy.md#staking-mechanism)
      from other token holders, typically setting minimum delegation amounts
      and configuring revenue sharing percentages. They must carefully balance
      delegation rewards to remain competitive while maintaining profitability.  
    * **Technical Operations**  
      * Must run
      [AvalancheGo](https://docs.avax.network/nodes/run/node-manually) nodes
      with specific hardware requirements, implement comprehensive monitoring
      systems, maintain database health, and ensure optimal network
      connectivity. This includes managing [chain
      state](Mechanism%20Taxonomy.md#three-chain-architecture), handling
      upgrades, and monitoring system resources.  
    * **Risk Management**  
      * Face potential slashing for poor performance or malicious behavior.
      They must implement robust security measures, maintain high uptime
      through redundancy, and carefully monitor validation performance metrics.  
    * **Economic Optimization**  
      * These validators optimize [fee
      structures](Economic%20Taxonomy.md#fee-structure), balance delegation
      rewards with operational costs, and develop long-term strategies for
      maximizing returns while maintaining network health.  
    * **Cross-L1 Operations**  
      * Often validate multiple L1s, requiring careful resource allocation and
      management of different validation requirements across networks.

  * ### L1 Validator (L1V)

    * **Definition**  
      * L1 Validators are specialized validators focused on specific
      [L1s](Mechanism%20Taxonomy.md#l1-management), operating within customized
      validation environments.  
    * **Eligibility**  
      * Meet L1-specific requirements/conditions  
      * Custom L1 specific validation periods  
      * May require KYC/permissions  
    * **Actions Performed**  
      * These validators focus on L1-specific [transaction
      validation](Mechanism%20Taxonomy.md#consensus-layer-implementation),   
      * Maintain individual L1 states  
      * execute specialized logic required by their particular L1.  
    * **Value Flows**  
      * L1Vs receive L1-specific rewards, may earn custom token incentives, and
      participate in various [fee-sharing
      models](Economic%20Taxonomy.md#l1-economics) unique to their L1.  
    * **Preferences**  
      * specialize in specific L1 operations  
      * focus on application-specific requirements  
    * **Considerations**  
      * While capital requirements may be lower, L1Vs need specialized
      knowledge of their L1’s operations and must navigate variable reward
      structures.  
    * **Delegation Mechanics**  
      * L1Vs may have L1-specific delegation rules, custom token requirements,
      and unique revenue sharing models based on L1 parameters.  
    * **Technical Operations**  
      * They must maintain specialized infrastructure for L1 validation,
      implement L1-specific monitoring, and manage custom [virtual
      machines](Mechanism%20Taxonomy.md#virtual-machine-components) as required
      by their L1.  
    * **Risk Management**  
      * L1Vs navigate L1-specific slashing conditions, maintain compliance with
      custom validation rules, and manage risks across multiple token types.  
    * **Economic Optimization**  
      *  These validators optimize for L1-specific rewards, balance resources
      across different validation activities, and develop strategies for
      maximizing returns within L1 parameters.  
    * **Cross-**L1 **Operations**  
      * L1Vs must manage interactions between their L1 and the primary network,
      handle cross-L1 messaging, and maintain operational efficiency across
      multiple validation environments.

  * ### Delegator

    * **Definition**  
      * Delegators participate in network security by
      [staking](Economic%20Taxonomy.md#staking-mechanism) AVAX to validators  
      * They can delegate through [Core Wallet](https://core.app) or liquid
      staking protocols  
      * Liquid staking options include [Benqi](https://benqi.fi) and
      [GoGoPool](https://gogopool.com)  
    * **Actions & Responsibilities**  
      * Research and select reliable validators  
      * Monitor validator uptime (critical for rewards)  
      * Manage delegation through Core Wallet or liquid staking  
      * Claim rewards after validation periods  
      * Track validator performance metrics  
    * **Value Flows**  
      * [Stake](Economic%20Taxonomy.md#staking-mechanism) minimum 25 AVAX per
      delegation  
      * Earn [staking rewards](Economic%20Taxonomy.md#validator-incentives)
      (minus validator fee)  
      * No rewards if validator fails minimum uptime requirement  
      * Liquid staking options provide additional flexibility  
    * **Key Considerations**  
      * Validator uptime history is crucial  
      * Choose between direct staking vs liquid staking  
      * Minimum time is 2 weeks and maximum time is 1 year  
      * Reward claiming responsibility  
      * Risk of losing rewards due to poor validator performance

  * ### Token Holder

    * **Definition:**  
      * Primary stakeholders in the Avalanche ecosystem  
      * Hold AVAX tokens with full custody and control  
      * Can transition between multiple participant roles  
      * Key participants in [network
      governance](Mechanism%20Taxonomy.md#governance-components)  
    * **Actions Performed:**  
      * Store and manage AVAX tokens  
      * Participate in [governance
      voting](Mechanism%20Taxonomy.md#voting-process)  
      * [Delegate](Economic%20Taxonomy.md#staking-mechanism) tokens to
      validators  
      * Trade and transfer tokens  
      * Interact with dApps and services  
      * Stake tokens directly as validators  
    * **Value Flows:**  
      * **Inflows:**  
        * Token acquisitions through purchases  
        * [Staking/delegation
        rewards](Economic%20Taxonomy.md#validator-incentives)  
        * Airdrops and incentives  
        * DeFi yields and returns  
      * **Outflows:**  
        * [Transaction fees](Economic%20Taxonomy.md#fee-structure)  
        * Token transfers  
        * Smart contract interactions  
        * [Governance
        participation](Mechanism%20Taxonomy.md#governance-components) costs  
    * **Preferences:**  
      * Asset security and custody  
      * Network governance participation  
      * Return on investment opportunities  
      * Ecosystem utility and growth  
      * Low [transaction costs](Economic%20Taxonomy.md#fee-structure)

* ## Development Organizations

  * ### Ava Labs 

    * **Definition**  
      * Core development organization behind [Avalanche
      Network](https://avax.network)  
      * Research-driven technology company focused on blockchain innovation  
      * Founded by [Emin Gün Sirer](https://www.avalabs.org/team), Kevin
      Sekniqi, and Ted Yin  
    * **Actions Performed**  
      * Core [protocol development](Mechanism%20Taxonomy.md) and maintenance  
      * Infrastructure and tooling development ([Core
      Wallet](https://core.app), SDKs)  
      * Security monitoring and upgrades  
      * Technical documentation and education  
      * Enterprise partnership development  
    * **Value Flows**  
      * Invests in R\&D and protocol innovation  
      * Provides developer tools and resources  
      * Delivers security improvements and updates  
      * Enables ecosystem growth through partnerships  
      * Supports community education and adoption  
    * **Preferences**  
      * Open source development methodology  
      * Research-backed innovation approach  
      * Community-driven improvement process  
      * Security-first engineering practices  
      * Pragmatic solution design

  * ### Avalanche Foundation

    * **Definition:**  
      * The [Avalanche Foundation](https://www.avax.network/foundation) is a
      non-profit entity separate from Ava Labs  
      * Focuses on ecosystem advancement and community growth  
      * Does NOT develop the core protocol (that's Ava Labs)  
      * Manages ecosystem funding and development programs  
    * **Actions Performed:**  
      * Manages ecosystem funding programs and grants  
      * Coordinates [network
      governance](Mechanism%20Taxonomy.md#governance-components) initiatives  
      * Supports developer onboarding and education  
      * Oversees [staking delegation
      rewards](Economic%20Taxonomy.md#validator-incentives) program  
      * Facilitates institutional partnerships and adoption  
      * Provides community incentives and rewards  
    * **Value Flows:**  
      * Manages foundation treasury  
      * Distributes ecosystem grants  
      * Provides staking delegation rewards  
      * Funds community infrastructure  
      * Supports ecosystem growth initiatives

  * ### Infrastructure Providers

    * **Definition**  
      * Organizations providing critical network infrastructure  
      * Operate RPC endpoints, indexers, and APIs  
      * Support network reliability and accessibility  
    * **Actions Performed**  
      * Maintain public RPC endpoints  
      * Operate network indexers  
      * Provide API services  
      * Monitor network health  
      * Support developer tools  
    * **Value Flows**  
      * Generate revenue from API services  
      * Receive infrastructure grants  
      * Monetize premium services  
      * Support ecosystem growth  
    * **Preferences**  
      * High service reliability  
      * Scalable infrastructure  
      * Developer-friendly solutions  
      * Sustainable business models  
        

* ## Community Members

  * ### Trader

    * **Definition:**  
      * Market participants who actively trade AVAX tokens  
      * Provide market liquidity and price discovery  
      * Operate across centralized and decentralized exchanges  
      * May engage in various trading strategies  
    * **Actions Performed:**  
      * Execute token trades and swaps  
      * Provide liquidity to trading pools  
      * Monitor market conditions  
      * Analyze price movements  
      * Manage trading positions  
    * **Value Flows:**  
      * **Inflows:**  
        * Trading profits  
        * Liquidity provision fees  
        * Yield farming rewards  
        * Arbitrage opportunities  
      * **Outflows:**  
        * Trading fees and spreads  
        * [Gas costs](Economic%20Taxonomy.md#fee-structure) for transactions  
        * Liquidity pool deposits  
        * Value at risk  
    * **Preferences:**  
      * High market liquidity  
      * Low [trading fees](Economic%20Taxonomy.md#fee-structure)  
      * Price efficiency  
      * Advanced trading tools  
      * Risk/reward optimization

  * ### Investors

    * **Definition:**  
      * Strategic capital providers to the Avalanche ecosystem  
      * Long-term token holders focused on value appreciation  
      * May include both retail and institutional participants  
    * **Actions Performed:**  
      * Conduct due diligence on projects  
      * Deploy capital strategically  
      * Participate in
      [governance](Mechanism%20Taxonomy.md#governance-components)  
      * Support ecosystem growth  
    * **Value Flows:**  
      * **Inflows:**  
        * Token value appreciation  
        * Staking yields  
        * Ecosystem rewards  
        * Investment returns  
      * **Outflows:**  
        * Initial capital deployment  
        * Operating costs  
        * Portfolio management fees  
        * Value at risk  
    * **Preferences:**  
      * Long-term value creation  
      * Network growth and adoption  
      * Strong governance rights  
      * Risk-adjusted returns

      

  * ### App User

    * **Definition:**  
      * End users of applications built on Avalanche  
      * Interact with dApps, DeFi protocols, and services  
      * May or may not hold AVAX tokens directly  
      * Focus on utility and functionality  
    * **Actions Performed:**  
      * Use DeFi applications and protocols  
      * Engage with GameFi and NFT platforms  
      * Execute transactions and swaps  
      * Interact with smart contracts  
      * Access decentralized services  
    * **Value Flows:**  
      * **Inflows:**  
        * Application utility and benefits  
        * Rewards from protocol usage  
        * Service access and features  
        * Yield from DeFi activities  
      * **Outflows:**  
        * [Transaction fees](Economic%20Taxonomy.md#fee-structure)  
        * Service usage costs  
        * Protocol interaction fees  
        * Subscription payments  
    * **Preferences:**  
      * Low [transaction costs](Economic%20Taxonomy.md#fee-structure)  
      * User-friendly interfaces  
      * Fast transaction speeds  
      * Reliable service access  
      * Strong security features

  * ### Developer

    * **Definition**  
      * Builds applications and services on
      [Avalanche](https://docs.avax.network/)  
      * Creates [smart contracts](Mechanism%20Taxonomy.md#evm-c-chain) and
      protocols  
      * Contributes to ecosystem tooling  
      * Innovates new use cases  
    * **Actions Performed**  
      * Develops dApps and protocols  
      * Writes and deploys [smart
      contracts](https://docs.avax.network/dapps/smart-contracts/)  
      * Creates developer tools and [SDKs](https://docs.avax.network/tooling/)  
      * Tests and audits code  
      * Maintains documentation  
    * **Value Flows**  
      * **Inflows**  
        * Development grants  
        * Protocol fees and revenue  
        * Token incentives  
        * Community rewards  
      * **Outflows**  
        * Development costs  
        * Infrastructure expenses  
        * Testing and auditing fees  
        * Marketing and user acquisition  
    * **Preferences**  
      * Strong developer tooling  
      * Clear documentation  
      * Active support channels  
      * Scalable infrastructure  
      * Engaged user community


#### 

## Role Taxonomy Summary

The Avalanche ecosystem comprises a diverse set of actors working together to
maintain, develop, and grow the network. Network Participants, including
[Primary Network Validators](Economic%20Taxonomy.md#validator-incentives), L1
Validators, and [Delegators](Economic%20Taxonomy.md#staking-mechanism), form
the backbone of network security and operations. Development Organizations like
[Ava Labs](https://avalabs.org) and the [Avalanche
Foundation](https://www.avax.network/foundation) provide technical innovation
and ecosystem support, while Infrastructure Providers ensure reliable network
access and tools. Community Members represent various levels of engagement,
from Token Holders who participate in
[governance](Mechanism%20Taxonomy.md#governance-components) to active Traders
managing market dynamics. Investors provide strategic capital and long-term
support, while App Users drive network adoption through daily interactions.
[Developers](https://docs.avax.network/) create applications and tools that
expand ecosystem utility. 

[image1]:
<data:image/png;base64,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>
