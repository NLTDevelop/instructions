# Setting up the PM2 Logs Cleaning Script
## Create the PM2 Logs Cleaning Script

Create a new file named clean_pm2_logs.sh in the user's home directory. Here's an example script content:

```bash
nano ~/clean_pm2_logs.sh
```

```bash
Copy code
#!/bin/bash

# Лог файл
LOGFILE=~/clean_pm2_logs.log

# Очистка логов PM2
echo "[$(date)] Starting PM2 log flush" >> $LOGFILE
pm2 flush >> $LOGFILE 2>&1
echo "[$(date)] Finished PM2 log flush" >> $LOGFILE
```

## Make the Script Executable

Give execute permission to the script using the chmod command:

```bash
chmod +x ~/clean_pm2_logs.sh
```

## Add a Cron Job

Open the cron editor using the command:

```bash
crontab -e
```
Add the following line to the cron file to run the script daily at midnight:

```bash
0 0 * * * ~/clean_pm2_logs.sh
```
Save the changes and close the editor.

## Check the Execution of the Cron Job

After setting up the cron job, ensure it runs correctly. You can check the cron system log entries using the command:

```bash
grep CRON /var/log/syslog
```
You should see entries about the execution of your cron job.

## Check the Log File Content

After running the script, verify that the log file contains execution information:

```bash
cat ~/clean_pm2_logs.log
```
If the script executed successfully, you'll see entries about the start and finish of the PM2 logs flush.

## Check the PM2 Logs

After running the script, ensure that the PM2 logs were successfully cleared. You can check them using the command:

```bash
pm2 logs
```


