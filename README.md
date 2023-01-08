# PocketBase + Fly.io Template
For hosting PocketBase instances on Fly.io (for free). Taken from https://github.com/pocketbase/pocketbase/discussions/537; this repo merely exists for brevity.

## Deploying
1. Login: ```flyctl auth signup``` or ```flyctl auth login```
2. Launch (but decline hosting/database CLI prompts): ```flyctl launch```
3. Create storage: ```flyctl volumes create pb_data --size=1```
4. Mount data (insert into newly created .toml):
```toml
[mounts]
  destination = "/pb/pb_data"
  source = "pb_data"
```
5. Deploy: ```flyctl deploy```

## Retrieving Backups
1. Register an ssh key: ```flyctl ssh issue --agent```
2. Proxy connection to Fly.io: ```flyctl proxy 10022:22```
3. Copy data (use separate terminal): ```scp -r -P 10022 root@localhost:/pb/pb_data  /your/local/pb_data```