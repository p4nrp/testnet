# Running an Elixir v2.0 Validator


<p align="center">
  <img height="auto" width="auto" src="https://i.imgur.com/N9KAUN8.png">
</p>


* [Installation](https://github.com/p4nrp/testnet/blob/main/seinetwork.md#1-installation-1)
* [Setting DockerFile](https://github.com/p4nrp/testnet/blob/main/seinetwork.md#2-setting-dockerfile)
* [Start Your Validator](https://github.com/p4nrp/testnet/blob/main/seinetwork.md#3-start-your-validator)
* [Usefull Command](https://github.com/p4nrp/testnet/blob/main/seinetwork.md#usefull-commands)


### 1. Installation

SETUP SEI FULLNODE

```
wget -O sei.sh https://raw.githubusercontent.com/kj89/testnet_manuals/main/sei/sei.sh && chmod +x sei.sh && ./sei.sh
```

When installation is finished please load variables into system
```
source $HOME/.bash_profile
```

Next you have to make sure your validator is syncing blocks. You can use command below to check synchronization status
```
seid status 2>&1 | jq .SyncInfo
```



### 2. Wallet 

To create new wallet you can use command below. Don’t forget to save the mnemonic
```
seid keys add $WALLET
```

(OPTIONAL) To recover your wallet using seed phrase
```
seid keys add $WALLET --recover
```

list of wallets
```
seid keys list
```

SAVE WALLET INFO 
```
SEI_WALLET_ADDRESS=$(seid keys show $WALLET -a)
SEI_VALOPER_ADDRESS=$(seid keys show $WALLET --bech val -a)
echo 'export SEI_WALLET_ADDRESS='${SEI_WALLET_ADDRESS} >> $HOME/.bash_profile
echo 'export SEI_VALOPER_ADDRESS='${SEI_VALOPER_ADDRESS} >> $HOME/.bash_profile
source $HOME/.bash_profile
```


Cek Wallet Ballance
```
seid query bank balances $SEI_WALLET_ADDRESS
```

Cek status 
```
seid status 2>&1 | jq .SyncInfo
```

Create Validatro and Register to block 
```
seid tx staking create-validator \
  --amount 1000000usei \
  --from $WALLET \
  --commission-max-change-rate "0.01" \
  --commission-max-rate "0.2" \
  --commission-rate "0.07" \
  --min-self-delegation "1" \
  --pubkey  $(seid tendermint show-validator) \
  --moniker $NODENAME \
  --chain-id $SEI_CHAIN_ID
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
