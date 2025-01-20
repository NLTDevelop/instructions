## Create key pair

Create key pair
```bash
ssh-keygen -t rsa -b 4096 -C "your_email@example.com" -f ~/.ssh/my_key
```

Open public key
```bash
cat ~/my_key.pub
```

## Add public key to AWS EC2

1. Go to EC2
2. Once you are connected to your EC2 instance, navigate to the ~/.ssh directory:
   
    ```bash
    cd ~/.ssh
    ```
3. If the authorized_keys file does not exist, create it:
   
    ```bash
    touch authorized_keys
    ```

4. Open the authorized_keys file with a text editor and paste the public key that you copied from your local machine into the file, then save and close the file.

    ```bash
    nano authorized_keys
    ```

5. Change the permissions of the authorized_keys file with the chmod command so that only the root user can read and write to the file:

    ```bash
    chmod 600 authorized_keys
    ```

6. Restart the SSH service to apply the changes:

    ```bash
    sudo service ssh restart
    ```

## Add private key to github EC2_INSTANCE_KEY

1. Go to github
2. Go to settings
3. Go to Secrets and Variables
4. Open Actions 
5. Press New repository secret
6. Add your private key

How to check you private key

```bash
cat ~/my_key
```

Instruction how to get AWS_ACCESS_KEY_ID and AWS_SECRET_ACCESS_KEY
https://wanago.io/2023/02/13/nestjs-api-ci-cd-aws-ecs-github-actions/


Lates instruction CI/CD
https://www.youtube.com/watch?v=YBjrZZMXNe8