---
html: install-cosmovisor.html
parent: evm-sidechains.html
blurb: Install cosmovisor for automated upgrades
labels:
  - Development, Interoperability
status: not_enabled

---

# Install Cosmovisor

[Cosmovisor](https://docs.cosmos.network/main/build/tooling/cosmovisor) is a small process manager for Cosmos SDK application binaries that monitors the governance module for incoming chain upgrade proposals. If it sees a proposal that gets approved, cosmovisor can automatically download the new binary, stop the current binary, switch from the old binary to the new one, and finally restart the node with the new binary.

The following section gives details on how to perform a migration to cosmovisor using docker.

## Backup node data

After performing any important maintenance action such as this one, you should first back up all the node files such as the private keys and the blockchain history. All this data can be found in the folder  `.exrpd` in the root of the node. If you followed the docker installation guide, the folder should be under `~/.exrpd` .

**⚠️ Before continuing, please make sure you have a copy of this entire folder. The most important files are `~/.exrpd/config` and `~/.exrpd/keyring*` .**

## Remove the node container

The first thing we have to do is to stop the docker container running the node. We can list what running containers are in the machine by running `docker ps`

```bash
validator-node:~# docker ps
CONTAINER ID   IMAGE                                COMMAND                  CREATED       STATUS       PORTS                                           NAMES
a2a5c4d97b5b   peersyst/exrp-cosmovisor:latest      "sh -c …"                13 days ago   Up 13 days   0.0.0.0:26656->26656/tcp, :::26656->26656/tcp   validator
```

After seeing the listing containers, we can then stop and remove the container by running `docker kill <container_name>` and `docker rm <container_name>`

```bash
validator-node:~# docker kill validator
validator-node:~# docker rm validator
```

## Initialize the Cosmovisor client

The very first step is to pull the latest cosmovisor image from the docker registry by running `docker pull peersyst/exrp-cosmovisor:latest`

```bash
validator-node:~# docker pull peersyst/exrp-cosmovisor:latest
latest: Pulling from peersyst/exrp-cosmovisor
f56be85fc22e: Already exists 
78134ebb758f: Pull complete 
6e29bafc19de: Pull complete 
ce839fca64c6: Pull complete 
5e741889d497: Pull complete 
182ead5dc398: Pull complete 
60e70e19a85a: Pull complete 
Digest: sha256:fea74e4253b1d4cca78ea15b599a3736cfe99980a78663294ab48603d64dda16
Status: Downloaded newer image for peersyst/exrp-cosmovisor:latest
docker.io/peersyst/exrp-cosmovisor:latest
```

After pulling the docker image, we can initialize the new version by running `docker run --rm -v $HOME/.exrpd:/root/.exrpd peersyst/exrp-cosmovisor:latest initialize`

```bash
validator-node:~# docker run -it --rm -v $HOME/.exrpd:/root/.exrpd peersyst/exrp-cosmovisor:latest initialize
```

After running this command we should see the **cosmovisor** folder created in our node home:
```bash
validator-node:~# ls -la $HOME/.exrpd
total 32
drwxr-xr-x 8 root root 4096 May 22 07:48 .
drwx------ 6 root root 4096 May  9 15:11 ..
drwxr-xr-x 3 root root 4096 May 22 07:46 config
drwxr-xr-x 3 root root 4096 May 22 07:48 cosmovisor
drwx------ 9 root root 4096 May 22 07:47 data
drwx------ 2 root root 4096 Jun  2  2023 keyring-file

validator-node-0:~# ls -la $HOME/.exrpd/cosmovisor/
total 12
drwxr-xr-x 3 root root 4096 May 22 07:50 .
drwxr-xr-x 8 root root 4096 May 22 07:48 ..
lrwxrwxrwx 1 root root   31 May 22 07:50 current -> /root/.exrpd/cosmovisor/genesis
drwxr-xr-x 3 root root 4096 May 22 07:48 genesis
```

## Start the cosmovisor client

The next step after initializing, is to start the cosmovisor client. To do so, we are going to create a new docker container that will use the cosmovisor image by running `docker run -d -p 26656:26656 -v <node_home>:/root/.exrpd peersyst/exrp-cosmovisor:latest cosmovisor run start`

```bash
validator-node:~# docker run -d --name validator -p 26656:26656 -v $HOME/.exrpd:/root/.exrpd peersyst/exrp-cosmovisor:latest cosmovisor run start
```

After we run this command, we can check that the container is running with the `docker ps`  command.

```bash
validator-node:~# docker ps
CONTAINER ID   IMAGE                                COMMAND                  CREATED          STATUS          PORTS                                           NAMES
a2a5c4d97b5b   peersyst/exrp-cosmovisor:latest      "cosmovisor run start"   10 seconds ago   Up 10 seconds   0.0.0.0:26656->26656/tcp, :::26656->26656/tcp   validator
```

And check the logs of the container by running `docker logs --tail 100 -f <container_name>`. After some time we should see usual activity in our node being in sync with the network.

```bash
validator-node:~# docker logs --tail=100 -f validator
6:00PM INF commit synced commit=436F6D6D697449447B5B37392032343020313133203133382035342031373020393320313637203135392031353120313436203136302032313320343720313033203533203130382039372036203737203536203130382039203130322032313120382031333320323033203235302031343320313636203134375D3A3739313234427D
6:00PM INF committed state app_hash=4FF0718A36AA5DA79F9792A0D52F67356C61064D386C0966D30885CBFA8FA693 height=7934539 module=state num_txs=0 server=node
6:00PM INF indexed block exents height=7934539 module=txindex server=node
6:00PM INF Timed out dur=2976.595543 height=7934540 module=consensus round=0 server=node step=1
6:00PM INF received proposal module=consensus proposal={"Type":32,"block_id":{"hash":"1B25046566DDE8C009321B627AB1C0C8CC162CE07D5E77BD5725F8C8FA45FC6F","parts":{"hash":"8BE3F8E82916DBA87A3A63B6C8405FC478440658CA5979EEC8E0574888BE67F0","total":1}},"height":7934540,"pol_round":-1,"round":0,"signature":"l1PaiPtgG8qZxWgHrdyfnXOnWmnKI4fVSPeWQLRvRG/ryumf+N3+M8f5VBDAydJfaE0cOVyiCeBejjDoAw8hDw==","timestamp":"2024-04-23T18:00:34.988182155Z"} server=node
6:00PM INF received complete proposal block hash=1B25046566DDE8C009321B627AB1C0C8CC162CE07D5E77BD5725F8C8FA45FC6F height=7934540 module=consensus server=node
6:00PM INF finalizing commit of block hash={} height=7934540 module=consensus num_txs=0 root=4FF0718A36AA5DA79F9792A0D52F67356C61064D386C0966D30885CBFA8FA693 server=node
```