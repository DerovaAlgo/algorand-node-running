# Algorand Node Running

Community driven set of guides, benchmarks and best practices for Algorand node running.

## Official docs

## Quick Start

There are multiple ways to run an Algorand node. Here are the most common use-case focused guides that allows you to quickly setup a non-archival node in ~1hr and optionally become a validator or start incentivized staking*

<!-- TODO
proper guides instead of external links
 -->
### Mouse friendly one-click nodes

#### Windows
[Aust One Click Node](https://github.com/AustP/austs-one-click-node) is a simple installer to get up and running on Windows with minimal effort.
Download the exe file under the releases section on the Github page, run the exe (then go More Info and Allow).
After a few seconds you'll see the interface load, and start syncing.

Under the settings menu, be sure to enable "Start Node on Startup" to ensure the software runs if the node ever loses power or reboots.

#### Linux/MacOS

[Pixelnode](https://www.pixelnode.org) provide a simple install script to get your node up and running as quickly and easily as possible using Docker containers.
From your server terminal, enter:
```sudo curl -L http://get.pixelnode.org | sudo bash```

Once the installation is complete, you should be able to access the Pixelnode web interface on port 8000 of your server's public IP address (e.g., http://<your_server_ip>:8000).
_If you're running this on your home network and not a VPS (Linode, DigitalOcean, etc), you won't be able to access it via the IP provided until you update your NAT / Port Forward rules on your router to direct the traffic to the machines Local IP - TCP Ports 3000 (Grafana), 4190 (Algod-8080), 8000 (WebUI), 9090 (Prometheus). Please be aware that exposing port 3000 will allow anyone to access your Grafana instance using the default credentials (admin/admin). If this is enabled, login immediately and change the password or lock down your NAT rule to only allow your IP._

On the WebGUI, follow the on-screen instructions to install the node, specify the network (Mainnet, Testnet, etc.) and setting your stake amount (for participation nodes).

The Pixelnode web interface will display the status of your Algorand node. You can see if it's running, syncing with the network (catching up), and other details.

### Terminal managed

* [Official one-click-node](https://github.com/algorandfoundation/algorun), docker based

* Linux Node on Ubuntu on Windows WSL
Ensure that you have virtualisation enabled in your BIOS/UEFI settings (VT-x/AMD-V) and that it's supported by your CPU.
Install the Windows Subsystem for Linux:
```wsl --install```
Reboot and run the Ubuntu app, follow the on-screen prompts to setup your WSL account / environment.
Update the distro by running "sudo apt update".
Then install the node software using the Linux guide.

* Linux node on Ubuntu


## UI / Web interface add-ons

### Terminal UI

Algorand provide a Terminal UI that shows realtime node status, fast-catchup progress and realtime block data (such as proposers).
This UI is accessed via the terminal directly.
On Linux you can download the binary under the Github releases section, and if you run the binary on your local node, just point it to your data directory.

For example:
```
wget https://github.com/algorand/node-ui/releases/download/v0.2.0/nodeui_Linux_x86_64.tar.gz
tar -xzf nodeui_Linux_x86_64.tar.gz
ALGORAND_DATA=/var/lib/algorand ./nodeui
```
Read more here: [Official terminal UI](https://github.com/algorand/node-ui)

### Web UI

Allo'Ctrl is a node manager that is accessed via a web browser instead of within the Terminal.
Once the dependancies have been installed, simply create the directory
```
mkdir ~/algorand-dashboard
cd ~/algorand-dashboard
```
And run the NPX command to install it.
```
npx alloctrl
    Need to install the following packages:
        alloctrl@0.1.4
    Ok to proceed? (y) 
```
The installer will ask you a few questions to setup the environment file.

Read more here: [Allo'Ctrl](https://github.com/AlgoNode/alloctrl)

## Node types

There are various node types that are used to support the Algorand network, their roles are descibed below.

### Relay Node

Relay nodes receive and broadcast information (blocks, transactions) between other relay nodes.
They help the network run smoothly and efficiently by distributing messages as quickly and directly as possible across the globe.
It's important to note that these *DO NOT* play any role in the consensus mechanism _(Block Proposal/Transaction Validation/Block Voting)_.

### Participation Node

Participation Nodes are the core of consensus, by securing the network in a decentralised way.
These nodes are responsible for proposing blocks, valdating transactions, and voting on blocks proposed by other nodes.
Hardware requirements are a lot lower than Relay Nodes as the VRF they run is light on resources, and they only need to keep a record of the last 1000 blocks.
These nodes host the participation keys for an account that has Algo staked, as the VRF lottery is weighted based on the amount an account has online (staked).

### Archival Node

Archive nodes store the entire history of the blockchain (all transactions ever made) for anyone who needs it.
This acts as a backup for the network and allows users to see past activity, typically relay nodes are also archival nodes.

### Indexer

Indexers take the massive amount of blockchain data (stored by archival nodes) and organise it in a database such as Postgres.
This allows applications (eg: Blockchain explorers such as [allo.info](https://allo.info)) to query the database, and present blockchain data to you in a readable / human friendly format.

## Installing

### Home node

### Cloud node

### K8S

### Docker/Docker-compose

## Running

### Boostrapping

[Bootstrapping](running/bootstrapping.md) involves getting your node in sync with other nodes on the network.

### Start/Stop/Auto



### Updating

Updating is usually an automatic process but you can do it manually as explained in this [updating guide](/running/updating.md)

### Monitoring

[Monitoring](monitoring/monitoring.md) your node is cruicial to ensuring the node is operating as expected and protecting the network.
We have provided two example ways you can monitor your node using Netdata or Telegraf. 

### Troubleshooting

## Config tweaking

## Staking

## FAQ

## Developer resources

### Switching networks
