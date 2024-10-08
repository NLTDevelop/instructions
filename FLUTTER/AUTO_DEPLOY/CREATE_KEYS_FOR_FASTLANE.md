# Создание ключей для Fastlane

## Apple Issuer ID, Apple Key ID, and Apple Key Content

Чтобы получить **Apple Issuer ID**, **Apple Key ID**, и **Apple Key Content**, перейдите
в [Users and Access](https://appstoreconnect.apple.com/access/integrations/api). Там переходим в раздел **Интеграции**.
В левой колонке выбираем **API App Store Connect** и выбираем раздел **Ключи команды**. Нажимаем на **+** и даем добавляем
описание, чтобы не забыть назначение ключа а так же, кто сможет с ним работать, в нашем случае через какой аккаунт
будет производиться сборка.

**Внимание!** После создания ключ будет доступен до момента обновления страницы.

- **Apple Issuer ID** - этот значение расположено над списком ключей.
- **Apple Key ID** - это значение расположено в списке ключей и соотвествует скаченом ключу по принципу Auth_{Apple Key
  ID}.p8.
- **Apple Key Content** - это значение расположено в скаченном ключе.
  ![Users Access Keys](images/team_keys.jpeg)
 
## Developer Portal Team ID 

Для получения **Developer Portal Team ID** перейдите в [Apple Developer](https://developer.apple.com/account). Далее
спуститься ниже до раздела **Membership Details**. В этом разделе будет указано **Team ID**.
![Membership Details](images/membership_details.jpeg)
