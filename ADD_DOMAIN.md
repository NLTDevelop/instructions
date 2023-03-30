## Buy a domain name ##

1) Go to site [nic.ua](https://nic.ua)
2) Login to site and click 'ЗАРЕГИСТРИРОВАТЬ ДОМЕН'
3) Select domain name
4) Confirm your purchase
5) Change domain config to 'DNS' and add your elastic IP

## Add elastic IP ##

1) Go to [AWS EC2](https://console.aws.amazon.com/ec2/v2/home?region=eu-west-1#Home:)
2) Click on Elastic IPs
3) Click on Allocate new address
4) Click on Allocate
5) Click on Actions -> Associate address
6) Select your instance
7) Click on Associate

## Install Nginx ##

1) Update your default packages.
```
sudo apt update
```
2) Install Nginx
```
sudo apt install nginx 
```
3) Confirm Successful Installation
```
nginx -v
```

## Configure Nginx ##

1) Create a new configuration file for your custom domain:
```
sudo nano /etc/nginx/sites-available/mydomain.com
```
2) In this file, add the following server block:
```perl
server {
    listen 80;
    listen [::]:80;

    server_name mydomain.com www.mydomain.com;

    location / {
        proxy_pass http://localhost:3000; # Replace with your app's URL or IP
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection 'upgrade';
        proxy_set_header Host $host;
        proxy_cache_bypass $http_upgrade;
    }
}
```
3) Save and close the file when you are finished.
4) Create a symbolic link from the configuration file to the Nginx sites-enabled directory:
```bash
sudo ln -s /etc/nginx/sites-available/mydomain.com /etc/nginx/sites-enabled/
```
5) Test the Nginx configuration for syntax errors:
```bash
sudo nginx -t
```
6) If there are no errors, restart Nginx:
```bash
sudo systemctl restart nginx
```
7) Open your browser and navigate to your domain name. You should see the default Nginx landing page.

<!-- ## Configure Nginx for SSL ##
1) Install Certbot:
```bash
sudo apt-get install certbot python3-certbot-nginx
```
2) Run Certbot to obtain an SSL certificate and have Certbot edit your Nginx configuration automatically to serve it, turning on HTTPS access in a single step:
```bash
sudo certbot --nginx
```
3) Follow the prompts to answer a few questions and provide your email address. You will then be asked to choose how you would like to authenticate with the Let's Encrypt CA. Choose the second option, which will redirect HTTP traffic to HTTPS and use a temporary webserver to validate your domain name.
4) When the installation is complete, you should see a message similar to the following:
```bash
Congratulations! You have successfully enabled https://mydomain.com and https://www.mydomain.com
```
5) Open your browser and navigate to your domain name. You should see the default Nginx landing page, but this time accessed via HTTPS. -->
