# Install PostgresSQL  on EC2

https://dev.to/amedd/dockerize-a-postgresql-database-in-an-aws-ec2-instance-5dej

# Updating the apt package index
sudo apt-get update

# Installing the packages to allow apt to download the repository over https
sudo apt-get install ca-certificates curl gnupg lsb-release

# Add Docker’s official GPG key
sudo mkdir -p /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg

#Setting up the repository
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

# Updating the apt package index
sudo apt-get update

#Installing the latest version of the docker-cli, compose, etc
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-compose-plugin


sudo docker run --name postgresql -e POSTGRES_USER=postgres -e POSTGRES_PASSWORD=post123 -p 5432:5432 -v /data:/var/lib/postgresql/data -d postgres:alpine