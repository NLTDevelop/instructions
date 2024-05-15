## Edit nginx config

Open config for special server

```bash
sudo nano /etc/nginx/sites-enabled/domain.com
```

Add redirect
    
Check config

```bash
sudo nginx -t
```

Restart nginx

```bash
sudo service nginx restart
```