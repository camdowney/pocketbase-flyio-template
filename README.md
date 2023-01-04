# Pocketbase + Fly.io Template
Taken from: https://github.com/pocketbase/pocketbase/discussions/537

## Deploying
### 1. Login
Run ```flyctl auth signup``` or ```flyctl auth login```

### 2. Launch
Run ```flyctl launch```, but do not set up any databases or deploy yet

### 3. Create storage
Run ```flyctl volumes create pb_data --size=1``` and insert the following config into fly.toml:

```toml
[mounts]
  destination = "/pb/pb_data"
  source = "pb_data"
```

### 4. Deploy
 Run ```flyctl deploy```

## Retrieving Backups
```bash
# Register ssh key if not done already
flyctl ssh issue --agent

# Proxy connection to Fly.io VM
flyctl proxy 10022:22

# Run in separate terminal to copy data
scp -r -P 10022 root@localhost:/pb/pb_data  /your/local/pb_data
```