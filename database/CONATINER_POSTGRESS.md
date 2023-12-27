# Create container Postgres on aws ec2 #

1) Install docker on ec2
```
sudo apt-get update
sudo apt-get install docker.io
``` 
2) Running a PostgreSQL DB in a docker container
```
sudo docker run --name postgresql -e POSTGRES_USER=postgres -e POSTGRES_PASSWORD=post123 -p 5432:5432 -v /data:/var/lib/postgresql/data -d postgres:alpine
```
**--name postgresql** : name of our container

**-e POSTGRES_USER=postgres** : name of the user

**-e POSTGRES_PASSWORD=post123** : password of the user

**-p 5432:5432** : binding ec2 instance port to docker port, our postgreSQL DB is exposed in this port

**-v /data:/var/lib/postgresql/data** : volume binding to persist & saving our data in the ec2 instance.

**-d** : running in detached mode, so that our container always runs in the background

**postgres:alpine** : postgres docker image. we chose the alpine image, due to its small size.

3) Check if the container is running
```
sudo docker ps
```
4) Exposing your DB server

- select your ec2 instance & select the security group related to the instance.
- Select the "Inbound rules" tab, then click "Edit inbound rules".
- Now you need to add the following rule to your inbound rules.
  - **Protocol : TCP**
  - **Port : 5432**
  - **Source : 0.0.0.0/0**

# [Article](https://dev.to/amedd/dockerize-a-postgresql-database-in-an-aws-ec2-instance-5dej) #