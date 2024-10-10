---
html: run-and-synchronize-your-node.html
parent: evm-sidechains.html
blurb: Learn how to run and synchronize the XRPL EVM Sidechain Devnet node.
labels:
- Syncing, Development
status: not_enabled
---

# Run and Synchronize your node

This tutorial walks you through the steps to sync the **XRP Ledger EVM Sidechain Devnet**.

## Syncing Options

### Syncing from Genesis

Synchronization from genesis involves starting your node from the very first block of the blockchain and processing all transactions to reach the current state. This method ensures your node has the complete history of the blockchain and is fully up-to-date with all network changes and upgrades.

#### Why Sync from Genesis?

- Ensures your node has the complete transaction history.
- Verifies all past network upgrades and hard forks.
- Essential for participating in the network as a full node or validator.

#### Chain Upgrades

To keep your node up-to-date, you need to update the binaries whenever a hard fork occurs. Below is a table indicating all the hard forks for each network:

<embed src="/snippets/_evm-sidechain-upgrades-table.md" />

#### Steps to Sync from Genesis

1. Ensure your node is initialized and configured as per the [Installation Guide](install-evm-sidechain-devnet.html).
2. Start the node with the initial binary version:
    ```bash
    exrpd start
    ```
3. Monitor the logs for any errors related to hard forks or network upgrades. When an error like the following happens, update the binary to the next version and repeat step 2 as needed until the node is fully synced with the latest version.
    ```text
7:58AM INF Replay last block using real app module=consensus server=node
7:58AM ERR UPGRADE "v2.0.0" NEEDED at height: 8912879: {"binaries":{"linux/amd64":"https://github.com/Peersyst/exrp/releases/download/v2.0.0/exrp_2.0.0_Linux_amd64.tar.gz","linux/arm64":"https://github.com/Peersyst/exrp/releases/download/v2.0.0/exrp_2.0.0_Linux_arm64.tar.gz","darwin/amd64":"https://github.com/Peersyst/exrp/releases/download/v2.0.0/exrp_2.0.0_Darwin_amd64.tar.gz","darwin/arm64":"https://github.com/Peersyst/exrp/releases/download/v2.0.0/exrp_2.0.0_Darwin_arm64.tar.gz"}}
panic: UPGRADE "v2.0.0" NEEDED at height: 8912879: {"binaries":{"linux/amd64":"https://github.com/Peersyst/exrp/releases/download/v2.0.0/exrp_2.0.0_Linux_amd64.tar.gz","linux/arm64":"https://github.com/Peersyst/exrp/releases/download/v2.0.0/exrp_2.0.0_Linux_arm64.tar.gz","darwin/amd64":"https://github.com/Peersyst/exrp/releases/download/v2.0.0/exrp_2.0.0_Darwin_amd64.tar.gz","darwin/arm64":"https://github.com/Peersyst/exrp/releases/download/v2.0.0/exrp_2.0.0_Darwin_arm64.tar.gz"}}
    ```

### Syncing from Snapshot

Syncing from a snapshot involves downloading a recent state of the blockchain, allowing your node to catch up quickly without processing the entire history from the genesis block.

#### Steps to Sync from Snapshot

1. Download a snapshot from a provider that you trust:

| Provider | Type   | Current size | Snapshot URL                                                          |
|----------|--------|--------------|-----------------------------------------------------------------------|
| Peersyst | Pruned | >100GB       | https://evm-sidechain-snapshots-devnet.s3.amazonaws.com/exrpd.tar.lz4 |

2. Extract the snapshot to the `data` directory:
    ```bash
    tar -xzf exrpd.tar.gz -C ~/.exrpd/data
    ```
3. Start the node:
    ```bash
    exrpd start
    ```