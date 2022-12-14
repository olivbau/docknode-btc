# Docknode BTC

## Metrics

* Bitcoin RPC endpoint: `https://mydomain.com`
* Mempool API endpoint: `https://mydomain.com:9102`
* Nodeexporter endpoint: `https://mydomain.com:9100/metrics`

## Install 

0. VPS config (optional)
```bash
apt update
apt upgrade
apt install git
# Install docker: https://docs.docker.com/engine/install/ubuntu/#install-using-the-repository
```

1. Clone the repository and
```bash
git clone https://github.com/olivbau/docknode-btc.git
cd docknode-btc
```

2. Configure environement variables
```bash
cp .env.example .env

# Generate users passwords for basic auth
docker run --rm caddy:2-alpine caddy hash-password --plaintext 'password'

# Set users and passwords for basic auth
# Set the host
nano .env
```

3. Setup UFW
```bash
ufw allow ssh
ufw deny 8332 && ufw deny 8999 && ufw deny 3306 && ufw deny 50001 && ufw deny 8080 && ufw deny 8000
ufw enable
```

4. Run
```bash
docker compose pull
docker compose up -d
docker logs -f docknode-btc-bitcoind-1 --since 20m
docker logs -f docknode-btc-fulcrum-1 --since 20m
docker logs -f docknode-btc-mempoolapi-1 --since 20m
docker compose down
```