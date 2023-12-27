## Configure Nginx to Use SSL ##

1) Update your default packages.
```
sudo apt update
```
2) Install Certbot
```bash
sudo apt install certbot python3-certbot-nginx
```
3) Run Certbot to add the SSL certificate
```bash
sudo certbot --nginx -d example.com -d www.example.com
```
4) Select your domain name when prompted.
5) Select whether or not to redirect HTTP traffic to HTTPS, then enter Y.
6) Enter your email address when prompted.
7) Enter Y to agree to the terms of service.
8) Certbot will now retrieve the SSL certificate and install it.
9) Open your browser and go to your domain name or IP address. You should now see the default Nginx landing page, but with a green padlock in the address bar indicating that the connection is secure.
