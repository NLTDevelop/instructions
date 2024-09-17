# Вступ: #
***React*** - JavaScript-бібліотека для розробки інтерфейсів користувача.
Включає такі інструменти: Webpack, Babel, Jest.<br>
https://create-react-app.dev/ 

***Webpack*** - це модульний пакувальник, який дозволяє об'єднувати різні модулі (наприклад, JavaScript-файли, CSS, зображення та інші ресурси) в один або декілька вихідних файлів.

# Більш сучасний пакувальник Vite: #
***Vite*** - це більш сучасний пакувальник, який забезпечує швидкий запуск та оновлення програми завдяки використанню нативних можливостей браузера та функції «гарячого перезавантаження» (HMR).
Основні переваги над Webpack:
- використовує нативні ES-модулі для розробки, що дозволяє йому запускатись швидше, ніж Webpack, який вимагає повного складання програми при кожній зміні.
- забезпечує миттєве оновлення лише змінених модулів, що робить процес розробки більш чуйним порівняно з Webpack, який може мати повільне оновлення у великих проектах.
- має мінімалістичну та просту конфігурацію, що спрощує налаштування та використання. У Webpack налаштування може бути складнішим і потребує великої кількості конфігураційних опцій.
- використовує механізм складання на основі Rollup для продакшен-збирання, який забезпечує більш ефективне розбиття коду та оптимізацію.
- має вбудовану підтримку для TypeScript, JSX та інших сучасних технологій, що спрощує налаштування порівняно з Webpack, де може знадобитися встановлення додаткових завантажувачів та плагінів.

# Tailwind CSS #
***Tailwind CSS*** – це утилітарний CSS-фреймворк, який надає набір класів для стилізації веб-сторінок. Замість того, щоб писати стилі в традиційному стилі (наприклад, за допомогою CSS або Sass), Tailwind CSS дозволяє використовувати певні класи для стилізації елементів.

# Shadcn/ui
***Shadcn/ui*** - це бібліотека інтерфейсів користувача, розроблена для використання з React.

# Ініціалізація проекту: #
<u>Vite</u>

1. Створення проекту:
```
npm create vite@latest
```

Далі необхідно виконати конфігурацію проекту:
- вказати назву проекту
- обрати фреймворк, що використовується (React/Next etc.)
- обрати мову програмування (JavaScript / TypeScript) c можливість встановлення SWC (швидкий компілятор JavaScript і TypeScript, який може використовуватися як альтернатива Babel)

<u>Tailwind CSS</u>
1. Установка tailwind.css та його залежностей:
```
npm install -D tailwindcss postcss autoprefixer
```
2. Генерація конфігураційних файлів (tailwind.config.js/postcss.config.js):
```
npx tailwindcss init -p
```
3. Редагування файлу tsconfig.json(замінити на):
```
{
  "files": [],
  "references": [
    {
      "path": "./tsconfig.app.json"
    },
    {
      "path": "./tsconfig.node.json"
    }
  ],
  "compilerOptions": {
    "baseUrl": ".",
    "paths": {
      "@/*": ["./src/*"]
    }
  }
}
```
4. Редагування файлу tsconfig.app.json(в compilerOptions додати):
```
"baseUrl": ".", 
"paths": { 
        "@/*": [ "./src/*" ] 
},
```
5. Оновити файл vite.config.ts:
```
plugins: [react()],
resolve: {    
      alias: {      
           "@": path.resolve(__dirname, "./src"),    
      },  
},
```
6. У файл index.css додати директиви:
```
@tailwind base;
@tailwind components;
@tailwind utilities;
```
7. Редагувати файл tailwind.config.js(необхідно додати):
```
content: [ "./index.html", "./src/**/*.{js,ts,jsx,tsx}", ],
```
8. Для автозаповнення стилів використовується плагін: ***Tailwind CSS IntelliSense***

<u>Shadcn/ui</u>
1. Підключення бібліотеки до проекту:
```
npx shadcn@latest init
```
Далі виконується конфігурація бібліотеки:
- Which style would you like to use? › New York 
- Which color would you like to use as base color? › Zinc 
- Do you want to use CSS variables for colors? › no / yes


# Посилання: #
https://vitejs.dev/guide/ - док по Vite<br>
https://ui.shadcn.com/docs/installation/vite -  док по ShadCN<br>
https://tailwindcss.com/docs/installation -  док по Tailwind
