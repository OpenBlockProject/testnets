# Moxy Testnet Instructions

## TLDR
Block explorer:

Binaries: 

Genesis file: [genesis.json](https://github.com/OpenBlockProject/testnets/blob/main/moxy/genesis.json)

Seeds:

## Minimum hardware requirements
* 1GB RAM
* 25GB of disk space
* 1.4 GHz CPU

## Software Requirements
Moxy has releases for Linux and MacOS [here](https://github.com/OpenBlockProject/openblockchain/releases/tag/latest)

## Install Moxy
You can install Moxy by downloading the binary (easiest) or compiling from source.

### Option 1: Download binary
1. Download the binary for your platform: [releases](https://github.com/OpenBlockProject/openblockchain/releases/tag/latest).
2. Copy it to a location in your PATH, i.e: ```/usr/local/bin``` or ```$HOME/bin```

i.e.:
```
TBD
```
### Option 2: Clone from source

## Initialize Node
Use openblockchaind to initialize your node (replace the ```NODE_NAME``` with a name of your choosing):
```
openblockchaind init NODE_NAME --chain-id=moxy
```
Open the config.toml to edit the seeds and persistent peers.
```
cd $HOME/.openblockchaind/config
nano config.toml
```
Use page down or arrow keys to get to the line that says seeds = "" and replace it with the following:
```
seeds = "(seeds TBD)"
```
Next, add persistent peers:
```
persisent_peers: "(peers TBD)"
```
## Set up Cosmovisor
Set up Cosmovisor to ensure future upgrades happen flawlessly.  To install:
```
go install github.com/cosmos/cosmos-sdk/cosmovisor/cmd/cosmovisor@v1.0.0
```
Create the required directories:
```
mkdir -p ~/.openblockchaind/cosmovisor
mkdir -p ~/.openblockchaind/cosmovisor/genesis
mkdir -p ~/.openblockchaindd/cosmovisor/genesis/bin
mkdir -p ~/.openblockchaind/cosmovisor/upgrades
```
Set the environment variables:
```
echo "# Setup Cosmovisor" >> ~/.profile
echo "export DAEMON_NAME=openblockchaind" >> ~/.profile
echo "export DAEMON_HOME=$HOME/.openblockchaind" >> ~/.profile
echo "export DAEMON_ALLOW_DOWNLOAD_BINARIES=false" >> ~/.profile
echo "export DAEMON_LOG_BUFFER_SIZE=512" >> ~/.profile
echo "export DAEMON_RESTART_AFTER_UPGRADE=true" >> ~/.profile
echo "export UNSAFE_SKIP_BACKUP=true" >> ~/.profile
source ~/.profile
```
Download and replace the genesis file (TBD):
```
cd $HOME/.openblockchaind/config
(TBD)
```
Copy the current openblockchaind binary into the cosmovisor/genesis folder:
```
cp $GOPATH/bin/openblockchaind ~/.openblockchaind/cosmovisor/genesis/bin
```
To check your work, ensure the version of cosmovisor and openblockchaind are the same:
```
cosmovisor version
openblockchaind version
```
Reset private validator file to genesis state:
```
openblockchaind unsafe-reset-all
```
## Download Chain Data
(TBD)
