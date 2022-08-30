# Guide on how to prepare a staking machine for the Merge

[The Merge](https://ethereum.org/en/upgrades/merge/) is a protocol upgrade that is being rolled out on all Ethereum networks being kept around. This procotol upgrade will be rolled out on Mainnet. Ethereum validators will need to take some measures and some actions to make sure their staking machine will work during this upgrade and that they will keep running well after the upgrade. Tests are already underway and [the Merge upgrade has been applied to testnets](https://wenmerge.com/) already.

This guide is meant for people who are managing and maintaining staking machines. It will explain which steps or actions you should take in order to be ready for the Merge.

# Ethereum client updates are mandatory for the Merge on Mainnet

Here are the clients that are ready for the merge on Mainnet and their version. You **must** update your clients to these versions or later before [the Merge on Mainnet](https://blog.ethereum.org/2022/08/12/finalized-no-36/). You **must** update your clients before **September 6th 2022 at 11:34:47am UTC**.

#### Execution clients that are ready for the Merge on Mainnet

- [Geth](https://geth.ethereum.org/): v1.10.23 (or later)
- [Nethermind](http://nethermind.io/): v1.14.0 (or later)
- [Besu](https://hyperledger.org/use/besu): v22.7.1 (or later)
- [Erigon](https://github.com/ledgerwatch/erigon#erigon): v2022.08.03-alpha (or later)

#### Consensus clients that are ready for the Merge on Mainnet

- [Teku](https://consensys.net/knowledge-base/ethereum-2/teku/): v22.8.1 (or later)
- [Lighthouse](https://lighthouse.sigmaprime.io/): v3.0.0 (or later)
- [Prysm](https://prysmaticlabs.com/): v3.0.0 (or later)
- [Nimbus](https://nimbus.team/): v22.8.0 (or later)
- [Lodestar](https://lodestar.chainsafe.io/): v1.0.0 (or later)

## Why would you want to prepare for the Merge?

There are some risks your staking machine will stop performing its duties if you are not well prepared. There are some risks your Ethereum validator will miss some rewards if you are not well prepared.

## When is the Merge going to happen on Mainnet?

The Merge on Mainnet is happening in [a few different steps](https://blog.ethereum.org/2022/08/12/finalized-no-36/#%EF%B8%8F-all-hands-on-deck-%EF%B8%8F). The first one will happen on **September 6th 2022 at 11:34:47am UTC**. It's a fork called Bellatrix to prepare for the Merge. The final and definitive step will happen around **September 15th 2022**. The uncertainty around the exact date and time depends in part on the current miners and the overall Ethereum network hash rate.

Make sure to follow [the official Ethereum blog](https://blog.ethereum.org/) and watch for announcements there. You can also subscribe to [this newsletter](https://groups.google.com/u/1/a/ethereum.org/g/announcements).

## Overview

1. Make sure you are running your own execution client.
2. Make sure your Ethereum clients are updated.
3. Make sure you are using the new configuration options for your Ethereum clients.
4. Make sure you have a configured JWT token file for the engine API.
5. Make sure you have a configured fee recipient address.
6. Make sure you have a configured MEV solution if you want one.

## Running your own execution client

Running your own execution client is going to be required after the Merge for an Ethereum validator. Some Ethereum validators are entirely relying on public infrastructure like Infura or Alchemy for their execution data. If you are in this case, you will need to install and configure your own execution client.

If you are running your own execution client and using a public infrastructure provider as a fallback endpoint, that fallback endpoint will not work after the merge. Using multiple execution clients after the Merge is going to be slightly more complex. This is out of scope for this guide.

The 2 main concerns for an Ethereum validator when running your own execution client is disk usage and bandwidth usage.

### Installing and configuring a new execution client

If you are not currently running your own execution client and if you used a guide or a tool to setup your staking machine, you should first check to see if that guide or tool has a section on how to setup an execution client. If you don't know where to start, check out [the client setup tools and guides](https://ethereum.org/en/staking/solo/#node-and-client-tools). [Our support](#support) can also help you here.

Syncing an execution from nothing can take a few hours or a few days. Make sure to install and configure your execution client at least a week before the Merge to be safe.

### Managing your execution client disk usage

It is not uncommon for an execution client to use more than 650GB to store its data on Mainnet. If your disk size is less than 2TB for storing everything, you should consider migrating and replacing that disk with one which is at least 2TB in size. You could possibly still manage to run an effective Ethereum validator with only a 1TB disk but that is going to require a lot of efforts which might not be worth it for the price difference of a new disk. Alternatives include adding another a new disk to your machine if it has an available slot or running your execution client on another machine on your local network. Make sure to get in touch with [our support](#support) if you are interested in those alternatives.

Pruning your execution client database is a good strategy for managing your execution client disk usage. If you are using Geth, [you should prune it regularly](https://gist.github.com/yorickdowne/3323759b4cbf2022e191ab058a4276b2) and you should prune it just before the Merge. Geth currently only offers offline prunning that takes a few hours to complete. You should know that having an offline execution client after the Merge will result in your validator failing to perform all its duties meaning that you will lose rewards during that time.

Other execution clients have different strategies for managing data growth. Some are leaner in terms of disk size usage to get started with and some include automatic online pruning. You should consider running [a minority execution client](#execution-client-diversity).

I suggest you implement [monitoring](monitoring.md) and [alerting](alerting.md) to help you find out when you are low on available disk space.

### Managing your execution client bandwidth usage

An execution client will use a lot of bandwidth. Reducing the number of peers is one way of reducing bandwidth usage. It comes with some risks and the con of potentially being out of sync at the wrong time and making your Ethereum validator lose some rewards. The default configuration option for the number of peers should be your baseline value.

### Execution client diversity

Geth is currently the supermajority execution client. It is used to build almost all blocks right now. This is not currently a big issue but it will become one after the Merge. You should consider running [a minority execution client](https://clientdiversity.org/). We have some great execution clients that work well for an Ethereum validator that should be considered:

- [Erigon](https://github.com/ledgerwatch/erigon#erigon) ([Discord](https://github.com/ledgerwatch/erigon#erigon-discord-server))
- [Besu](https://hyperledger.org/use/besu) ([Discord](https://discord.com/invite/hyperledger))
- [Nethermind](http://nethermind.io/) ([Discord](https://discord.com/invite/PaCMRFdvWT))

## Updating your Ethereum clients

There are new specification changes that were added recently that will be needed for the Merge. If you have not updated your Ethereum clients regularly, you will need to update them before the Merge.

If you used a guide or a tool to setup your staking machine, you should first check out with that guide or tool on how you can update your Ethereum clients. If they don't have any section on how to do it, you can check with each client or get touch with [our support](#support).

### Execution clients

- [Geth](https://geth.ethereum.org/) ([Discord](https://discord.com/invite/nthXNEv))
- [Erigon](https://github.com/ledgerwatch/erigon#erigon) ([Discord](https://github.com/ledgerwatch/erigon#erigon-discord-server))
- [Besu](https://hyperledger.org/use/besu) ([Discord](https://discord.com/invite/hyperledger))
- [Nethermind](http://nethermind.io/) ([Discord](https://discord.com/invite/PaCMRFdvWT))

### Consensus clients

- [Prysm](https://prysmaticlabs.com/) ([Discord](https://discord.gg/YMVYzv6))
- [Nimbus](https://nimbus.team/) ([Discord](https://discord.gg/qnjVyhatUa))
- [Lodestar](https://lodestar.chainsafe.io/) ([Discord](https://discord.gg/yjyvFRP))
- [Teku](https://consensys.net/knowledge-base/ethereum-2/teku/) ([Discord](https://discord.gg/9mCVSY6))
- [Lighthouse](https://lighthouse.sigmaprime.io/) ([Discord](https://discord.gg/cyAszAh))

## Using the new configuration options for your Ethereum clients

The communication between your consensus client and your execution client is going to change with the Merge. They will use this [new Engine API](https://github.com/ethereum/execution-apis/tree/main/src/engine) which will be served at a port independant from the JSON-RPC API currently in use.

You are likely going to need to use a new configuration option for this endpoint or at least update it on your consensus client beacon node. The default port for the Engine API is 8551 and the default port for the JSON-RPC API is 8545. You might not need to change any configuration option on your execution client, but you will likely need to modify your beacon node configuration. Here are the common values you will likely need to add or modify for each consensus client assuming your execution client engine API endpoint is at `http://localhost:8551`:

- Prysm beacon node: `--execution-endpoint http://localhost:8551`
- Nimbus: `--web3-url=http://localhost:8551`
- Lodestar beacon node: `--execution.urls http://localhost:8551`
- Teku: `--ee-endpoint http://localhost:8551`
- Lighthouse beacon node: `--execution-endpoint http://localhost:8551`

As usual, when changing the configuration for your consensus client, you will need to reload this configuration and probably restart the client.

## Configuring a JWT token file

The new Engine API used to communicate between the execution client and the consensus client requires [authentication](https://github.com/ethereum/execution-apis/blob/main/src/engine/authentication.md) which is provided with a JWT token stored in a file. There are various ways to configure this. Here is a simple one.

### Creating the JWT token file

Create a JWT token file in a neutral location and make it readable to everyone. We will use the `/var/lib/ethereum/jwttoken` location to store the JWT token file.

```
$ sudo mkdir -p /var/lib/ethereum
$ openssl rand -hex 32 | tr -d "\n" | sudo tee /var/lib/ethereum/jwttoken
$ sudo chmod +r /var/lib/ethereum/jwttoken
```

### Configure your execution client to use the JWT token file

Each execution client will need a different configuration option for the JWT token file. Here are the common values:

- Geth: `--authrpc.jwtsecret /var/lib/ethereum/jwttoken`
- Erigon: `--authrpc.jwtsecret /var/lib/ethereum/jwttoken`
- Besu: `--engine-jwt-secret=/var/lib/ethereum/jwttoken`
- Besu on mainnet: `--engine-rpc-enabled --engine-jwt-secret=/var/lib/ethereum/jwttoken`
- Nethermind: `--JsonRpc.JwtSecretFile=/var/lib/ethereum/jwttoken`

As usual, when changing the configuration for your execution client, you will need to reload this configuration and probably restart the client.

> Besu requires `--engine-rpc-enabled` when no TTD has been configured for the network. Once mainnet has an announced TTD, this flag is no longer necessary

### Configure your consensus client to use the JWT token file

- Prysm beacon node: `--jwt-secret /var/lib/ethereum/jwttoken`
- Nimbus: `--jwt-secret=/var/lib/ethereum/jwttoken`
- Lodestar beacon node: `--jwt-secret /var/lib/ethereum/jwttoken`
- Teku: `--ee-jwt-secret-file /var/lib/ethereum/jwttoken`
- Lighthouse beacon node: `--execution-jwt /var/lib/ethereum/jwttoken`

As usual, when changing the configuration for your consensus client, you will need to reload this configuration and probably restart the client.

## Configuring your fee recipient address

After the Merge, validators will replace miners in building blocks and getting the associated rewards. The validators will receive the tips from each included transaction on their proposed block. For this, they will need to configure a fee recipient address. This will represent the address where tips are sent to when your validator propose a block. Those fees will be available right away for any transaction.

This address can be configured at different layers depending on which client you are using. It can be at the execution client layer, at the consensus beacon node layer, it can be at the consensus validator client layer and it can even be for each different validator key. Here are the common values to configure this on the consensus client. Make sure to replace the `0x0000000000000000000000000000000000000000` address with your own Ethereum address that you control where you want to receive the transaction tips.

- Prysm: `--suggested-fee-recipient 0x0000000000000000000000000000000000000000`
- Nimbus: `--suggested-fee-recipient=0x0000000000000000000000000000000000000000`
- Lodestar validator: `--suggestedFeeRecipient 0x0000000000000000000000000000000000000000`
- Teku: `--validators-proposer-default-fee-recipient=0x0000000000000000000000000000000000000000`
- Lighthouse: `--suggested-fee-recipient 0x0000000000000000000000000000000000000000`

As usual, when changing the configuration for your consensus client, you will need to reload this configuration and probably restart the client.

There are some privacy implications in using a fee recipient address. That address will be forever linked with your validator when it proposes a block after the Merge. If you want to maximize your privacy, you should use your validator deposit address as your fee recipient address if you still have control over it since it is already linked with your validator.

Here are the detailed configuration options for the fee recipient for each client and their documentation.

- [Prysm](https://docs.prylabs.network/docs/execution-node/fee-recipient)
- [Nimbus](https://nimbus.guide/suggested-fee-recipient.html)
- [Lodestar](https://chainsafe.github.io/lodestar/usage/validator-management/#configuring-the-fee-recipient-address)
- [Teku](https://docs.teku.consensys.net/en/latest/HowTo/Prepare-for-The-Merge/#configure-the-fee-recipient)
- [Lighthouse](https://lighthouse-book.sigmaprime.io/suggested-fee-recipient.html)

## Choosing and configuring an MEV solution

[Maximal extractable value (MEV)](https://ethereum.org/en/developers/docs/mev/) refers to the maximum value that can be extracted from block production in excess of the standard block reward and gas fees by including, excluding, and changing the order of transactions in a block. After the Merge, there will be an opportunity for Ethereum validators to get that value. If you want to get that value, you will need to install some additional software and configure your consensus client [to communicate with that software](https://github.com/flashbots/mev-boost/#mev-boost) when the time comes to propose a block.

A preview of MEV and mev-boost can be seen on https://youtu.be/sZYJiLxp9ow

### What about MEV on Mainnet?

You should wait until public relays are published before trying to install and configure any MEV solution for Mainnet. We suggest you try it on Goerli/Prater in the meantime.

### Installing mev-boost on Goerli/Prater

Install [a recent version of Go](https://go.dev/doc/install). [Go is also available](https://go.dev/dl/) for architectures that are different than linux AMD64. Adjust if needed.

```console
$ cd ~
$ wget https://go.dev/dl/go1.19.linux-amd64.tar.gz
$ sudo rm -rf /usr/local/go && sudo tar -C /usr/local -xzf go1.19.linux-amd64.tar.gz
$ export PATH=$PATH:/usr/local/go/bin
$ echo 'PATH="$PATH:/usr/local/go/bin"' >> ~/.profile
$ rm go1.19.linux-amd64.tar.gz
```

Create a user account for the service to run under. This account will not be able to log into the machine. It will only be used to run the service.

```console
$ sudo useradd --no-create-home --shell /bin/false mevboost
```

Install mev-boost globally.

```console
$ CGO_CFLAGS="-O -D__BLST_PORTABLE__" go install github.com/flashbots/mev-boost@latest
$ sudo cp ~/go/bin/mev-boost /usr/local/bin
$ sudo chown mevboost:mevboost /usr/local/bin/mev-boost
```

Create a systemd service file to store the service config which tells systemd to run mev-boost as the mevboost user.

```console
$ sudo nano /etc/systemd/system/mevboost.service
```

Paste the following into the file to run mev-boost on Goerli. Exit and save once done (`Ctrl` + `X`, `Y`, `Enter`).

```ini
[Unit]
Description=mev-boost (Goerli)
Wants=network-online.target
After=network-online.target

[Service]
Type=simple
User=mevboost
Group=mevboost
Restart=always
RestartSec=5
ExecStart=mev-boost \
    -goerli \
    -relay-check \
    -relays https://0xafa4c6985aa049fb79dd37010438cfebeb0f2bd42b115b89dd678dab0670c1de38da0c4e9138c9290a398ecd9a0b3110@builder-relay-goerli.flashbots.net,https://0x821f2a65afb70e7f2e820a925a9b4c80a159620582c1766b1b09729fec178b11ea22abb3a51f07b288be815a1a2ff516@bloxroute.max-profit.builder.goerli.blxrbdn.com

[Install]
WantedBy=multi-user.target
```

Reload systemd to reflect the changes.

```console
$ sudo systemctl daemon-reload
```

And then start the service with the following command and check the status to make sure it’s running correctly.

```console
$ sudo systemctl start mevboost
$ sudo systemctl status mevboost
```

If you did everything right, it should say active (running) in green. If not then go back and repeat the steps to fix the problem. Press Q to quit.
Lastly, enable mev-boost to start on boot.

```console
$ sudo systemctl enable mevboost
```

### Configure your consensus and validator client to use mev-boost

Add this flag to the `ExecStart` of your consensus client and, if needed, validator client service. Note that client flags can be in flux
through August 2022. When in doubt consult each client's `--help`.

- Prysm consensus: `--http-mev-relay=http://127.0.0.1:18550`
- Prysm validator: `--enable-builder`
- Nimbus combined: `--payload-builder=http://127.0.0.1:18550`
- Lodestar consensus: `--builder --builder.urls http://127.0.0.1:18550`
- Lodestar validator: `--builder`
- Teku combined: `--validators-builder-registration-default-enabled=true --builder-endpoint=http://127.0.0.1:18550`
- Lighthouse consensus: `--builder http://127.0.0.1:18550` 
- Lighthouse validator: `--builder-proposals`

Tell systemd you made the changes: `sudo systemctl daemon-reload`

And restart the service(s) you changed: `sudo systemctl restart SERVICENAME`

### Update mev-boost

When a new version is released, you can update mev-boost.

```console
$ CGO_CFLAGS="-O -D__BLST_PORTABLE__" go install github.com/flashbots/mev-boost@latest
$ sudo cp ~/go/bin/mev-boost /usr/local/bin
$ sudo chown mevboost:mevboost /usr/local/bin/mev-boost
```

## Support

If you have any question or if you need additional support, make sure to get in touch with the EthStaker community on:

* Discord: [discord.io/ethstaker](https://discord.io/ethstaker)
* Reddit: [reddit.com/r/ethstaker](https://www.reddit.com/r/ethstaker/)

## Credits

Based on [CoinCashew's Ethereum Merge Upgrade Checklist for Home Stakers and Validators](https://www.coincashew.com/coins/overview-eth/ethereum-merge-upgrade-checklist-for-home-stakers-and-validators).
