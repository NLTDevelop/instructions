# Create dump #

1) Create dump
```
pg_dump -h localhost -U your_username -d your_database_name -f /path/to/your/dump_file.sql
```

2) Restore dump
```
psql -h localhost -U your_username -d your_database_name -f /path/to/your/dump_file.sql
```