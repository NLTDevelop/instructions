# Group setting

Create group
```bash
sudo groupadd name_group
```

Adding users to groups
```bash
sudo usermod -aG name_group user_name

You should definitely add this:
sudo usermod -aG name_group www-data
```

Customize a folder for a group
```bash
sudo chown -R :name_group path_folder
```

Configure a folder so that only group owners can manage it
```bash
sudo chmod -R 770 path_folder
```

# Create User

Create user
```bash
sudo adduser new_user
```

Create password for user
```bash
sudo passwd name_user
```

# Dependency setup
```bash
sudo apt update
sudo apt install openssh-server
```

# Setting sshd_config
## SSH KEY login

```bash
sudo nano /etc/ssh/sshd_config
```
For single user:
```bash
Match User your_username
PasswordAuthentication no
```

For all users:
```bash
PasswordAuthentication no
```

[Add key in user](https://github.com/NLTDevelop/instructions/blob/main/DEPLOY/ADD_PUBLIC_KEY_TO_AWS_EC2.md)

## Password login
```bash
sudo nano /etc/ssh/sshd_config
```
For single user:
```bash
Match User your_username
PasswordAuthentication yes
```

For all users:
```bash
PasswordAuthentication yes
```

Restart ssh
```bash
sudo systemctl restart ssh
```

# Setting up a server connection for the user

Install sshpass
```bash
 brew install sshpass
```

Server login
```bash
sshpass -p 'your_password' ssh your_user@00.000.00.000
```

# Example
```bash
1. sudo adduser frontend
2. sudo passwd frontend
3. su frontend
4. sudo mkdir -p /home/frontend/.ssh
5. sudo touch /home/frontend/.ssh/authorized_keys
6. sudo nano /home/frontend/.ssh/authorized_keys
7. chmod 600 authorized_keys
8. sudo service ssh restart
9. exit

10. sudo groupadd webusers
11. sudo usermod -aG webusers frontend
12. sudo usermod -aG webusers ubuntu
13. sudo usermod -aG webusers www-data
14. sudo chown -R :webusers var/www/build
15. sudo chmod -R 770 var/www/build
```
