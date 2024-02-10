# Running an BEVM Validator Node


<p align="center">
  <img height="auto" width="auto" src="https://i.imgur.com/N9KAUN8.png">
</p>


* [Installation Docker](https://github.com/p4nrp/testnet/blob/main/taiko.md#1-Installation-Docker)
* [Alchemy Setting](https://github.com/p4nrp/testnet/blob/main/taiko.md#2-Alchemy-Setting)
* [Setup And Run Node](https://github.com/p4nrp/testnet/blob/main/taiko.md#3-Setup-And-Run-Node)
* [Monitor Node](https://github.com/p4nrp/testnet/blob/main/taiko.md#4-Monitor-Node)
* [Usefull Command](https://github.com/p4nrp/testnet/blob/main/taiko.md#usefull-commands)


### 1. Installation Docker

Install docker 
```
curl -fsSL https://get.docker.com | bash -s docker
```



### 2. Establish a directory and initial the config.json
1. Make a new directory and enter it ```mkdir node && cd node```
2. Create a JSON Configuration File ```touch config.json```
3. Then, open the file in a text editor. The vim editor is used here as an example: ```nano config.json```
4. Paste the content below (You need to adjust the content on your own.)
5. ```
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
7. Navigate to apps already created `VIEW DETAILS`
8. Select `VIEW KEY`
9. Copy HTTP & WSS

### 3. Setup And Run Node
1. Download Node
   ```
   git clone https://github.com/taikoxyz/simple-taiko-node.git
   ```
3. To Directory simple-taiko-node
   ```
   cd simple-taiko-node
   ```
4. Copy .env
   ```
   cp .env.sample .env
   ```
3. Edit .env
   ```
   nano .env
   ```
   Change value `L1_ENDPOINT_HTTP` and `L1_ENDPOINT_WS` with your HTTPS And WSS From Alchemy

   Change Value `ENABLE_PROVER` to `true`
   
   Change Value `L1_PROVER_PRIVATE_KEY` with your private key from metamask (new wallet)
   
   Save file CTRL + x + Y + enter
   
4. Update Node
   ```
   docker compose pull
   ```
5. Run Node
   ```
   docker compose up -d
   ```
6. Check log
   ```
   docker compose logs -f 
   ```
   or use
   ```
   docker ps
   ```
   ```
   docker inspect CONTAINER_NAME | grep log
   ```
   ```
   tail -f
   ```
   ```
   cd LOG_FOLDER
   ```
   file -i .log
   The files type: "application/octet-stream; charset=binary" have errors, can be RENAMED/REMOVED/UPDATED for fix.
   ```
8. Cek log for block approval
   ```
   docker compose logs -f | grep "💰 Your block proof was accepted"
   ```
   
### 4. Monitor Node

A node dashboard will be running on `localhost` on the `GRAFANA_PORT` you set in your `.env` or `.env.l3` file. For a Grimsvotn L2 node that would default to: 
```
http://localhost:3001/d/L2ExecutionEngine/l2-execution-engine-overview
```
