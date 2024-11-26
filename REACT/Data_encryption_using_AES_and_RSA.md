# Инструкция по шифрованию данных #
В данной инструкции описаны шаги, необходимые для безопасного шифрования данных перед их передачей, используя технологию AES и RSA, а также цифровую подпись.

***1. Описание алгоритма***
Шифрование данных осуществляется в несколько этапов:
- Генерация временного симметричного AES-ключа и IV (инициализационного вектора).
- Шифрование данных с использованием AES.
- Шифрование AES-ключа с использованием RSA (публичного ключа).
- Генерация временной метки.
- Создание цифровой подписи для верификации целостности данных.
- Формирование итогового пакета данных для отправки.

***2. Подготовка окружения***
Перед началом работы убедитесь, что выполнены следующие условия:

Файлы ключей:
- Публичный ключ public.pem.
- Приватный ключ private.pem.
- Разместите их в папке keys в корне проекта.

Необходимые модули:
```
npm install crypto-js node-rsa
```

***3. Код шифрования***
```
const CryptoJS = require('crypto-js');
const NodeRSA = require('node-rsa');
const fs = require('fs');
const path = require('path');

// Пути к ключам
const privateKeyPath = path.join(process.cwd(), 'keys', 'private.pem');
const publicKeyPath = path.join(process.cwd(), 'keys', 'public.pem');

// Чтение ключей
const publicKey = fs.readFileSync(publicKeyPath, 'utf8');
const privateKey = fs.readFileSync(privateKeyPath, 'utf8');

// Функция для шифрования данных
function encryptData(data) {
    // 1. Генерация AES-ключа и IV
    const aesKey = CryptoJS.lib.WordArray.random(32); // 256 бит
    const iv = CryptoJS.lib.WordArray.random(16); // 128 бит

    // 2. Шифрование данных AES
    const encryptedData = CryptoJS.AES.encrypt(JSON.stringify(data), aesKey, { iv }).ciphertext;

    // 3. Шифрование AES-ключа RSA
    const rsaPublicKey = new NodeRSA(publicKey);
    rsaPublicKey.setOptions({ encryptionScheme: 'pkcs1_oaep', signingScheme: 'sha256' });
    const encryptedAESKey = rsaPublicKey.encrypt(aesKey.toString(CryptoJS.enc.Hex), 'base64');

    // 4. Создание временной метки
    const timestamp = Date.now().toString();

    // 5. Подпись данных RSA
    const rsaPrivateKey = new NodeRSA(privateKey);
    rsaPrivateKey.setOptions({ signingScheme: 'sha256' });
    const signaturePayload = encryptedData.toString(CryptoJS.enc.Base64) + timestamp;
    const signature = rsaPrivateKey.sign(signaturePayload, 'base64');

    // 6. Форматирование данных для отправки
    return {
        data: encryptedData.toString(CryptoJS.enc.Base64),
        key: encryptedAESKey,
        iv: iv.toString(CryptoJS.enc.Base64),
        signature,
        timestamp,
    };
}

module.exports = { encryptData };
```
***4. Проверка работы***
Убедитесь, что ключи находятся в папке keys.
Вставьте тестовые данные в функцию encryptData.

Проверьте, что результат соответствует ожидаемому формату:
- data: зашифрованные данные.
- key: зашифрованный AES-ключ.
- iv: инициализационный вектор.
- signature: цифровая подпись.
- timestamp: временная метка.

***5. Рекомендации***
Безопасность ключей: 
- Ограничьте доступ к ключам.
- Приватный ключ должен быть недоступен извне.
- Мониторинг времени жизни ключей:
- Регулярно обновляйте RSA-ключи.
Логирование:
- Не логируйте открытые ключи или зашифрованные данные.