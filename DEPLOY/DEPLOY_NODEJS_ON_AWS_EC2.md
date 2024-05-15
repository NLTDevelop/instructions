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
4) Create app for our project
```
mkdir apps
```
5) Go to folder apps
```
cd apps
```

## Clone project from Github ##

1) Generate  SSH key 
```
ssh-keygen -t ed25519 -C "your_email@example.com"
```
2) Start the ssh-agent in the background.
```
eval "$(ssh-agent -s)"
```
3) Create .ssh/config
```
touch ~/.ssh/config
ssh-add ~/.ssh/id_ed25519
```
4) Show public SSH key
```
cat ~/.ssh/id_ed25519.pub
```
5) Add  public SSH key to your Github settings -> SSH and GPG keys
[Video instruction](https://www.youtube.com/watch?v=YqrKu9QZvsc)
[Git instruction](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent)
6) Clone project from Github
```
git clone <link SSh>
```

## Update nodejs ##

1) Clear npm cache
```
sudo npm cache clean -f
```

2) Install n package
```
sudo npm install -g n
```

3) Install latest stable version of nodejs
```
sudo n stable
```

4) Close terminal and open again
```
node -v
```

## Install postgres ##

1) Update the apt package index
```
sudo apt-get update
```

2) Install the postgres package
```
sudo apt-get install postgresql postgresql-contrib
```

3) Confirm Successful Installation
```
psql --version
```

4) Start the postgres service
```
sudo service postgresql start
```

5) Access the postgres shell
```
sudo -u postgres psql
```

6) Create a new user
```
CREATE USER dmitriy WITH PASSWORD 'dmitriy1234';
```

7) Create a new database
```
CREATE DATABASE dmitriy;
```

8) Grant privileges to the user
```
GRANT ALL PRIVILEGES ON DATABASE dmitriy TO dmitriy;
```

9) Exit the postgres shell
```
\q
```
 
## Install PM2 ##

1) Install PM2
```
sudo npm install pm2 -g
```

2) Start the app
```
pm2 start dist/main.js --name my-project-name
```

















## Install Docker ##

1) Install packages to allow apt to use a repository over HTTPS
```
sudo apt-get install \
    ca-certificates \
    curl \
    gnupg \
    lsb-release
```
2) Add Docker’s official GPG key
```
sudo mkdir -m 0755 -p /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
```
3) Use the following command to set up the repository:
```
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```
4) Update the apt package index:
```
sudo apt-get update
```
5) Install the latest version of Docker Engine and containerd
```
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
``` 
6) Confirm Successful Installation
```
docker -v
```



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
