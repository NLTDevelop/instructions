Lates instruction CI/CD
https://www.youtube.com/watch?v=YBjrZZMXNe8

Go to github.com -> your_project -> Settings -> Secrets and Variables -> Actions

1) Create EC2_SSH_KEY

Open .pem file and copy all content to EC2_SSH_KEY

2) Create HOST_DNS

Go to AWS -> EC2 -> Instances -> your_instance -> Public IPv4 DNS -> copy and paste to EC2_HOST

3) Create USERNAME

If you use ubuntu, then USERNAME is ubuntu