# Pocketbase + Fly.io Template
Taken from: https://github.com/pocketbase/pocketbase/discussions/537

## Deploying
1. Login: ```flyctl auth signup``` or ```flyctl auth login```
2. Launch: ```flyctl launch``` *do not set up any databases or deploy yet
3. Create free volume: ```flyctl volumes create pb_data --size=1```
4. Insert the following config into fly.toml:
```toml
[mounts]
  destination = "/pb/pb_data"
  source = "pb_data"
```
5. Deploy: ```flyctl deploy```

## Retrieving Backups
```bash
# this will register a ssh key with your local agent (if you haven't already)
flyctl ssh issue --agent

# proxies connections to a fly VM through a Wireguard tunnel
flyctl proxy 10022:22

# run in a separate terminal to copy the pb_data directory
scp -r -P 10022 root@localhost:/pb/pb_data  /your/local/pb_data
```