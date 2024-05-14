## Group setting

Create group
```bash
sudo groupadd name_group
```

Adding users to groups
```bash
sudo usermod -aG name_group user_name

You should definitely add this:
sudo usermod -aG name_group www-data

```

Customize a folder for a group
```bash
sudo chown -R :name_group path_folder
```

Configure a folder so that only group owners can manage it
```bash
sudo chmod -R 770 path_folder
```