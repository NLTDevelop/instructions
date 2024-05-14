## Dependency setup
```bash
sudo apt update
sudo apt install openssh-server
```

## Setting sshd_config
```bash
sudo nano /etc/ssh/sshd_config
```
For single user: /n \n
Match User your_username
PasswordAuthentication yes

For all users:
PasswordAuthentication yes

```bash
sudo systemctl restart ssh
```

## Setting up a server connection for the user

Install sshpass
```bash
 brew install sshpass
```

Server login
```bash
sshpass -p 'your_password' ssh your_user@00.000.00.000
```