## Remove BD container ##

sudo docker rm $(sudo docker ps -a -q)

sudo docker run --name postgresql -e POSTGRES_USER=postgres -e POSTGRES_PASSWORD=NltDev2022 -p 5432:5432 -v /data:/var/lib/postgresql/data -d postgres:alpine

## Start web site NktDev ##

cd ~/web/applications/nltdev-website/ && pm2 start npm --name "nltdev-website" -- start

## Start nlt-scan-audit-back ##

cd ~/server/applications/nlt-scan-audit-back/ && pm2 start dist/main.js --name nlt-scan-audit-back 

## Start truksta-back##

cd ~/server/applications/truksta-back/ && pm2 start dist/main.js --name truksta-back

## Start zoolux-admin-back ##

cd ~/server/applications/zoolux-admin-back/ && pm2 start dist/main.js --name zoolux-admin-back


## Reboot CTO ##

# Start containers pizzaday-back-main #

```
cd Pizzaday-back && sudo docker compose up -d —build
```

# Start containers aws-shop-admin-main #

```
cd ./server/applications/aws-shop-admin && sudo docker compose up -d —build
```

# Start containers apulse-tg-bot-radios-main #

```
cd ./server/applications/apulse-tg-bot-radios && sudo docker compose up -d —build
```

# nlt-dev-shop-back #

cd ~/web/applications/nlt-dev-shop-back/ && pm2 start npm --name "nlt-dev-shop-back" -- start

# pizzaday-employee-shop-back #

cd ~/web/applications/pizzaday-employee-shop-back/ && pm2 start npm --name "pizzaday-employee-shop-back" -- start