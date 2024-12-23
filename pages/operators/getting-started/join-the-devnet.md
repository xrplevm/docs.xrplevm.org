# Join the Devnet

Now that you have successfully installed the `exrpd` binary, it’s time to take the next steps and fully connect to the XRPL EVM Devnet. In this section, you’ll learn how to initialize your node configuration, download the correct genesis file, and set up peer connections so your node can begin synchronizing with the network.

By following these instructions, you will ensure that your node is properly configured and ready to start participating in the Devnet—verifying transactions, maintaining state, and providing the foundation you need for subsequent testing, development, and experimentation.

## Prerequisites

> **Note**: Make sure the [exrpd is installed](./installing-the-node.md).

## Configure the Node
Once you have the `exrpd` binary installed, you need to initialize and configure the node. This involves generating initial configuration files, downloading the appropriate genesis file, and establishing connections to network peers.

### Initialize the node
Initializing your node creates the required configuration files, including validator keys and a default configuration structure. The `<moniker>` is a human-readable name you assign to your node (often the name of your organization or a recognizable identifier), and `<chain-id>` specifies the target network.

```bash
exrpd init <moniker> --chain-id <chain-id>
```
Replace `<moniker>` with a name for your node and `<chain-id>` with the correct chain ID for the network you are joining. After running this command, the necessary configuration and key files will be generated in the `~/.exrpd` directory.

### Download genesis file
The `genesis.json` file defines the initial state of the network. It’s critical that your node uses the same genesis file as the rest of the network to synchronize properly.

```bash
wget https://raw.githubusercontent.com/Peersyst/xrp-evm-archive/main/poa-devnet/genesis.json -O ~/.exrpd/config/genesis.json
exrpd validate-genesis
```

If the validation succeeds without errors, your genesis file is correctly set up.

### Add Peers

our node needs to connect to other nodes (peers) to synchronize and participate in the network. Persistent peers are nodes to which your instance will attempt to maintain ongoing connections.
1. Retrieve a list of available peers from the [XRPL EVM archive repository](https://raw.githubusercontent.com/Peersyst/xrp-evm-archive/main/poa-devnet/peers.txt).
2. Update the `persistent_peers` field in `~/.exrpd/config/config.toml`:

```bash
PEERS=`curl -sL https://raw.githubusercontent.com/Peersyst/xrp-evm-archive/main/poa-devnet/peers.txt | sort -R | head -n 10 | awk '{print $1}' | paste -s -d, -`
sed -i.bak -e "s/^persistent_peers *=.*/persistent_peers = \"$PEERS\"/" ~/.exrpd/config/config.toml
cat ~/.exrpd/config/config.toml | grep persistent_peers
```
### Advanced Configuration Options
If you need to fine-tune your node beyond the basic setup (e.g., adjusting database backends, logging levels, or network timeouts), refer to the [Advanced Configuration section](../advanced/node-configuration-options.md). There, you’ll find detailed guidance on customizing your node’s behavior to better suit your infrastructure and operational requirements.

## Synchronize the Node

To quickly get started, node operators can choose to sync by downloading a snapshot from a well-known contributor. For more advanced information on setting up a node, see the [Sync Options section](../advanced/sync-options.md)

**Note**: Make sure to set the `--home` flag when initializing and starting `exrpd` if mounting snapshot data externally.

### Download the latest snapshot

Node Operators can decide how much of historical state they want to preserve by choosing between `Pruned`, `Default`, and `Archive`. See the [Snapshots page](../resources/snapshots.md) for up-to-date snapshot sizes.

###### Default

```bash=
sudo apt-get install wget liblz4-tool aria2 jq -y

export URL=`curl -L https://quicksync.io/cosmos.json|jq -r '.[] |select(.file=="cosmoshub-4-default")|.url'`

echo $URL

cd $HOME/.gaia

aria2c -x5 $URL
```

###### Pruned

```bash=
sudo apt-get install wget liblz4-tool aria2 jq -y

export URL=`curl -L https://quicksync.io/cosmos.json|jq -r '.[] |select(.file=="cosmoshub-4-pruned")|.url'`

echo $URL

cd $HOME/.gaia

aria2c -x5 $URL
```

###### Archive

```bash=
sudo apt-get install wget liblz4-tool aria2 jq -y

export URL=`curl -L https://quicksync.io/cosmos.json|jq -r '.[] |select(.file=="cosmoshub-4-archive")|.url'`

echo $URL

cd $HOME/.gaia

aria2c -x5 $URL
```

**The download logs should look like the following**

```
01/11 07:48:17 [NOTICE] Downloading 1 item(s)
[#7cca5a 484MiB/271GiB(0%) CN:5 DL:108MiB ETA:42m41s]
```

**Completed Download Process:**

```
[#7cca5a 271GiB/271GiB(99%) CN:1 DL:77MiB]
01/11 08:32:19 [NOTICE] Download complete: /mnt/quicksync_01/cosmoshub-4-pruned.20220111.0310.tar.lz4

Download Results:
gid   |stat|avg speed  |path/URI
======+====+===========+=======================================================
7cca5a|OK  |   105MiB/s|/mnt/quicksync_01/cosmoshub-4-pruned.20220111.0310.tar.lz4

Status Legend:
(OK):download completed.
```

##### Unzip

```bash
lz4 -c -d `basename $URL` | tar xf -
```

##### Copy Address Book Quicksync

```bash
curl https://quicksync.io/addrbook.cosmos.json > $HOME/.gaia/config/addrbook.json
```

##### Start Gaia

```bash
gaiad start --x-crisis-skip-assert-invariants

```