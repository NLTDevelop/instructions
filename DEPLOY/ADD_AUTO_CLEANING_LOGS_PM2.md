# Настройка скрипта для очистки логов PM2
## Создайте скрипт для очистки логов PM2

Создайте новый файл с именем clean_pm2_logs.sh в домашней директории пользователя. Вот пример содержимого скрипта:

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

## Сделайте скрипт исполняемым

Дайте скрипту права на выполнение с помощью команды chmod:

```bash
chmod +x ~/clean_pm2_logs.sh
```


## Добавьте cron задание

Откройте редактор cron с помощью команды:

```bash
crontab -e
```
Добавьте следующую строку в файл cron, чтобы запускать скрипт ежедневно в полночь:

```bash
0 0 * * * ~/clean_pm2_logs.sh
```
Сохраните изменения и закройте редактор.

## Проверьте выполнение cron задания

После настройки cron задания, убедитесь, что оно запускается правильно. Вы можете проверить записи в системном журнале cron с помощью команды:

```bash
grep CRON /var/log/syslog
```
Вы должны увидеть записи о выполнении вашего cron задания.

## Проверьте содержимое лог файла

После запуска скрипта, убедитесь, что лог файл содержит информацию о выполнении:

```bash
cat ~/clean_pm2_logs.log
```
Если скрипт успешно выполнился, вы увидите записи о начале и завершении очистки логов PM2.

## Проверьте логи PM2

После выполнения скрипта, убедитесь, что логи PM2 были успешно очищены. Вы можете проверить их с помощью команды:

```bash
pm2 logs
```



## Create key pair

Create key pair
```bash
ssh-keygen -t rsa -b 4096 -C "your_email@example.com" -f ~/my_key
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