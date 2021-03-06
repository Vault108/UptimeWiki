## 🆙🐳 Docker

Re-pull the latest docker image and create another container with the same volume.

For someone who used my "How-to-use" commands to install Uptime Kuma, you can update by this:

```bash
docker pull louislam/uptime-kuma:1
docker stop uptime-kuma
docker rm uptime-kuma
docker run -d --restart=always -p 3001:3001 -v uptime-kuma:/app/data --name uptime-kuma louislam/uptime-kuma:1
```

PS: For every new release, it takes some time to build the docker image, please be patient if it is not available yet.

## 🆙 💪🏻 Without Docker

```bash
cd <uptime-kuma-directory>
git fetch --all
git checkout 1.7.3 --force
npm install --legacy-peer-deps
node node_modules/esbuild/install.js
npm run build
pm2 restart uptime-kuma
```

If you see node-pre-gyp error, please use your npm to the latest version
```bash
# Update your npm to the latest version
npm install npm -g
```