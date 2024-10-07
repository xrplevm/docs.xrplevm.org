---
html: bridges-intro.html
blurb: Introduction to bridges for the EVM compatible XRP Ledger Sidechain.
labels:
  - Interoperability
status: not_enabled
---
# Axelar

<!-- <embed src="/snippets/_axelar-disclaimer.md" /> -->

Bridges are mechanisms that connect two blockchains together, enabling interoperability between the two. This connection enables users to transfer data or digital assets across separate blockchains that may have different protocols, consensus mechanisms, and other underlying technologies.

<!-- Amendment draft XLS-38d introduces bridges to the XRP Ledger. To learn more about the specifics of the XRPL bridge implementation, see: [XLS-38d-XChainBridge](https://github.com/XRPLF/XRPL-Standards/tree/master/XLS-38d-XChainBridge). -->

Bridging XRP from XRPL ledger to XRPL EVM Sidechain is currently supported by the [Axelar Network](https://axelar.network/). Axelar is a secure cross-chain communication network for Web3, enabling you to build Interchain dApps that grow beyond a single chain. Secure means Axelar is built on proof-of-stake, the battle-tested approach used by Ethereum, Polygon, Cosmos, and more.


## Intergration Overview

The integration of the Axelar Network as a bridge for native token transfers between the XRPL Ledger and the XRPL EVM Sidechain blockchains enables seamless interoperability across these distinct blockchain environments. Axelar functions as a cross-chain communication layer, facilitating secure, permissionless transfers of native assets without the need for intermediaries or wrapped tokens.

By leveraging Axelar's decentralized network of validators and robust message-passing protocol, assets can move between the XRPL's native ledger and its EVM-compatible sidechain with full transactional consistency. This integration allows for expanded use cases, such as decentralized finance (DeFi) applications and cross-chain liquidity solutions, by bridging the gap between the XRPL's high-throughput, low-cost transactions and the programmable smart contract capabilities of the EVM ecosystem.


For further details on the implementation of the Axelar bridge on the XRPL EVM sidechain, see: 

- [Axelar Architecture](axelar-architecture.md): Learn more about the architecture of the Axelar bridge.
- [Axelar Interchain Transfer](axelar-interchain-transfer.md): Learn more about Axelar interchain transfer.
- [Axelar General Message Passing (GMP)](axelar-general-message-passing.md): Learn more about Axelar general message passing.
- [Deployed Contracts](axelar-deployed-contracts.md): List of deployed contracts on the XRPL EVM Sidechain networks.