I have an instruction for creating MAILER account for back-end
I need translate it to English and make it more informative
Return markdown format:

Как настроить сторонний почтовый клиент для работы с Gmail

### Включение IMAP в почте Gmail ###

1. Заходим в почту https://mail.google.com/ и переходим в настройки.
2. Переходим в “Пересылка и POP/IMAP” и включаем IMAP.

Заходим в почту https://mail.google.com/ и переходим в настройки.

1) Войдите в [Google Accounts](https://myaccount.google.com) с помощью своего аккаунта Google.
2) В консоли управления аккаунтом нажмите слева выберите пункт меню <b>Безопасность</b>><b>Двухэтапная аутентификация</b>><b>Включить двухэтапную аутентификацию</b>
3) Возвращаемся в меню <b>Безопасность</b> и выбираем <b>Пароли приложений</b>
4) Выбираем <b>Другое (имя настраиваемое)</b> и вводим название приложения
5) Вам показывается пароль, который нужно сохранить, так как после закрытия окна его уже не будет видно

```
Если у вас личный аккаунт Google
В июне 2024 года параметры "Включить IMAP" и "Отключить IMAP" станут недоступны. В Gmail доступ по протоколу IMAP всегда включен, и для уже подключенных у вас сервисов электронной почты ничего не изменится. Никаких действий с вашей стороны не требуется.
```

Данные для подклбчение сервиса

MAIL_USER: Ваша почта
MAIL_PASSWORD: Пароль для приложения
MAIL_HOST: smtp.gmail.com
MAIL_PORT: 587



# Setting Up a Third-Party Email Client to Work with Gmail

### Enabling IMAP in Gmail

1. Log in to your Gmail account at [Gmail](https://mail.google.com/).
2. Go to settings.
3. Navigate to “Forwarding and POP/IMAP” and enable IMAP.

### Configuring Google Account for App Passwords

1. Log in to your [Google Account](https://myaccount.google.com).
2. In the account management console, select **Security** > **2-Step Verification** > **Turn on 2-Step Verification**.
3. Return to the **Security** menu and select **App Passwords**.
4. Choose **Other (Custom name)** and enter a name for your application.
5. You will be shown a password. Save this password as it will not be displayed again after you close the window.

Note for Personal Google Accounts:
Starting June 2024, the options "Enable IMAP" and "Disable IMAP" will no longer be available. IMAP access will always be enabled in Gmail, and nothing will change for your already connected email services. No action is required on your part.


### Email Service Connection Details

- **MAIL_USER**: Your email address
- **MAIL_PASSWORD**: The app password you generated
- **MAIL_HOST**: smtp.gmail.com
- **MAIL_PORT**: 587
