# Overview

Operating a node on XRPL EVM is integral to maintaining the network’s security, performance, and reliability. Whether you’re running an API node for developer-facing infrastructure, a seed node to help peers find each other, or serving as a validator, you’re helping build the backbone of the XRPL EVM ecosystem. This section introduces the different types of nodes, outlines the role of validators within the Proof of Authority (PoA) consensus mechanism, and provides guidance on how to join and participate in network governance.

## Node Types and Their Roles

The XRPL EVM network consists of multiple node types, each serving distinct yet complementary purposes. Understanding these node types will help you choose which configuration aligns with your goals and resources.

1. **API Nodes:**  
   API nodes provide endpoints that developers and users can interact with. They’re often optimized for quick responses, high availability, and scalability. Running an API node helps dApp developers, wallets, explorers, and other services access on-chain data and submit transactions without needing to run their own infrastructure.

2. **Seed Nodes:**  
   Seed nodes are the first contact points for new nodes joining the network. They maintain a list of peers and help new nodes discover other participants in the network. By running a seed node, you facilitate smoother network onboarding and ensure a robust peer-to-peer topology.

3. **Validator Nodes:**  
   Validators are the core decision-makers in the XRPL EVM network. They propose, validate, and finalize blocks, helping secure the chain and maintain its integrity. Unlike Proof of Stake or Proof of Work systems, XRPL EVM’s Proof of Authority model requires validators to be approved through a governance process. Validator operators must maintain high-uptime nodes, meet hardware and security requirements, and commit to the network’s best interests.

4. **Archive Nodes:**  
   Archive nodes store the entire chain’s historical data, including all blocks and states since the genesis block. These nodes are invaluable for research, historical analysis, compliance, and for any application that requires deep historical queries. Archive nodes typically require more storage and stable hardware configurations.

## Consensus and Proof of Authority

XRPL EVM employs a Proof of Authority (PoA) consensus mechanism. In this model, known and trusted entities (validators) run nodes that propose and validate new blocks. Since validators must be identified and endorsed through a governance process, PoA networks often have lower resource requirements and faster block times than permissionless systems—while still retaining a level of decentralization and fault tolerance.

### Key Properties of PoA on XRPL EVM

- **Validator Selection:**  
  New validators are added through a governance vote. This ensures that only entities with a track record of reliability, security, and community trust are allowed to participate in block validation.

- **Stability & Performance:**  
  With fewer, well-known validators, XRPL EVM can achieve high throughput, low-latency block production, and predictable finality times.

- **Governance-Driven Evolution:**  
  Because validators are chosen through governance, changes to validator sets, protocol upgrades, and network parameter adjustments are guided by a collective decision-making process, ensuring changes are deliberate and community-driven.

## Economic Model and Incentives

The XRPL EVM network’s primary currency is **XRP**, the digital asset native to the XRP Ledger ecosystem. XRP serves multiple roles, including transaction fees and cross-chain liquidity. While validators in PoA systems are often chosen for their reputational value and commitments to network growth, operational incentives and fee structures may evolve over time to reward validators for their contributions to the network’s stability and accessibility.

## Getting Started as an Operator

1. **Select Your Node Type:**  
   Determine which node type best suits your objectives. If you’re providing data to dApps, an API node may be ideal. If you want to help the network scale and ensure reliable peer discovery, consider running a seed node. For contributing directly to consensus, focus on becoming a validator.

2. **Set Up Infrastructure:**  
   Provision reliable hardware and networking resources. Each node type has different requirements, but all benefit from stable internet connections, redundant storage solutions, and robust security measures.

3. **Follow the Guides:**  
   This documentation provides step-by-step instructions, best practices, and maintenance tips for each node type. You’ll find information on installation, configuration, upgrades, and troubleshooting.

4. **Join the Community & Governance Processes:**  
   Engage with the XRPL EVM community by joining forums, participating in governance proposals, and contributing to network discussions. If you plan to become a validator, understanding the governance framework is essential to actively participate in block production and protocol evolution.

## Next Steps

When you’re ready to get started, head over to our [Getting Started](./getting-started/installing-the-node.md) section. There, you’ll find detailed information about:

- **System Requirements:** Understand what kind of hardware and network specifications are optimal for running different node types.
- **Installing the `exrpd` Binary:** Learn how to download, install, and configure the XRPL EVM node software to begin participating in the network.

As you progress through these steps, you’ll acquire the foundational knowledge and infrastructure setup needed to operate confidently within the XRPL EVM ecosystem.
