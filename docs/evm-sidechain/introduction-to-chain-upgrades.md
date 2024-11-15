---
html: introduction-to-chain-upgrades.html
parent: evm-sidechains.html
blurb: Learn about XRPL EVM Sidechain upgrades.
labels:
  - Development, Interoperability
status: not_enabled
---

# Introduction to chain upgrades

Blockchain upgrades are a complex process that requires all network participants to agree on a specific time to execute a specific change in the protocol. Cosmos based networks, like the XRPL EVM Sidechain, solve this complexity with a set of fixed operations that need to happen when  upgrading the chain:

1. A governance proposal containing a chain upgrade transaction is created. This transaction contains specific details of the upgrade such as which block will the upgrade be executed, the version number and some metadata.
2. Once the proposal is created it is voted as another regular governance proposal.
3. If the proposal collects enough votes to be approved, the chain upgrade is planned at the block specified.
4. When the block of the upgrade is minted, all the nodes, that are running the old version will halt, showing an error in the logs notifying the operator to upgrade it to the new binary.
5. After more than 2/3 of the total validators upgrade their nodes, the chain starts creating new blocks. And the upgrade has finished successfully.

## List of upgrades
Below is a table indicating all the hard fork upgrades for each network:

{% partial file="/snippets/_evm-sidechain-upgrades-table.md" /%}

## Automated upgrades

In order to automate the manual actions required by node operators during the chain upgrades, we have integrated Cosmovisor. This client automatically detects new binaries for newer versions available and downloads them. Once a new chain upgrade is triggered, the cosmovisor restarts the node with the new binary, reducing the downtime of your node.

Read more in the next section [Install Cosmovisor](install-cosmovisor.md)