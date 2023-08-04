# Running an Taiko Validator Node


<p align="center">
  <img height="auto" width="auto" src="https://i.imgur.com/N9KAUN8.png">
</p>


* [Installation Docker](https://github.com/p4nrp/testnet/blob/main/taiko.md#1-Installation-Docker)
* [Alchemy Setting](https://github.com/p4nrp/testnet/blob/main/taiko.md#2-Alchemy-Setting)
* [Setting DockerFile](https://github.com/p4nrp/testnet/blob/main/taiko.md#3-setting-dockerfile)
* [Start Your Validator](https://github.com/p4nrp/testnet/blob/main/taiko.md#4-start-your-validator)
* [Usefull Command](https://github.com/p4nrp/testnet/blob/main/taiko.md#usefull-commands)


### 1. Installation Docker

Install docker 
install a few prerequisite packages which let apt use packages over HTTPS:

```
sudo apt install apt-transport-https ca-certificates curl software-properties-common
```

add the GPG key for the official Docker repository to your system:
```
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
```

add the Docker repository to APT sources:
```
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

Update your existing list of packages again for the addition to be recognized:
```
sudo apt update
```

Make sure you are about to install from the Docker repo instead of the default Ubuntu repo:
```
apt-cache policy docker-ce
```

Install Docker
```
sudo apt install docker-ce
```

### 2. Alchemy Setting
1. Create [AlchemyAccount](https://auth.alchemy.com/signup?redirectUrl=https%3A%2F%2Fdashboard.alchemy.com%2Fsignup%2F%3Freferrer_origin%3DDIRECT)
2. Select `+CREATE NEW APP`
3. Define name apps
4. Network Use Sepolia
5. `CREATE APP`
6. Navigate to apps already created `VIEW DETAILS`
7. Select `VIEW KEY`
8. Copy HTTP & WSS

