# Автоматическая выгрузка на TestFlight с помощью GitHub Actions

## Конечная цель руководства

Научиться настраивать автоматическую выгрузку приложения **iOS** в **TestFlight** с помощью **GitHub Actions** и
**Fastlane** на собственном удаленном устройстве под управлением **macOS**.

### Условия успешного выполнения руководства

- Аккаунт на который будет происходить выгрузка приложения должен быть
  участником [Apple Developer Program](https://developer.apple.com/programs/).
- Наличие созданного приложения в [App Store Connect](https://appstoreconnect.apple.com/).
- Свое устройство под управлением **macOS**, которое будет выполнять задачу **Runner-а** для сборки и выгрузки
  приложения.

> Указанные выше пункты не будет рассмотрены в данном руководстве, так как они выходят за его рамки. Мы по умолчанию
> подразумеваем, что они уже выполнены.

## Ключи и методы их получения

Наши ключи будут храниться в безопасном месте, чтобы не попасть в руки злоумышленникам. Для этого мы будем использовать
**GitHub Secrets**. Для того чтобы перейти в раздел **Secrets** перейдите в ваш репозиторий на **GitHub** и выберите
вкладку **Settings**. Далее в левой колонке **Secrets** выберете **Secrets and variables** и нажмите на **Actions**.
Теперь вы можете добавить свои ключи нажав на кнопку **New repository secret**.

Для выполнения задачи нам понадобится следующее ключи и идентификаторы:

- GIT_AUTHORIZATION - <YOUR_GITHUB_USERNAME>:<YOUR_PERSONAL_ACCESS_TOKEN>
- APPLE_KEY_ID — App Store Connect API Key ID
- APPLE_ISSUER_ID — App Store Connect Issuer ID
- APPLE_KEY_CONTENT — App Store Connect API Key ID значение, которое храниться в файле .p8
- APP_STORE_CONNECT_TEAM_ID - the ID of your App Store Connect team in you’re in multiple teams


- DEVELOPER_APP_ID - in App Store Connect, go to the app -> App Information -> Scroll down to the General Information
  section of your app and look for Apple ID.
- DEVELOPER_APP_IDENTIFIER - your app’s bundle identifier
- DEVELOPER_PORTAL_TEAM_ID - the ID of your Developer Portal team if you’re in multiple teams
- FASTLANE_APPLE_ID - the Apple ID or developer email you use to manage the app
- MATCH_PASSWORD - the passphrase that you assigned when initializing match, will be used for decrypting the
  certificates and profiles.
- TEMP_KEYCHAIN_USER & TEMP_KEYCHAIN_PASSWORD - assign a temp keychain user and password for your workflow.

### Git Authorization

Для того, чтобы создать ключ **GIT_AUTHORIZATION** перейдите в настройки вашего профиля на **GitHub** и в левой
навигационной панели ищем **Developer settings**. Далее переходим в раздел **Personal access tokens** и нажимаем на
кнопку **Generate new token**. В поле **Note** введите название вашего токена, например **GIT_AUTHORIZATION**.
Далее в разделе **Select scopes** выберите **repo** и **workflow**. Нажмите на кнопку **Generate token**.
![GitHub Personal Access Token](images/git_auth_key.png)
Скопируйте ваш токен. Теперь перейдите в настройки вашего репозитория на **GitHub** и в разделе **Secrets** создайте
новый секрет с именем **GIT_AUTHORIZATION** и вставьте в него ваш токен и ник аккаунта по принципу
**<YOUR_GITHUB_USERNAME>:<YOUR_PERSONAL_ACCESS_TOKEN>**.

### Apple Issuer ID, Apple Key ID, Apple Key Content

Чтобы получить **Apple Issuer ID**, **Apple Key ID**, и **Apple Key Content**, перейдите
в [Users and Access](https://appstoreconnect.apple.com/access/integrations/api). Там переходим в раздел **Интеграции**.
В левой колонке выбираем **API App Store Connect** и выбираем раздел **Ключи команды**. Нажимаем на **+** и даем
добавляем
описание, чтобы не забыть назначение ключа а так же, кто сможет с ним работать, в нашем случае через какой аккаунт
будет производиться сборка.

**Внимание!** После создания ключ будет доступен до момента обновления страницы.

- **Apple Issuer ID** - этот значение расположено над списком ключей.
- **Apple Key ID** - это значение расположено в списке ключей и соотвествует скачанном ключу по принципу Auth_{Apple Key
  ID}.p8. Можно закодировать в base64, но в скрипте нужно уточнить это.
- **Apple Key Content** - это значение расположено в скаченном ключе.
  ![Users Access Keys](images/team_keys.jpeg)

### Developer Portal Team ID

Для получения **Developer Portal Team ID** перейдите в [Apple Developer](https://developer.apple.com/account). Далее
спуститься ниже до раздела **Membership Details**. В этом разделе будет указано **Team ID**.
![Membership Details](images/membership_details.jpeg)

## Настройка Fastlane

Для начала установим **Fastlane** на наше устройство. Для этого выполним команду:

- Перехожу в папку ios

```bash
cd ios
```

- Устанавливаю fastlane

```bash
fastlane init
```

Файл Fastlane со скриптом состоит из следующих частей:

- Платформа с которой мы будем работать

```ruby
default_platform(:ios)
```

- Получение ключей из хранилища **GitHub Secrets**

```ruby
DEVELOPER_PORTAL_TEAM_ID = ENV["DEVELOPER_PORTAL_TEAM_ID"]
GIT_AUTHORIZATION = ENV["GIT_AUTHORIZATION"]
TEMP_KEYCHAIN_USER = ENV["TEMP_KEYCHAIN_USER"]
TEMP_KEYCHAIN_PASSWORD = ENV["TEMP_KEYCHAIN_PASSWORD"]
APPLE_KEY_ID = ENV["APPLE_KEY_ID"]
APPLE_ISSUER_ID = ENV["APPLE_ISSUER_ID"]
APPLE_KEY_CONTENT = ENV["APPLE_KEY_CONTENT"]
```

- Методы для создания временного хранилища и его удаления. Необходимо, поскольку мы импортируем сертификаты, нам
  требуется создать хранилище для их хранения.

```ruby
def delete_temp_keychain(name)
  delete_keychain(
    name: name
  ) if File.exist? File.expand_path("~/Library/Keychains/#{name}-db")
end

def create_temp_keychain(name, password)
  create_keychain(
    name: name,
    password: password,
    unlock: false,
    timeout: 0
  )
end

def ensure_temp_keychain(name, password)
  delete_temp_keychain(name)
  create_temp_keychain(name, password)
end
```

- Метод для выгрузки на **TestFlight**. В этом методе мы будем использовать ключи, которые мы получили ранее.

```ruby
platform :ios do
  lane :upload_to_store do
    keychain_name = TEMP_KEYCHAIN_USER
    keychain_password = TEMP_KEYCHAIN_PASSWORD
    ensure_temp_keychain(keychain_name, keychain_password)
```

- Метод для создания **API Key** для **App Store Connect**. В этом методе мы будем использовать ключи, которые мы
  получили ранее. Для получения ключа используется метод **app_store_connect_api_key**. В этом методе мы указываем
  следующие параметры:
    - **key_id** - **Apple Key ID**
    - **issuer_id** - **Apple Issuer ID**
    - **key_content** - **Apple Key Content**
    - **duration** - время жизни ключа
    - **in_house** - является ли ключ для **App Store** или **Enterprise**
    - **is_key_content_base64** - если **key_content** закодирован в **base64**, по умолчанию **false**

```ruby
    api_key = app_store_connect_api_key(
      key_id: APPLE_KEY_ID,
      issuer_id: APPLE_ISSUER_ID,
      key_content: APPLE_KEY_CONTENT,
      duration: 1200,
      in_house: false,
      is_key_content_base64: true // если ключ закодирован в base64, по умолчанию false
    )
```

- Установка **Pods** игнорируя **cache**. Это необходимо, чтобы установить **Pods** с нуля.

```ruby
    cocoapods(clean_install: true)
```

- Метод для подписания кода. Состоит из следующих параметров:
    - type - определение типа профиля
    - git_basic_authorization - авторизация для **Git** для дальнейшего получения сертификатов и подписей из репозитория
    - readonly - только для чтения
    - keychain_name - имя временного хранилища
    - keychain_password - пароль временного хранилища
    - api_key - ключ для **App Store Connect**

```ruby
    match(
      type: 'appstore',
      git_basic_authorization: Base64.strict_encode64(GIT_AUTHORIZATION),
      readonly: false,
      keychain_name: keychain_name,
      keychain_password: keychain_password,
      api_key: api_key
    )
```

- Очистка **Flutter** и установка **pub** пакетов

```ruby
    sh("flutter clean")
    sh("flutter pub get")
```

- Собирает проект и упаковывает его в **.ipa** файл. В этом методе мы указываем следующие параметры:
    - **export_method** - метод экспорта, в нашем случае **app-store**
    - **export_options** - опции экспорта, в нашем случае **teamID** - **DEVELOPER_PORTAL_TEAM_ID**

```ruby
    gym(
      export_method: "app-store",
      export_options: {
        teamID: DEVELOPER_PORTAL_TEAM_ID,
      }
    )
```

- Последний метод - выгрузка на **TestFlight**. В этом методе мы указываем следующие параметры:
    - **api_key** - ключ для **App Store Connect**
    - **ipa** - путь к **.ipa** файлу
    - **skip_submission** - пропустить отправку на **App Store Connect**
    - **skip_waiting_for_build_processing** - пропустить ожидание обработки сборки

```ruby
    pilot(
      api_key: api_key,
      ipa: "./Runner.ipa",
      skip_submission: true,
      skip_waiting_for_build_processing: true
    )
  end
end
```

## Настройка GitHub Actions

Для начала создадим файл **.github/workflows/auto_deploy.yaml** в корне нашего проекта. В этом файле мы будем описывать
наши шаги для автоматической выгрузки на **TestFlight**. Код файла будет состоять из следующих частей:

- **name** - название нашего действия

```yaml
name: Deploy Application
```

- **on** - событие, при котором будет запускаться наше действие

```yaml
on:
  push:
    branches:
      - master
```

- **jobs** - описание наших задач с указанием на **self-hosted** для запуска нашего действия на нашем удаленном
  устройстве под управлением **macOS**. Наша задача будет состоять из следующих шагов:
    - **checkout** - клонирование нашего репозитория
    - **cache** - кеширование **Flutter SDK**
    - **flutter-action** - установка **Flutter SDK**
    - **cache** - кеширование **pub packages**
    - **run** - установка пакетов **pub**
    - **checkout** - клонирование нашего репозитория
    - **run** - установка **Pods**
    - **run** - установка **bundle**
    - **run** - запуск **Fastlane** c указанием переменных окружения полученных из **GitHub Secrets**

```yaml
jobs:
  build-and-deploy-ios:
    runs-on: self-hosted

    steps:
      - uses: actions/checkout@v4
      - name: Cache Flutter SDK
        uses: actions/cache@v4
        with:
          path: /opt/flutter
          key: flutter-sdk-${{ runner.os }}-${{ hashFiles('pubspec.yaml') }}
          restore-keys: |
            flutter-sdk-${{ runner.os }}-

      - uses: subosito/flutter-action@v2
        with:
          flutter-version: '3.24.0'
          channel: 'stable'

      - name: Cache pub packages
        uses: actions/cache@v4
        with:
          path: |
            ~/.pub-cache
          key: pub-cache-${{ runner.os }}-${{ hashFiles('pubspec.yaml') }}
          restore-keys: |
            pub-cache-${{ runner.os }}-

      - run: flutter pub get

      - name: Set up git and fetch history
        uses: actions/checkout@v4

      - name: Pods install and update
        run: |
          cd ./ios 
          pod install
          pod update

      - name: Bundle install for iOS Gemfile
        run: |
          cd ./ios
          bundle install

      - name: Run Fastlane
        run: |
          cd ./ios  
          bundle exec fastlane upload_to_store
        env:
          DEVELOPER_PORTAL_TEAM_ID: '${{ secrets.DEVELOPER_PORTAL_TEAM_ID }}'
          GIT_AUTHORIZATION: '${{ secrets.GIT_AUTHORIZATION }}'
          TEMP_KEYCHAIN_USER: '${{ secrets.TEMP_KEYCHAIN_USER }}'
          TEMP_KEYCHAIN_PASSWORD: '${{ secrets.TEMP_KEYCHAIN_PASSWORD }}'
          APPLE_KEY_ID: '${{ secrets.APPLE_KEY_ID }}'
          APPLE_ISSUER_ID: '${{ secrets.APPLE_ISSUER_ID }}'
          APPLE_KEY_CONTENT: '${{ secrets.APPLE_KEY_CONTENT }}'
```

## Результат

После выполнения всех шагов, вы сможете автоматически выгружать ваше приложение на **TestFlight** с помощью **GitHub
Actions** и **Fastlane**. Теперь вам не нужно тратить время на ручное создание **build**-ов и выгрузку их на
**TestFlight**. Все это можно сделать автоматически. 

![Success Deploy](images/success_deploy.png) 

![Success Details](images/success_deploy_details.png)