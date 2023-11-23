# Running an ChainFlip Validator


<p align="center">
  <img height="auto" width="auto" src="https://i.imgur.com/N9KAUN8.png">
</p>


* [Installation](https://github.com/p4nrp/testnet/blob/main/elixirfinance.md#1-installation-1)
* [Setting DockerFile](https://github.com/p4nrp/testnet/blob/main/elixirfinance.md#2-setting-dockerfile)
* [Start Your Validator](https://github.com/p4nrp/testnet/blob/main/elixirfinance.md#3-start-your-validator)
* [Usefull Command](https://github.com/p4nrp/testnet/blob/main/elixirfinance.md#usefull-commands)


### 1. Installation

Install Go lang

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

### 2. Setting DockerFile

Download dockerfile from elixir finance
```
wget https://files.elixir.finance/Dockerfile
```

Edit file DockerFile with your address and your private key
```
nano DockerFile
```

Build DockerFile image
```
docker build . -f Dockerfile -t elixir-validator
```

### 3. Start Your Validator
Run the validator by executing the following docker command: 
```
docker run -it --name ev elixir-validator
```
Optionally, you can configure the the validator to automatically run at startup:
```
docker run -d --restart unless-stopped --name ev elixir-validator
```
Your validator should start up in 20 seconds and begin submitting order proposals to the network.


# Usefull commands
check docker available running
```
docker ps
```

check docker logs realtime run
```
docker logs -f machinename
```

Upgrading Node 
```
docker kill ev
docker rm ev
docker pull elixirprotocol/validator:testnet-2
docker build . -f Dockerfile -t elixir-validator
```
