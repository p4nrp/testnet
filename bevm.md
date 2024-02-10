# Running an BEVM Validator Node


<p align="center">
  <img height="auto" width="auto" src="https://i.imgur.com/N9KAUN8.png">
</p>


* [Installation Docker](https://github.com/p4nrp/testnet/blob/main/taiko.md#1-Installation-Docker)
* [Establish a directory and initial the config.json](https://github.com/p4nrp/testnet/blob/main/taiko.md#2-Alchemy-Setting)
* [Setup And Run Node](https://github.com/p4nrp/testnet/blob/main/taiko.md#3-Setup-And-Run-Node)
* [Monitor Node](https://github.com/p4nrp/testnet/blob/main/taiko.md#4-Monitor-Node)
* [Usefull Command](https://github.com/p4nrp/testnet/blob/main/taiko.md#usefull-commands)


### 1. Installation Docker

Install docker 
```
curl -fsSL https://get.docker.com | bash -s docker
```



### 2. Establish a directory and initial the config.json
1. Make a new directory and enter it
```
mkdir node && cd node
```
3. Create a JSON Configuration File
```
touch config.json
```
5. Then, open the file in a text editor. The vim editor is used here as an example:
```
nano config.json
```
7. Paste the content below (You need to adjust the content on your own.)
Change Your-Node-Name on your own
```
{
  "chain": "testnet",
  "log-dir": "/log",
  "enable-console-log": true,
  "no-mdns": true,
  "validator": true,
  "unsafe-rpc-external": true,
  "offchain-worker": "when-authority",
  "rpc-methods": "unsafe",
  "log": "info,runtime=info",
  "port": 30333,
  "rpc-port": 8087,
  "pruning": "archive",
  "db-cache": 2048,
  "name": "Your-Node-Name",
  "base-path": "/data",
  "telemetry-url": "wss://telemetry-testnet.bevm.io/submit 1",
  "bootnodes": []
}
```

   
### 4. Run the node with Docker

Fetch the docker image
```
docker pull btclayer2/bevm:testnet-v0.1.2
```
Run a docker container
```
docker run -d --restart always --name bevm-node \
  -p 8087:8087 -p 30333:30333 \
  -v $PWD/config.json:/config.json -v $PWD/data:/data \
  -v $PWD/log:/log -v $PWD/keystore:/keystore \
  btclayer2/bevm:testnet-v0.1.2 /usr/local/bin/bevm \
  --config /config.json
```
Check the logs from your container
```
tail -f log/bevm.log
```
Check it on the telemetry
[Telemetry Link](https://telemetry-testnet.bevm.io/)
