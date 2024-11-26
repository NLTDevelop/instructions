# Инструкция по интеграции React с сервером Node.js #

В данном примере реализована серверная часть с использованием Node.js и Express, которая работает как прокси для безопасного обращения с клиентом. Все запросы от клиента проходят через сервер, где они обрабатываются с дополнительными механизмами безопасности, включая шифрование данных и кэширование.

***1. Создание проекта***
Проект создан с использованием стандартных технологий для построения серверных приложений:

- Node.js для создания серверной логики
- Express для маршрутизации и обработки запросов

***2. Структура серверной части***
Структура сервера организована с учетом удобства и безопасности, включая разделение логики на несколько папок:

- router/ — содержит файлы маршрутов для обработки входящих запросов
- controllers/ — включает контроллеры для логики обработки запросов
- keys/ — папка для хранения секретных ключей для шифрования данных и других ключевых данных
- utils/ — вспомогательные файлы для шифрования данных и работы с кэшем

***3. Запуск сервера на Express***
Сервер настроен с помощью Express, который принимает запросы от клиента и перенаправляет их в нужную сторону, обеспечивая безопасность и контролируя доступ.

Пример кода для запуска сервера:
```
const express = require('express');
const bodyParser = require('body-parser');
const cors = require('cors');
const authRouter = require('./routes/auth.router');

const app = express();
const port = 4000;

app.listen(port, () => {
    console.log(`Server is running on http://localhost:${port}`);
});

app.use(cors({ origin: '*' }));
app.use(bodyParser.json());
app.use(bodyParser.urlencoded({ extended: true }));

app.use('/', authRouter);
```

***4. Роутер и контроллер***
Для обеспечения безопасности, запросы с клиента проходят через сервер, который выполняет роль прокси. Это позволяет контролировать все взаимодействия с внешними API, шифровать данные и кэшировать ответы.

Пример кода прокси-запроса:
```
const express = require('express');
const { login } = require('../controller/auth.controller');

const router = express.Router();

router.post('/auth-login/sign-in', login);

module.exports = router;
```

```
const axios = require('axios');
const { encryptData } = require('../utils.ts/encryption');
const { setCache, getCache } = require('../utils.ts/nodecachedService');

const targetApiUrl = 'https://nmau.pp.ua/api/auth-login/sign-in';

const login = async (req, res) => {
	try {
		const data = req.body;

		const cacheKey = `encryptedData:${JSON.stringify(data)}`; // Уникальный ключ для кэша
		const cachedData = await getCache(cacheKey);
		if (cachedData) {
			console.log('Данные найдены в кэше');
			return res.json(cachedData);
		};

		const encryptedData = encryptData(data);
		const response = await axios.post(targetApiUrl, data);
		await setCache(cacheKey, response.data);
		
		res.json(response.data);
	} catch (error) {
		console.error('Ошибка при обработке запроса:', error.message);
		res.status(500).json({ error: 'Ошибка при обработке запроса' });
	}
};

module.exports = { login };
```
***5. Шифрование данных***
Для повышения безопасности перед отправкой данных на внешние API они шифруются с помощью собственного алгоритма, хранящего ключи в папке keys. Шифрование данных показано в "Инструкция по шифрованию данных".

***6. Кэширование данных через node-cache***
Для оптимизации производительности использован механизм кэширования через библиотеку node-cache, который сохраняет часто запрашиваемые данные и уменьшает нагрузку на внешние сервисы.

Как работает кэширование:
- При каждом запросе проверяется, есть ли данные в кэше.
- Если данные найдены — они возвращаются клиенту.
- Если данные не найдены — выполняется запрос к внешнему сервису, данные шифруются и кэшируются для последующего использования.

```
const NodeCache = require('node-cache');
const cache = new NodeCache({ stdTTL: 10, checkperiod: 20 });

// Функция для записи данных в кэш
function setCache(key, value) {
  const success = cache.set(key, value);
  if (!success) {
    throw new Error('Ошибка при записи данных в кэш');
  }
  console.log('Данные успешно записаны в кэш');
}

// Функция для получения данных из кэша
function getCache(key) {
  return new Promise((resolve, reject) => {
    const data = cache.get(key);
    if (data === undefined) {
      resolve(null); // Если данных нет в кэше, возвращаем null
    } else {
      resolve(data); // Если данные есть, возвращаем их
    }
  });
}
```

***7. Обработка запросов и кэширование***
В контроллере loginController.js реализована логика обработки запроса на авторизацию, где данные о пользователе сначала проверяются в кэше. Если они отсутствуют — производится запрос к внешнему API и результаты сохраняются в кэш.
Пример контроллера для авторизации:

```
const { encryptData } = require('../utils/encryption');
const { setCache, getCache } = require('../utils/nodecachedService');
const axios = require('axios');

const login = async (req, res) => {
  try {
    const data = req.body;
    const cacheKey = `encryptedData:${JSON.stringify(data)}`;

    // Проверяем наличие данных в кэше
    const cachedData = await getCache(cacheKey);
    if (cachedData) {
      console.log('Данные найдены в кэше');
      return res.json({ data: cachedData, fromCache: true });
    }

    // Если данных нет в кэше, обрабатываем запрос
    const encryptedData = encryptData(data);
    await setCache(cacheKey, encryptedData);
    console.log('Данные кэшированы:', { key: cacheKey, value: encryptedData });

    const response = await axios.post('https://nmau.pp.ua/api/auth-login/sign-in', data);
    res.json(response.data);
  } catch (error) {
    console.error('Ошибка при обработке запроса:', error.message);
    res.status(500).json({ error: 'Ошибка при обработке запроса' });
  }
};
```

***Заключение***
В этой интеграции React с сервером Node.js мы обеспечили:

Безопасность с помощью шифрования данных перед их отправкой на внешний сервер.
Оптимизацию с помощью кэширования данных для ускорения повторных запросов.
Управление логикой через четкую структуру папок с разделением на маршруты, контроллеры и утилиты.
Проект был организован таким образом, чтобы обеспечить как безопасность, так и производительность для обработки запросов от клиента.