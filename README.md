# Home Server

Configs etc for my home network/server

## Setup

- Hardware: Dell Wyse 5070 [from eBay](https://www.ebay.com.au/itm/256696383835))
- OS: Ubuntu Server

## Network Configuration

### Netplan

1. `sudo wget -O /etc/netplan/01-netcfg.yaml https://raw.githubusercontent.com/JMontagu/home-server/refs/heads/main/01-netcfg.yaml && sudo chmod 600 /etc/netplan/01-netcfg.yaml`
2. `sudo netplan try` — check networking still works, if not config will revert after 120 seconds
    - `ping -c 4 192.168.86.1`
    - `ping -c 4 8.8.8.8`
4. `sudo netplan apply`

### [Network Config](https://github.com/JMontagu/home-server/blob/main/network_config.yaml)

Defines network topology to be manually applied

## Infra
### Docker

1. Install docker [using official instructions](https://docs.docker.com/engine/install/ubuntu/#install-using-the-repository)
2. Pull docker-compose: `sudo curl -o docker-compose.yaml https://raw.githubusercontent.com/JMontagu/home-server/refs/heads/main/docker-compose.yaml`
3. Run containers: `sudo docker compose up -d`

## Services
### [ddclient](https://ddclient.net/)
Automatically syncs this servers IP address with Cloudflare so we can host public services off jademontagu.com:
1. Log into [Cloudflare Dashboard](https://dash.cloudflare.com/login)
    1. Go to "My Profile" → "API Tokens"
    2. Create a token with "Zone:Zone:Read" and "Zone:DNS:Edit" permissions for your domain
2. `sudo nano /etc/environment`
3. Add this line `CLOUDFLARE_API_TOKEN=your_actual_token_here`
4. Setup ddclient conf: `sudo curl -o ddclient.conf https://raw.githubusercontent.com/JMontagu/home-server/refs/heads/main/ddclient.conf`
