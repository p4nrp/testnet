# Running an ChainFlip Validator


<p align="center">
  <img height="auto" width="auto" src="https://i.imgur.com/N9KAUN8.png">
</p>


* [Installation](https://github.com/p4nrp/testnet/blob/main/elixirfinance.md#1-installation-1)
* [StartNode](https://github.com/p4nrp/testnet/blob/main/elixirfinance.md#2-setting-dockerfile)
* [Start Your Validator](https://github.com/p4nrp/testnet/blob/main/elixirfinance.md#3-start-your-validator)
* [Usefull Command](https://github.com/p4nrp/testnet/blob/main/elixirfinance.md#usefull-commands)


### 1. Installation

# Install Go lang
update & upgrade package
```
apt update -y && apt upgrade -y
```

install golang
```
apt install golang-go
```

check go lang version
```
apt install golang-go
```

# Install Geth
The following command enables the launchpad repository:
```
sudo add-apt-repository -y ppa:ethereum/ethereum

```

Then, to install the stable version of go-ethereum:
```
sudo apt-get update
sudo apt-get install ethereum
```

Updating an existing Geth installation to the latest version can be achieved by stopping the node and running the following commands:
```
sudo apt-get update
sudo apt-get install ethereum
sudo apt-get upgrade geth
```

# Install ChainFlip

Adding Chainflip APT Repo
Download Chainflip GPG key from our official repo:

```
sudo mkdir -p /etc/apt/keyrings
curl -fsSL repo.chainflip.io/keys/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/chainflip.gpg
```

Verify the key's authenticity:
```
gpg --show-keys /etc/apt/keyrings/chainflip.gpg
```

add Chainflip's Repo to apt sources list:
```
echo "deb [arch=amd64 signed-by=/etc/apt/keyrings/chainflip.gpg] https://repo.chainflip.io/perseverance/$(lsb_release -c -s) $(lsb_release -c -s) main" | sudo tee /etc/apt/sources.list.d/chainflip.list
```

Installing The Packages
```
sudo apt update
sudo apt install -y chainflip-cli chainflip-node chainflip-engine1.0
```

Validator Keys
Generate new private key account 
It is recommended to generate and save the required keys using the following chainflip-cli command:

```
chainflip-cli generate-keys --path /etc/chainflip/keys
```

Recovering Your Private Keys
In case you lose access to your node, you can recover the private keys using the seed phrase. Using the example phrase generated above:
```
chainflip-cli generate-keys \
    --path /etc/chainflip/keys \
    --seed-phrase 'YOUR SEED PHARSE'
```

Engine Settings
We need to create the engine config file.
```
sudo mkdir -p /etc/chainflip/config
sudo nano /etc/chainflip/config/Settings.toml
```

Editing the Config
Copy the following to your `nano` editor. You also need to replace `IP_ADDRESS_OF_YOUR_NODE` with the public IP Address of your server. To get the public IP of your node you can run this command: `curl -w "\n" ifconfig.me`.
Also you'll need to provide the `ws_endpoint`, and `http_endpoint` for whichever Ethereum client you've selected. It will look different depending on which client you select:

# Copy this file

```
# Default configurations for the CFE
[node_p2p]
node_key_file = "/etc/chainflip/keys/node_key_file"
ip_address = "IP_ADDRESS_OF_YOUR_NODE"
port = "8078"
 
[state_chain]
ws_endpoint = "ws://127.0.0.1:9944"
signing_key_file = "/etc/chainflip/keys/signing_key_file"
 
[eth]
# Ethereum private key file path. This file should contain a hex-encoded private key.
private_key_file = "/etc/chainflip/keys/ethereum_key_file"
 
[eth.rpc]
ws_endpoint = "wss://my_local_geth_node:8546"
http_endpoint = "https://my_local_geth_node:8545"
 
# Optional
# [eth.backup_rpc]
# ws_endpoint = "wss://some_public_rpc.com:443/<secret_access_key>"
# http_endpoint = "https://some_public_rpc.com:443/<secret_access_key>"
 
[dot.rpc]
ws_endpoint = "wss://rpc-pdot.chainflip.io:443"
http_endpoint = "https://rpc-pdot.chainflip.io:443"
 
# Optional
# [dot.backup_rpc]
# ws_endpoint = "wss://rpc-pdot2.chainflip.io:443"
# http_endpoint = "https://rpc-pdot2.chainflip.io:443"
 
[btc.rpc]
basic_auth_user = "flip"
basic_auth_password = "flip"
http_endpoint = "http://a108a82b574a640359e360cf66afd45d-424380952.eu-central-1.elb.amazonaws.com"
 
# Optional
# [btc.backup_rpc]
# basic_auth_user = "flip2"
# basic_auth_password = "flip2"
# http_endpoint = "http://second-node-424380952.eu-central-1.elb.amazonaws.com"
 
# Optional (default: 36079)
# [logging]
# command_server_port = 36079
```

### 2. Start The Node
# Starting the Node
To start the chainflip-node, run the following command.
```
sudo systemctl start chainflip-node
```

To check on the service, we use `status`.
```
systemctl status chainflip-node
```

To view the live logs for the validator software, check on them via `journalctl`. You can quit at anytime using `ctrl/control + c`

Check the Node:
```
journalctl -f -u chainflip-node.service
```

At the start, you should see that your node is synchronising to the network, something like this:
```
2023-03-24 08:21:30 💻 Memory: 7957MB
2023-03-24 08:21:30 💻 Kernel: 5.4.0-122-generic
2023-03-24 08:21:30 💻 Linux distribution: Ubuntu 20.04.4 LTS
2023-03-24 08:21:30 💻 Virtual machine: yes
2023-03-24 08:21:30 📦 Highest known block at #0
2023-03-24 08:21:30 〽️ Prometheus exporter started at 127.0.0.1:9615
2023-03-24 08:21:30 Running JSON-RPC HTTP server: addr=127.0.0.1:9933, allowed origins=Some(["http://localhost:*", "http://127.0.0.1:*", "https://localhost:*", "https://127.0.0.1:*", "https://polkadot.js.org"])
2023-03-24 08:21:30 Running JSON-RPC WS server: addr=127.0.0.1:9944, allowed origins=Some(["http://localhost:*", "http://127.0.0.1:*", "https://localhost:*", "https://127.0.0.1:*", "https://polkadot.js.org"])
2023-03-24 08:21:30 🔍 Discovered new external address for our node: /ip4/178.128.36.211/tcp/30333/p2p/12D3KooWMDs3oyT2YpQw88V7TdmN1dJa73D1jrfQorLaBovh7Kim
2023-03-24 08:21:35 ⏩ Warping, Downloading finality proofs, 7.99 Mib (10 peers), best: #0 (0x2d00…c9b3), finalized #0 (0x2d00…c9b3), ⬇ 1.6MiB/s ⬆ 27.8kiB/s
2023-03-24 08:21:40 ⏩ Warping, Downloading finality proofs, 15.97 Mib (14 peers), best: #0 (0x2d00…c9b3), finalized #0 (0x2d00…c9b3), ⬇ 1.7MiB/s ⬆ 25.8kiB/s
2023-03-24 08:21:45 ⏩ Warping, Downloading state, 40.83 Mib (15 peers), best: #0 (0x2d00…c9b3), finalized #0 (0x2d00…c9b3), ⬇ 3.5MiB/s ⬆ 14.0kiB/s
2023-03-24 08:21:50 ⏩ Warping, Importing state, 58.00 Mib (15 peers), best: #0 (0x2d00…c9b3), finalized #0 (0x2d00…c9b3), ⬇ 2.0MiB/s ⬆ 3.1kiB/s
2023-03-24 08:21:54 Unable to author block in slot. No best block header: Chain lookup failed: Failed to get header for hash 0x0cdb…b083
2023-03-24 08:21:55 ⏩ Warping, Importing state, 58.00 Mib (15 peers), best: #1913239 (0x5b6b…c1b3), finalized #1913239 (0x5b6b…c1b3), ⬇ 9.3kiB/s ⬆ 1.3kiB/s
2023-03-24 08:21:56 Warp sync is complete (57 MiB), restarting block sync.
2023-03-24 08:21:57 ✨ Imported #1913240 (0xa922…5e2e)
2023-03-24 08:21:57 ✨ Imported #1913241 (0x3a15…012e)
2023-03-24 08:21:57 ✨ Imported #1913242 (0x0ceb…c1f8)
2023-03-24 08:21:57 ✨ Imported #1913243 (0xec83…ca57)
2023-03-24 08:21:57 ✨ Imported #1913244 (0x52c0…6594)
2023-03-24 08:22:00 ⏩ Block history, #4480 (11 peers), best: #1913244 (0x52c0…6594), finalized #1913242 (0x0ceb…c1f8), ⬇ 1.6MiB/s ⬆ 110.4kiB/s
2023-03-24 08:22:00 ✨ Imported #1913245 (0xd0b4…45a0)
2023-03-24 08:22:05 ⏩ Block history, #9152 (11 peers), best: #1913245 (0xd0b4…45a0), finalized #1913243 (0xec83…ca57), ⬇ 859.4kiB/s ⬆ 111.2kiB/s
2023-03-24 08:22:06 ✨ Imported #1913246 (0x93ad…15cd)
2023-03-24 08:22:10 ⏩ Block history, #11840 (11 peers), best: #1913246 (0x93ad…15cd), finalized #1913244 (0x52c0…6594), ⬇ 1.1MiB/s ⬆ 146.3kiB/s
2023-03-24 08:22:12 ✨ Imported #1913247 (0x1e1c…70df)
2023-03-24 08:22:15 ⏩ Block history, #19392 (11 peers), best: #1913247 (0x1e1c…70df), finalized #1913245 (0xd0b4…45a0), ⬇ 2.1MiB/s ⬆ 150.5kiB/s
2023-03-24 08:22:18 ✨ Imported #1913248 (0xbb74…9178)
2023-03-24 08:22:20 ⏩ Block history, #28800 (11 peers), best: #1913248 (0xbb74…9178), finalized #1913246 (0x93ad…15cd), ⬇ 2.9MiB/s ⬆ 169.1kiB/s
2023-03-24 08:22:24 ✨ Imported #1913249 (0xb062…b457)
2023-03-24 08:22:25 ⏩ Block history, #36288 (11 peers), best: #1913249 (0xb062…b457), finalized #1913246 (0x93ad…15cd), ⬇ 2.4MiB/s ⬆ 226.4kiB/s
2023-03-24 08:22:30 ⏩ Block history, #41088 (11 peers), best: #1913249 (0xb062…b457), finalized #1913247 (0x1e1c…70df), ⬇ 1.6MiB/s ⬆ 100.5kiB/s
2023-03-24 08:22:30 ✨ Imported #1913250 (0x4bc1…8362)
2023-03-24 08:22:35 ⏩ Block history, #43200 (11 peers), best: #1913250 (0x4bc1…8362), finalized #1913248 (0xbb74…9178), ⬇ 330.6kiB/s ⬆ 145.2kiB/s
```




