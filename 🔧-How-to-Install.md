## π Installer via CLI

[Ubuntu/CentOS] Interactive CLI installer, supports Docker or without Docker. 

```bash
curl -o kuma_install.sh http://git.kuma.pet/install.sh && sudo bash kuma_install.sh
```

## Advanced Installation

### π³ Docker

```bash
# Create a volume
docker volume create uptime-kuma

# Start the container
docker run -d --restart=always -p 3001:3001 -v uptime-kuma:/app/data --name uptime-kuma louislam/uptime-kuma:1
```

Browse to http://localhost:3001 after started.

Change Port and Volume

```bash
docker run -d --restart=always -p <YOUR_PORT>:3001 -v <YOUR_DIR OR VOLUME>:/app/data --name uptime-kuma louislam/uptime-kuma:1
```

β οΈ Please use in a local volume only. Other types such as nfs are not supported.

### πͺπ» Without Docker (Recommended for x86/x64 only)

Required Tools: Node.js >= 14, git and pm2.

(**Not recommended for ARM CPU users.** Since there is no prebuilt for node-sqlite3, it is hard to get it running)

```bash
# Update your npm to the latest version
npm install npm -g

git clone https://github.com/louislam/uptime-kuma.git
cd uptime-kuma
npm run setup

# Option 1. Try it
node server/server.js

# (Recommended)
# Option 2. Run in background using PM2
# Install PM2 if you don't have: npm install pm2 -g
pm2 start server/server.js --name uptime-kuma

```

Browse to http://localhost:3001 after started.

```
# Listen to different port or hostname
pm2 start server/server.js --name uptime-kuma -- --port=80 --hostname=0.0.0.0
```

#### Useful Commands

```bash
pm2 start uptime-kuma
pm2 stop uptime-kuma
pm2 restart uptime-kuma

# Run at startup
pm2 startup
```

### Docker Compose Example

https://github.com/louislam/uptime-kuma/blob/master/docker-compose.yml

### βΈοΈ Kubernetes

β  Warning: K8s deployment is provided by contributors. I have no experience with K8s and I can't fix error in the future. I only test Docker and Node.js. Use at your own risk.

See more [here](https://github.com/louislam/uptime-kuma/blob/master/kubernetes/README.md) 

### Install on Synology NAS

Unofficial tutorial by Marius Bogdan Lixandru:

https://mariushosting.com/how-to-install-uptime-kuma-on-your-synology-nas/

## (Optional) One more step for Reverse Proxy

This is optional for someone who want to do reverse proxy.

Unlikely other web apps, Uptime Kuma is based on WebSocket. You need two more headers **"Upgrade"** and **"Connection"** in order to reverse proxy WebSocket.

Please read wiki for more info:
https://github.com/louislam/uptime-kuma/wiki/Reverse-Proxy

## Experiment

### Install Uptime Kuma server in your Android phone
https://github.com/louislam/uptime-kuma/issues/423