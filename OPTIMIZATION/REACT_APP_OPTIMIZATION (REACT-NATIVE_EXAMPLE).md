# React-Native app optimization rules and recommendations
**Max Orlov 06.12.2023**

### 1. Обновление:

- **Польза обновлений:** Обновление до последних версий React Native и его зависимостей важно для получения новых функций, исправлений безопасности и улучшений производительности. Это также обеспечивает поддержку и безопасность вашего приложения.

- **Тестирование:** Перед обновлением всегда проводите тестирование приложения, чтобы удостовериться, что новые версии не приведут к конфликтам или проблемам существующего функционала.

### 2. Иерархия компонентов:

- **Разделение ответственности:** Разбиение сложных компонентов на более мелкие компоненты помогает в поддержании кода, улучшает читаемость и уменьшает сложность компонентов.

- **Перерендеринг:** Уменьшение количества пропсов и зависимостей также помогает в уменьшении вероятности ненужных перерендеров. Разбивка на более мелкие компоненты также может снизить влияние перерендеров.

### 3. Компоненты и Пропсы:

- **Гибкость с объектами:** Использование объектов для пропсов может быть удобным, особенно когда у вас много различных пропсов. Это делает код более читаемым и обслуживаемым, и новые пропсы могут быть добавлены без изменения существующего кода.

- **Типизация пропсов:** Рассмотрите введение типов для ваших пропсов, например, с использованием TypeScript или PropTypes. Это может предотвратить ошибки на этапе компиляции и улучшить поддержку кода.

Эти практики обеспечивают не только лучшую читаемость и удобство сопровождения кода, но и способствуют улучшению производительности и стабильности вашего React Native приложения.

### 4. React Native PureComponent

В React Native, для реализации функциональности аналогичной `PureComponent` из React, вы можете использовать функцию `memo` из библиотеки `react`. Она автоматически обеспечивает оптимизацию перерисовки компонента на основе поверхностного сравнения пропсов.

```jsx
import React, { memo } from 'react';

export const MemoizedComponent = memo((props) => {
  // ваш компонент
});
```

Теперь `MemoizedComponent` будет перерисовываться только при изменении пропсов.

### 5. Интерфейсы и Типы в TypeScript

При использовании TypeScript в React Native, грамотная типизация играет важную роль. Разбивайте сущности на более мелкие интерфейсы и типы для лучшей читаемости и переиспользования.

```ts
interface IUser {
  name: string;
  age: number;
  roles: TRoles;
  cards: ICard[];
}

interface ICard{
    cvv: string;
    number: number;
    expire: string
    holder: string
}

const type TRoles = 'admin' | 'user' | 'manager';
```

### 7. Использование FlatList в React Native

Для эффективного отображения списков в React Native рекомендуется использовать компонент `FlatList` вместо `ScrollView`. `FlatList` оптимизирован для работы со списками и рендерит только видимые элементы, что улучшает производительность вашего приложения.

### 8. Избегайте избыточных перерисовок

#### 8.1 Использование React.memo

`React.memo` может использоваться для предотвращения ненужных перерисовок функциональных компонентов. Компонент будет повторно рендериться только в случае изменения его пропсов.

Пример:

```jsx
import React, { memo } from 'react';

export const MyMemoizedComponent = memo((props) => {
  // ваш компонент
});
```

#### 8.2 Используйте мемоизацию с useMemo

В функциональных компонентах вы можете использовать `useMemo` для кэширования результатов сложных вычислений и избегания повторных вычислений при каждом рендере.

Пример:

```jsx
import React, { useMemo } from 'react';

const MyComponent = ({ data }) => {
  const processedData = useMemo(() => {
    // сложные вычисления
    return processData(data);
  }, [data]);

  // ваш код компонента
};
```

#### 8.3 MobX observer

Если вы используете MobX, вы можете воспользоваться оптимизациями для React, описанными в [документации MobX](https://mobx.js.org/react-optimizations.html). Использование `observer` из MobX может помочь улучшить производительность компонентов, автоматически обновляя их при изменениях в данных MobX.


### 9. Ленивая загрузка данных с использованием useEffect и Skeleton Content

При переходе на новый экран рекомендуется использовать ленивую загрузку данных, чтобы улучшить производительность. Можно использовать `useEffect` для запроса данных при монтировании экрана и отображать лоадер, пока данные не будут полностью загружены. Вы также можете использовать библиотеку `react-native-skeleton-content` для добавления эффекта загрузки.

Пример:

```jsx
import React, { useEffect, useState } from 'react';
import { View, Text } from 'react-native';
import SkeletonContent from 'react-native-skeleton-content-nonexpo';

const MyLazyLoadedScreen = () => {
  const [data, setData] = useState([]);
  const [loading, setLoading] = useState(true);

  useEffect(() => {
    // Запрос данных
    fetchData().then((result) => {
      setData(result);
      setLoading(false);
    });
  }, []);

  return (
    <View>
      {loading ? (
        <SkeletonContent
          containerStyle={{ flex: 1, width: '100%', padding: 20 }}
          isLoading={loading}
          layout={[
            { key: 'someId', width: '100%', height: 200, marginBottom: 10 },
            // Добавьте другие элементы загрузки по необходимости
          ]}
        />
      ) : (
        <View>
          {data.map((item) => (
            <Text key={item.id}>{item.title}</Text>
          ))}
        </View>
      )}
    </View>
  );
};

export default MyLazyLoadedScreen;
```

### 10. Мемоизация с использованием useMemo или useCallback

Мемоизация помогает избежать ненужных обновлений компонентов, особенно если состояние компонента большое и редко изменяется. Вы можете использовать `useMemo` или `useCallback` для кэширования результатов сложных вычислений.

Пример с `useMemo`:

```jsx
import React, { useMemo } from 'react';

const MyComponent = ({ data }) => {
  const processedData = useMemo(() => {
    // Сложные вычисления
    return processData(data);
  }, [data]);

  // Ваш код компонента
};
```

Пример с `useCallback`:

```jsx
import React, { useCallback } from 'react';

const memoizedCallback = useCallback(() => {
  // Ваш код обработки события
}, [/* зависимости */]);
```

Выберите подходящий метод в зависимости от вашего использования и требований производительности.

### 11. Кеширование данных

Для улучшения производительности и снижения количества запросов к серверу рекомендуется использовать кеширование данных. Если данные редко обновляются, их можно кэшировать и извлекать из памяти телефона. Это особенно полезно, когда пользователь переходит между экранами приложения.

### 12. Профилирование и оптимизация кода

Для обеспечения высокой производительности вашего приложения рекомендуется использовать инструменты для профилирования. React DevTools и Chrome DevTools предоставляют мощные средства для анализа производительности вашего кода.

1. **React DevTools:**
   - Установите расширение React DevTools для вашего браузера.
   - Используйте вкладку "Profiler" для анализа времени работы компонентов.

2. **Chrome DevTools:**
   - Откройте вкладку "Performance" в Chrome DevTools.

### 13. Удаление неиспользуемого кода

Удаление неиспользуемого кода помогает снизить объем проекта, улучшает читаемость кода и уменьшает возможность ошибок. Периодически просматривайте ваш код и удаляйте неиспользуемые библиотеки, компоненты и функции.

### 14. Тестирование на реальных устройствах

Тестирование производительности приложения на реальных устройствах является важным шагом для обеспечения хорошей работы на различных Android-устройствах с разными характеристиками. Виртуальные эмуляторы могут не всегда точно передавать реальные условия.

1. **Используйте физические устройства:**
   - Протестируйте приложение на нескольких физических устройствах с разными характеристиками (ресурсами, версиями Android).
   - Эмуляторы могут быть полезны для начального тестирования, но реальные устройства предоставляют более точные результаты.

2. **Профилирование производительности:**
   - Используйте инструменты для профилирования производительности, как описано в предыдущем совете.
   - Измеряйте время ответа приложения, задержки и другие показатели производительности.

3. **Оптимизация для разных устройств:**
   - При необходимости оптимизируйте ваш код и интерфейс для более слабых устройств, чтобы обеспечить хороший опыт для всех пользователей.

Тестирование на реальных устройствах позволяет выявить и решить проблемы, которые могут возникнуть на определенных устройствах и помогает создать более устойчивое приложение.