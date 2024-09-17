## Install PostgresSQL on EC2
```bash
1. sudo apt update
2. sudo apt-get -y install postgresql
```

## Update user
```bash
1. sudo su postgres
2. psql
3. ALTER USER postgres password 'your_password';
4. \q
5. exit
```

## Create User
```bash
1. sudo su postgres
2. psql
3. CREATE USER username password 'your_password';
4. \q
5. exit
```

## Give roles and privileges to the user
```bash
1. sudo su postgres
2. psql
3. ALTER ROLE username SUPERUSER CREATEROLE CREATEDB REPLICATION BYPASSRLS;
4. GRANT ALL PRIVILEGES ON DATABASE db_name TO your_user;
5. \q
6. exit
```

## Access settings
```bash
1. cd /etc/postgresql/10/main/
2. nano pg_hba.conf

**Paste(for all)**
host       all        all              0.0.0.0/0          md5

**Paste(for specific IP)**
host       all        all              193.176.251.151/32          md5
host       all        all              .../32          md5



3. nano postgresql.conf

**Paste(for all)**
listen_addresses='*'

**Paste(for specific IP)**
listen_addresses='localhost,193.176.251.151,...'
```

## Restart postgres
```bash
sudo service postgresql restart
```