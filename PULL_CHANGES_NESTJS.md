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
sudo git pull origin main
```
4) Rebuild project
```
sudo docker build --no-cache -t my-docker-image .
```
5) Once the build is complete, stop the running container by running the following command:
```
sudo docker-compose down
```
6) Run the container with your changes using the following command:
```
sudo docker compose up -d
```
7) Show containers list
```
sudo docker container ls
```
8) Check logs
```
sudo docker logs <container name>
```
