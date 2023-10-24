<p align="center">
  <img height="auto" width="auto" src="https://i.imgur.com/N9KAUN8.png">
</p>

You Can Use This If You Don't Have VPS
https://github.com/codespaces
✔️Use Template Blank
```
sudo apt update && sudo apt upgrade -y
```

```
sudo apt install nodejs && sudo apt install git
```

```
sudo apt install apt-transport-https ca-certificates curl software-properties-common -y
```

```
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
```

```
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu focal stable"
```

```
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-compose-plugin -y
```

```
sudo apt install npm
```

```
npm install --global @subsquid/cli@latest
```

```
sqd init <yourusername> -t https://github.com/subsquid-quests/single-chain-squid
```

```
cd <yourusername>
```

```
sqd up
```

```
npm ci
```

```
sqd build
```

```
sqd migration:apply
```

```
sqd run
```

