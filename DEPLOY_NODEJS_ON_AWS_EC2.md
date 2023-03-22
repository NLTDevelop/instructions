## Install Git ##

1) Update your default packages.
```
sudo apt update
```
2) Install Git
```
sudo apt install git 
```
3) Confirm Successful Installation
```
git version
```
Create app for our project
mkdir apps
Go to folder apps
cd apps
Add SSH key for Github access
Generate  SSH key

ssh-keygen -t ed25519 -C "your_email@example.com"
Start the ssh-agent in the background.
eval "$(ssh-agent -s)"
Create .ssh/config
touch ~/.ssh/config
ssh-add ~/.ssh/id_ed25519
Show public SSH key
cat ~/.ssh/id_ed25519.pub
Add  public SSH key to your Github settings -> SSH and GPG keys
video instruction - https://www.youtube.com/watch?v=YqrKu9QZvsc
Git instruction - https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent
Установка Docker
Install packages to allow apt to use a repository over HTTPS
sudo apt-get install \
    ca-certificates \
    curl \
    gnupg \
    lsb-release
Add Docker’s official GPG key
sudo mkdir -m 0755 -p /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
Use the following command to set up the repository:
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
Update the apt package index:
sudo apt-get update
Install Docker Engine, containerd, and Docker Compose.
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
Confirm Successful Installation
docker -v
Запуск проекта
Переходим в склонированный репозиторий
sudo docker compose up -d
sudo docker logs <container name>
sudo docker rm <container name> - f

Clear aws ec2 memory 
sudo docker system prune
Explore containers 
sudo  docker exec -it <name-of-container> bash
Show containers list
sudo docker container ls
Update docker build
sudo docker build -t getting-started .



video - https://www.youtube.com/watch?v=mqI5ZcV3prI&t=1145s
