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
