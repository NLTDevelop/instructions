# Create dump #

1) Create dump
```
pg_dump -h localhost -U your_username -d your_database_name -f /path/to/your/dump_file.sql
```

2) Restore dump
```
psql -h localhost -U your_username -d your_database_name -f /path/to/your/dump_file.sql
```

# Pull dump from server #

1) Connect to server using pem
``` 
ssh -i /path/to/your/pem_file.pem ec2-user@your_ec2_instance_ip
```

2) Pull dump from server
```
scp -i /path/to/your/pem_file.pem ec2-user@your_ec2_instance_ip:/path/to/your/dump_file.sql /path/to/your/local/directory
```