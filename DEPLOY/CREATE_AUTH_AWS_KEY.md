# 1 Generate RSA Key Pair: #

```bash
ssh-keygen -t rsa -b 2048 -f ~/.ssh/my_key_pair
```

# 2 Go to RSA Key Pair folder: #

```bash
cd ~/.ssh
```

# 3 Open Public Key: #

```bash
cat my_key_pair.pub
```

Copy you public key

# 4 Go to AWS ec2 instance: #

```bash
sudo nano ~/.ssh/authorized_keys
```

# 5 Paste your public key: #

# 6 Ensure that the authorized_keys file has the correct permissions: #

```bash
sudo chmod 600 ~/.ssh/authorized_keys
```

# 7 You can also edit the sshd_config file to disable password authentication and only allow key-based authentication for improved security: #

```bash
sudo nano /etc/ssh/sshd_config
```

# 8 Find the PasswordAuthentication line and change the value to no: #

```bash
PasswordAuthentication no
```

# 9 Restart the SSH service to apply the changes: #

```bash
sudo service ssh restart
```

# 10 Connect to your instance using your key pair: #

```bash
ssh -i ~/.ssh/my_key_pair ubuntu@your_ec2_ip
```