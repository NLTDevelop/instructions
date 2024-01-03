# Pull changes Nodejs project and update container #

1) Stops all running containers
```
sudo docker stop $(sudo docker ps -a -q)
```
2) Remove all containers
```
sudo docker rm $(sudo docker ps -a -q)
```
3) Pull project from Github
```
git pull origin main
```
4) Rebuild project
```
sudo docker build --no-cache -t <my-docker-image> .
```
5) Once the build is complete, stop the running container by running the following command:
```
sudo docker compose down
```
6) Run the container with your changes using the following command:
```
sudo docker compose up -d --build
```
7) Show containers list
```
sudo docker container ls
```
8) Check logs
```
sudo docker logs <container name>
```

# Clear memory and cache #

1) Stop all containers
```
sudo docker stop $(sudo docker ps -a -q)
```
2) Remove all containers
```
sudo docker rm $(sudo docker ps -a -q)
```
3) Remove all images
```
sudo docker rmi $(sudo docker images -q)
```
4) Remove all volumes
```
sudo docker volume rm $(sudo docker volume ls -q)
```
5) Remove all networks
```
sudo docker network rm $(sudo docker network ls -q)
```
6) Remove all stopped containers
```
sudo docker container prune
```
7) Remove all unused images
```
sudo docker image prune
```
8) Remove all unused volumes
```
sudo docker volume prune
```
9) Remove all unused networks
```
sudo docker network prune
```
10) Remove all unused containers, networks, images (both dangling and unreferenced), and optionally, volumes.
```
sudo docker system prune -a
```


docker system prune

docker system prune -a

docker volume prune
sudo docker compose up -d --no-deps --build