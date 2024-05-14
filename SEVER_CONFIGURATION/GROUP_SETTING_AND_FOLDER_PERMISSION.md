## Create group

Create group
```bash
sudo groupadd name_group
```

//Adding users to groups
```bash
sudo usermod -aG webusers user_name

You should definitely add this:
sudo usermod -aG webusers www-data

```

## Adding users to groups