# Flutter Developer Interview Questions

## Общие вопросы

### Что такое ООП?

**Объектно-ориентированное программирование** — это парадигма программирования, основанная на представлении программы в
виде совокупности объектов, каждый из которых является экземпляром определенного класса, а классы образуют иерархию
наследования.

Основные принципы **ООП**:

- **Абстракция** - моделирование взаимодействий сущностей в виде абстрактных классов и интерфейсов для представления
  системы;
- **Инкапсуляция** - сокрытие деталей реализации объекта от внешнего мира и доступ к ним только через интерфейс;
- **Наследование** - возможность создания новых классов на основе существующих;
- **Полиморфизм** - возможность использования объектов с одинаковым интерфейсом без знания их конкретного типа.

**Класс** - это шаблон для создания объектов, который определяет состояние и поведение объекта.

**Объект** - это экземпляр класса, который содержит данные и методы для работы с ними.

--- 

### Что такое SOLID?

**SOLID** - это аббревиатура, которая описывает пять базовых принципов объектно-ориентированного программирования:

- **Принцип единственной ответственности (Single Responsibility Principle)** - класс должен иметь только одну
  ответственность;
- **Принцип открытости/закрытости (Open/Closed Principle)** - программные сущности должны быть открыты для расширения,
  но закрыты для изменения;
- **Принцип подстановки Барбары Лисков (Liskov Substitution Principle)** - объекты базового класса могут быть заменены
  объектами его производного класса без изменения свойств программы;
- **Принцип разделения интерфейса (Interface Segregation Principle)** - клиенты не должны зависеть от интерфейсов,
  которые они не используют;
- **Принцип инверсии зависимостей (Dependency Inversion Principle)** - модули верхнего уровня не должны зависеть от
  модулей нижнего уровня. Оба типа модулей должны зависеть от абстракций.

### Что такое структура данных?

Если коротко, структура данных — это контейнер, информация в котором скомпонована характерным образом. Благодаря такой
«компоновке», структура данных будет эффективна в одних операциях и неэффективна — в других. В зависимости от
конкретного сценария, данные нужно хранить в подходящем формате. У нас в распоряжении — ряд структур данных,
обеспечивающих нас такими различными форматами.

Наиболее распространенные структуры данных:

- Массивы
- Стеки
- Очереди
- Связные списки
- Деревья
- Графы
- Боры (в сущности, это тоже деревья)
- Хеш-таблицы

**Массив** — это простейшая и наиболее распространенная структура данных. Другие структуры данных, например, стеки и
очереди, производны от массивов. Каждому элементу данных присваивается положительное числовое значение, именуемое
индексом и соответствующее положению этого элемента в массиве. В большинстве языков программирования элементы в массиве
нумеруются с 0.

Существуют массивы двух типов:

- Одномерные
- Многомерные (массивы, в которые вложены другие массивы)

**Стеки** - это линейные структуры данных, элементы в которых хранятся в последовательном порядке.
Стек можно сравнить с высокой стопкой книг. Если вам нужна какая-то книга, лежащая около центра стопки, вам сначала
придется снять все книги, лежащие выше. Именно так работает принцип LIFO (Последним пришел — первым вышел).

**Очереди**, как и стек — это линейная структура данных, элементы в которой хранятся в последовательном порядке.
Единственное существенное отличие между стеком и очередью заключается в том, что в очереди вместо LIFO действует принцип
FIFO (Первым пришел — первым вышел).
Идеальный реалистичный пример очереди — это и есть очередь покупателей в билетную кассу. Новый покупатель становится в
самый хвост очереди, а не в начало. Тот же, кто стоит в очереди первым, первым приобретет билет и первым ее покинет.

**Связный список** — еще одна важная линейная структура данных, на первый взгляд напоминающая массив. Однако, связный
список отличается от массива по выделению памяти, внутренней структуре и по тому, как в нем выполняются базовые операции
вставки и удаления.

Связный список напоминает цепочку узлов, в каждом из которых содержится информация: например, данные и указатель на
следующий узел в цепочке. Есть головной указатель, соответствующий первому элементу в связном списке, и, если список
пуст, то он направлен просто на null (ничто).

При помощи связных списков реализуются файловые системы, хеш-таблицы и списки смежности.

Существуют такие типы связных списков:

- Односвязный список (однонаправленный)
- Двусвязный список (двунаправленный)

**Граф** — это множество узлов, соединенных друг с другом в виде сети. Узлы также называются вершинами. Пара (x,y)
называется ребром, это означает, что вершина x соединена с вершиной y. Ребро может иметь вес/стоимость — показатель,
характеризующий, насколько затратен переход от вершины x к вершине y.

Типы графов:

- Неориентированный граф - ребра не имеют направления
- Ориентированный граф - ребра имеют направление

В языке программирования графы могут быть двух видов:

- Матрица смежности - двумерный массив, в котором хранится информация о ребрах
- Список смежности - список, в котором хранится информация о вершинах, смежных с данной

**Дерево** — это иерархическая структура данных, состоящая из вершин (узлов) и ребер, которые их соединяют. Деревья
подобны графам, однако, ключевое отличие дерева от графа таково: в дереве не бывает циклов.

Деревья широко используются в области искусственного интеллекта и в сложных алгоритмах, выступая в качестве эффективного
хранилища информации при решении задач.

**Бор**, также именуемый «префиксное дерево» — это древовидная структура данных, которая особенно эффективна при решении
задач на строки. Она обеспечивает быстрое извлечение данных и чаще всего применяется для поиска слов в словаре,
автозавершений в поисковике и даже для IP-маршрутизации.

**Хеширование** — это процесс, применяемый для уникальной идентификации объектов и сохранения каждого объекта по заранее
вычисленному индексу, именуемому его «ключом». Таким образом, объект хранится в виде «ключ-значение», а коллекция таких
объектов называется «словарь». Каждый объект можно искать по его ключу. Существуют разные структуры данных, построенные
по принципу хеширования, но чаще всего из таких структур применяется хеш-таблица.

---

### Императивное и декларативное программирование

- **Императивный стиль** - описываем, как добиться желаемого результата
- **Декларативный стиль** - описываем, какой именно результат нам нужен

---

### Стек и куча

- **Стек** — это область оперативной памяти, в которой хранятся временные данные, таких как локальные переменные и
  адреса возврата функций. Объем памяти, выделенный под стек, ограничен. Стек работает в порядке LIFO
- **Куча** — это область оперативной памяти, в которой хранятся данные, созданные во время выполнения программы. Куча
  используется для динамического выделения памяти для объектов, которые могут изменять размер во время выполнения
  программы. Размер кучи задаётся при запуске приложения, но, в отличие от стека, он ограничен лишь физически. Выделение
  памяти в куче происходит медленнее, чем в стеке.

---

### DI и Service Locator

- **DI** - передача зависимостей класса через параметры конструктора.
- **Service Locator** - синглтон / класс с набором статических методов. Доступ к Service Locator может производиться из
  любого место в коде. В этом заключается его основной минус

## Общие вопросы по Dart

### Отличия final и const

- **final** - переменная, значение которой устанавливается только один раз и не может быть изменено после этого. При
  этом, значение переменной может быть установлено во время выполнения программы. Переменная final не обязательно должна
  быть инициализирована в момент объявления.
- **const** - переменная, значение которой устанавливается только один раз и не может быть изменено после этого. При
  этом, значение переменной должно быть установлено во время компиляции программы. Переменная const обязательно должна
  быть инициализирована в момент объявления.

---

### Что такое JIT и AOT компиляция?

- **JIT (Just-In-Time)** - компиляция во время выполнения программы. Программа компилируется в машинный код во время
  выполнения программы. Программа запускается быстрее, но работает медленнее. Используется во время разработки.
- **AOT (Ahead-Of-Time)** - компиляция до выполнения программы. Программа компилируется в машинный код до выполнения
  программы. Программа запускается медленнее, но работает быстрее. Используется во время релиза.

---

### Какие отличия между Hot Restart и Hot Reload?

- **Hot Reload** загружает изменения в Dart VM и ребилдит дерево виджетов, сохраняя состояние. Не перезапускает main() и
  initState(). Позволяет быстро вносить изменения в приложение.
- **Hot Restart** загружает изменения в Dart VM и перезагружает всё приложение. Перезапускает main() и initState().

---

### Что такое hashcode?

**Хэш-код** - геттер, у любого объекта, который возвращает int. Нужен при сохранении объекта в map или set. Хэш-коды
должны быть одинаковыми для объектов, которые равны друг другу в соответствии с оператором ==
int get hashCode => Object.hash(runtimeType, ..., ...);

---

### Что такое extension?

**Extension** — это синтаксический сахар, который позволяет расширить существующий класс (добавить методы, операторы,
сеттеры и геттеры). При этом, класс, который расширяется, не изменяется.

--- 

### Что такое mixin?

**Миксин** - это механизм множественного наследования, который позволяет классам использовать функциональность других
классов без явного наследования.

Миксины в Dart определяются ключевым словом mixin. Они могут содержать методы, поля и геттеры/сеттеры, но не могут иметь
конструкторов. Вместо этого, миксины инициализируются автоматически, когда они применяются к классу. Для использования
миксинов применяется оператор with

Если у миксинов будет метод с одинаковым названием, то останется реализация, которая указана в последнем миксине. Так
как миксины будут переопределять этот метод

--- 

### Система типов в Dart

![System Type](images/system_type.png)
С появлением **null safety** в Dart, иерархия классов и интерфейсов была изменена для учета новых требований по
безопасности типов. Вот основные изменения:

1. Добавление non-nullable типов:
    - Non-nullable типы обозначают, что значение не может быть null.
    - Все существующие типы были разделены на non-nullable и nullable версии. Например, int стал int (non-nullable) и
      int?(nullable)
2. Новый корень иерархии - "Object?":
    - Введен новый корневой класс Object?, который может быть null. В предыдущих версиях Dart, корневым классом был
      Object
3. Изменения в иерархии ошибок:
    - Введен новый класс NullThrownError, который представляет собой ошибку, возникающую при попытке выбросить null
      исключение
4. late и required:
    - Введены ключевые слова late и required для обозначения переменных, которые могут быть инициализированы позднее и
      обязательно должны быть проинициализированы при объявлении, соответственно.

---

### В чем отличие dynamic, var и Object?

- **dynamic** - переменная с типом dynamic может содержать любое значение и тип. Проверка типов не производится во время
  компиляции, а только во время выполнения программы.
- **var** - переменная с типом var определяется во время компиляции и не может быть изменена после этого. При этом, тип
  переменной определяется автоматически на основе значения, которое ей присваивается.
- **Object** - переменная с типом Object может содержать любое значение и тип. Проверка типов производится во время
  компиляции.

---

### Что такое Late

**Late** - это ключевое слово в dart, которое позволяет объявить non-nullable переменную и при этом не установить для
нее значение. Значение инициализируется только тогда, когда мы к нему обращаемся. Late переменные могут быть только
non-nullable.

---

### Что такое Generics

**Generics** - это параметризованные типы. Они позволяют программе уйти от жесткой привязки к определенным типам,
определить функционал так, чтобы он мог использовать данные любых типов и обеспечить их безопасность. Так же
обобщения снижают повторяемость кода, дают вам возможность предоставить единый интерфейс и реализацию для многих
типов.

---

### Dart VM

Dart VM (Dart virtual machine) - среда выполнения Dart. Dart VM является основным компонентом Dart SDK и используется
для запуска Dart кода. Состоит из следующих компонентов:

- Среда исполнения
- Сборщик мусора
- Основные библиотеки и нативные методы
- Система отладка
- Профилировщик
- Симулятор ARM архитектуры

---

### Что такое зоны в Dart?

**Зона** - это механизм, который позволяет управлять и обрабатывать ошибки и другие события, происходящие в определенных
областях кода.

- Защита вашего приложения от завершения из-за необработанного исключения
- Ассоциирование данных, известных как zone-local values, с отдельными зонами
- Переопределение ограниченного набора методов, таких как print() и scheduleMicrotask(), внутри части или всего кода
- Выполнение операции каждый раз, когда код входит или выходит из зоны. Эти операции могут включать в себя запуск или
  остановку таймера, или сохранение stacktrace-а

### Какие есть классы для ошибок и исключений?

- **Exception** - это общий класс для исключений, которые обычно возникают из-за ошибок в программе, и их можно
  обработать и восстановиться от них.
- **Error** - это класс для ошибок, которые обычно не могут быть восстановлены, и они указывают на серьезные проблемы в
  программе или системе.

--- 

### Что такое тип Never?

**Never** - это тип, означающий, что ни один тип не разрешен и Never сам по себе не может быть создан. Используется
как возвращаемый тип при гарантированной ошибке. Например, функция, которая всегда бросает исключение, имеет тип
Never. Также используется для функций, которые никогда не завершаются.

--- 

### Для чего необходимо ключевое слово Covariant?

**Covariant** - это ключевое слово в dart, которое указывает на то, что тип возвращаемого значения может быть изменен
на более узкий тип в подклассе. Это позволяет использовать подтипы вместо супертипов.

--- 

### Что такое аннотации?

**Аннотации** — это синтаксические метаданные, которые могут быть добавлены к коду. Другими словами, это возможность
добавить дополнительную информацию к любому компоненту кода, например, к классу или методу. Аннотации всегда начинаются
с символа @ (@override, @required). Любой класс может служить аннотацией, если в нем определен const конструктор.
Аннотации могут использоваться для различных целей, таких как:

- Пометка кода для статического анализа
- Генерация кода
- Отладка
- Документирование
- Определение метаданных
- т.д.

## Асинхронность и многопоточность

### Что представляет собой Future?

**Future** - это обёртка над результатом выполнения асинхронной операции. Код Future НЕ выполняется параллельно, а
выполняется в последовательности, определяемой Event Loop. Future может находиться в одном из трех состояний:

- **Uncompleted** - операция не завершена
- **Completed with Result** - операция завершена успешно
- **Completed with Error** - операция завершена с ошибкой

Future имеет следующие типы конструкторов:

- **Future(FutureOr<T> computation())**: создает объект future, который с помощью метода Timer.run запускает функцию
  computation асинхронно и возвращает ее результат.
- **FutureOr<T>**: указывает, что функция computation должна возвращать либо объект Future, либо объект типа T.
  Например,
  чтобы получить объект Future, функция computation должна возвращать либо объект Future, либо объект int
- **Future.delayed(Duration duration, [FutureOr<T> computation()])**: создает объект Future, который запускается после
  временной задержки, указанной через первый параметр Duration. Второй необязательный параметр указывает на функцию,
  которая запускается после этой задержки.
- **Future.error(Object error, [StackTrace stackTrace])**: создает объект Future, который содержит информацию о
  возникшей
  ошибке.
- **Future.microtask(FutureOr<T> computation())**: создает объект Future, который с помощью функции scheduleMicrotask
  запускает функцию computation асинхронно и возвращает ее результат.
- **Future.sync(FutureOr<T> computation())**: создает объект Future, который содержит результат немедленно вызываемой
  функции computation.
- **Future.value([FutureOr<T> value])**: создает объект Future, который содержит значение value.

---

### Как работает await?

**await** - это ключевое слово, которое используется в асинхронной функции для ожидания завершения Future. Когда код
доходит до await, выполнение функции приостанавливается до тех пор, пока Future не завершится. После этого выполнение
кода продолжается. Под капотом await перемещает весь последующий код в then у Future, которую мы дожидаемся.

---

### Что такое Event Loop?

**Event Loop** - вечный цикл, выполняющий все поступающие в изолят задачи. В нём есть две FIFO очереди задач:

- Очередь MicroTask. Используется для очень коротких действий, которые должны быть выполнены асинхронно, сразу после
  завершения какой-либо инструкции перед тем, как передать управление обратно Event Loop. Очередь MicroTask имеет
  приоритет перед очередью Event. Используется для планирования операций, которые должны быть выполнены сразу после
  текущей операции.
- Очередь Event. Используется для планирования операций, которые получают результат от внешних событий (операции
  ввода/вывода, жесты, рисование, таймеры, потоки). Очередь Event обрабатывается после очереди MicroTask.

---

### Что такое Completer?

**Completer** позволяет поставлять Future, отправлять событие о выполнении или событие об ошибке. Это может быть
полезно, когда нужно сделать цепочку Future и вернуть результат.

---

### Что такое Stream и какие виды Stream существуют?

**Stream** - это последовательность асинхронных событий. Stream сообщает вам, что есть событие и когда оно будет
готово. Существует два вида Stream:

- Single subscription - это вид потока, при котором может быть только один подписчик.
- Broadcast - это вид потока, при котором может быть много подписчиков. При этом Broadcast стримы отдают свои данные вне
  зависимости от того, подписан ли кто-нибудь на них или нет. Подписчики стрима получают события только с момента
  подписки, а не с момента старта жизни стрима

---

### Что такое генераторы и какие виды генераторов существуют?

Генераторы (sync* / async*) - генератор это ключевое слово, которое позволяет создавать последовательность значений
с помощью yield. Существует два вида генераторов:

- **sync** - это синхронный генератор. Возвращает Iterable.
- **async** - это aсинхронный генератор. Возвращает Stream

---

## Многопоточность в Dart и Flutter

### Как обстоят дела с многопоточностью в Dart?

**Dart** — однопоточный язык программирования. Он исполняет одновременно одну инструкцию. Но при этом мы можем запустить
код в отдельный поток с помощью Isolate

---

### Что такое Isolate и Compute? Какие проблемы многопоточности существуют?

**Isolate** - это легковесный процесс (поток исполнения), который выполняется параллельно с другими потоками и
процессами в приложении. Каждый Isolate в Dart имеет свой собственный экземпляр виртуальной машины Dart, собственную
память и управляется с помощью своего Event Loop.

**Compute** - это функция, которая создаёт изолят и запускает переданный код.

Среди проблем многопоточности можно выделить:

- **Deadlock** — каждый из потоков ожидают событий, которые могут предоставить другие потоки
- **Race conditions** — проявление недетерминизма исполнителя программы при различном относительном порядке исполнения
  команд в различных потоках
- **Lock Contention** — основное время потока проводится не в исполнении полезной работы, а в ожидании блокированного
  другим потоком ресурса
- **Live Lock** — поток захватывает ресурс, но после того, как убедится, что завершить работу не может, освобождает
  ресурс, аннулируя результаты

## Общие вопросы по Flutter

### Что такое Stateless и Stateful?

- **StatelessWidget** - это виджет, который не имеет состояния, в процессе работы приложения не изменяет своих свойств.
  Они могут изменяться лишь посредством внешних событий, которые возникают в родительских виджетах.
- **StatefulWidget** - это виджет, который хранит состояние, в процессе работы приложения он может его изменять
  динамически с помощью setState().

### В чем отличие package и plugin в Flutter?

**Плагины (Plugin)** - если вкратце - нативные разработки.
Плагин Flutter — это оболочка собственного кода, такого как Android (Kotlin или Java) и iOS (swift или Objective C).
Flutter может делать все, что может собственное приложение, за счет использования каналов платформы и передачи
сообщений.

**Пакеты (Package)** - это библиотеки, которые содержат код, ресурсы и метаданные, предоставленные другими
разработчиками в экосистемах Flutter и Dart. Это позволяет быстро создать приложение без необходимости разрабатывать все
с нуля.

---

### Что такое pubspec.yaml файл?

**pubspec.yaml** - это файл конфигурации проекта Flutter, который содержит информацию о зависимостях проекта, таких как
пакеты и их версии, шрифты и т.д. Он гарантирует, что версия пакета будет такой же, как и в следующий раз, когда вы его
создадите. Вы также можете наложить ограничения на приложение. Этот файл конфигурации проекта будет использоваться очень
часто при работе с проектом Flutter. Эта спецификация написана на YAML, читаемом языке разметки.

### Что будет если запустить несколько runApp()?

6. Can you tell us how many kinds of widgets there are in Flutter?
   There are two main types of widgets in Flutter. These include:

StatelessWidget- It does not have any state information. It is static throughout its lifecycle. Examples are Row, Text,
Column, and Container.

StatefulWidget- It has state information. It contains two classes: the state object and the Widget. It is dynamic
because it can change the inner data during the Widget's lifetime. Examples are Radio, Form, Checkbox, and TextField.

8. runApp

Explain the term “Tree shaking” in Flutter.
Hide Answer
Tree shaking is a method of removing the unused module in the bundle during the development process. Tree shaking serves
as a sort of optimization technique that optimizes the code by removing the dead code.

While importing or exporting codes, there might be dead codes hanging around. Removing these dead codes reduces the code
size which in turn improves the performance of the application.

10. What's the role of BuildContext in Flutter?
    Hide Answer
    In Flutter, the BuildContext is an object that provides access to the location of a widget in the widget tree
    hierarchy and to various services such as Theme, MediaQuery, and Navigator. The BuildContext is used by widgets to
    access the properties of their parent widget, such as its size, position, and theme. It is also used to navigate
    between screens using the Navigator widget.

11.

What process will you use to reduce widget rebuild?
On rebuilding, the state of the widget changes. This, however, helps the user to see the UI reflect state changes. At
this point recreating sections of the user interface that do not need to be changed is unnecessary.

To avoid the needless rebuilding of the widgets one can divide the widget tree into small individual widgets each having
its own build process. Here const constructor can be used to inform Flutter that the dont need to be rebuilt.

## INTERMEDIATE FLUTTER INTERVIEW QUESTIONS AND ANSWERS

4.

What do you mean by Container class?
The container class is the convenience widget that enables positioning, sizing, and painting of widgets. A container
class can include multiple widgets and it enables developers to manage those widgets according to their convenience.

5. Can you name some popular database packages in Flutter?
6. Can you tell us some differences between const and final in Flutter?
   The only difference between const and final is that the const variables are evaluated at compile-time and are
   immutable whereas final variables are evaluated at runtime and can only be set once.
7. How would you optimize the performance of a Flutter app?
   Some techniques to optimize the performance of a Flutter app include using the const keyword to make widgets
   immutable, avoiding unnecessary widget rebuilds, using the Provider package for efficient state management, and
   minimizing the number of expensive operations in the build method.
   So, if your app is small, you can pass your data using the constructor of the widget class, but for a larger app,
   this
   is not an easy task. Unknowingly we use inherited widgets in many places while developing the flutter app.Theme.of(
   context), Navigator.of(context), and MediQuery.of(context).
8. Differentiate between setState and Provider?
   The setState() is used for managing the local state. Calling the setState() function notifies the framework about the
   change in the state of the object and that may affect the user interaction in the subtree.

Whereas, provider is a state management technique in Flutter that allows widgets to access data from a central
location (i.e., a "provider"). Providers can be used to manage the application state, such as user authentication or
data fetched from an API.

9.

Can you state some difference between runApp() and main()?
Main(): Main() function starts the program. You cannot write a program in Flutter without using the main() function
whereas runApp() is used to launch the software. RunApp() allows you to return the widgets that are connected to the
screen as the widget tree’s root.

10. What’s the need of mixins?
    Multiple inheritances are not supported in Dart. Hence, you would need mixins to use multiple inheritance in
    Flutter, as
    they allow you to write reusable class code in multiple class hierarchies.


15. What is the difference between push and pushReplacement methods in Flutter?

In Flutter, push and pushReplacement are two methods that are used to navigate between different screens in an app. Both
methods are available on the Navigator class, which manages the navigation stack in a Flutter app.

The push method is used to push a new route onto the navigation stack, which adds a new screen to the app’s UI. This
method does not remove the previous screen from the stack, which means that the user can use the back button or swipe
gesture to navigate back to the previous screen.
The pushReplacement method is similar to the push method, but it replaces the current screen on the navigation stack
with a new screen. This means that the previous screen is removed from the stack and cannot be navigated back to using
the back button or swipe gesture.
So, the main difference between push and pushReplacement methods is that push adds a new screen to the navigation stack
while pushReplacement replaces the current screen with a new screen.

18. Access modifiers in Dart
    Dart offers a set of access modifiers to control the visibility of members: public (default, if no modifier is
    specified), private (indicated by a leading underscore _), and protected (not explicitly available but achieved
    through conventions). Dart's approach to privacy is library-based, meaning that private members are hidden within
    the same library file but can be accessed across classes within that file.

19. Difference between Named Construction and Factory
    In Dart, a named constructor allows a class to define multiple ways to initialize, using different names for
    clarity. It directly creates a new instance of the class. On the other hand, a factory is a special kind of
    constructor that doesn't always return a new instance. Instead, it can return an existing instance, an instance of a
    subtype, or even an instance of a completely different class. While named constructors offer varied initialization
    methods, factories provide greater control over the object creation process.

23. cascade and spread operators
    The cascade operator (..) allows for performing a series of operations on a single object without breaking the
    chain. For instance:
    var obj = Object()..method1()..method2();
    The spread operator (...) is used to insert multiple elements from one collection into another. It's especially
    useful when constructing lists or other collections:
    var list = [1, 2, ...otherList, 3];
28. State Managers
    In Flutter, state management refers to the way developers handle the data used by the app to influence its behavior
    and appearance. It's about maintaining and manipulating the state, or data, of a widget, and determining how the
    changes in state reflect in the UI.
    InheritedWidget is a foundational class in Flutter, which is particularly useful for small to medium-sized projects.
    It simplifies the transfer of data down the widget tree, eliminating the need for numerous constructor arguments,
    making the code cleaner and more manageable.
    The Provider Package built atop InheritedWidget, is suitable for medium to large-sized projects, offering a range of
    features for handling state, including dependency injection, and it encapsulates common patterns of using
    InheritedWidget, making it more user-friendly.
    Bloc Pattern is ideal for managing the state in large, complex projects. It promotes a clear separation between the
    user interface and business logic, making the components of the application easier to debug and test.
    The Redux Pattern, originally developed for JavaScript applications, maintains all the application’s state
    information in a single entity called the store. It provides a single source of truth, making it easier to
    conceptualize the state of the application, but might be overkill for simpler state needs.
    MobX is another approach, best suited for developers who prefer working with reactive programming paradigms. It
    provides a reactive state that automatically updates the UI when the state changes, making state management seamless
    and efficient.
    The choice of approach should align with the project’s complexity and specific requirements, ensuring smooth
    development and optimal app performance.
29. Bloc vs Cubit
    In Flutter, Bloc and Cubit are distinct state management solutions with unique mechanisms, catering to different
    levels of complexity.
    Bloc, ideal for more complex scenarios, employs a reactive programming model, using streams and requiring the
    definition of events and states to manage state transitions meticulously. It’s particularly useful when multiple
    states and transitions are involved, necessitating a detailed and structured approach.
    On the other hand, Cubit is simpler and more direct, eliminating the need for event definitions and allowing state
    changes through simple function calls. This makes Cubit suitable for situations where simplicity and rapid
    development are crucial.
    In essence, while Bloc offers structured solutions for intricate scenarios, Cubit is optimal for simpler, more
    straightforward state management needs.

---



---
Жизненный цикл Stateful виджета

createState() вызывается единожды и создает изменяемое состояние для этого виджета в заданном месте в дереве
mounted is true
initState() вызывается единожды при инициализации
didChangeDependencies() вызывается единожды после инициализации и далее при уведомлениях от Inhherited-виджетов вверху
по дереву, от которых зависит виджет
build() вызывается каждый раз при перерисовке
didUpdateWidget(Widget oldWidget) вызывается каждый раз при обновлении конфигурации виджета
setState() вызывается императивно для перерисовки
deactivate() вызывается, когда ранее активный элемент перемещается в список неактивных элементов, при этом удаляясь из
дерева
dispose() вызывается, когда этот объект удаляется из дерева навсегда
mounted is false

---
Деревья виджетов

![Widget Tree](images/widget_tree.png)
Widget Tree состоит из Widget, которые используются для описания пользовательского интерфейса
Element Tree состоит из Element, которые управляют жизненым циклом виджета и связывают виджеты и объекты рендеринга.
Render Tree состоит из RenderObject, которые используются для определения размеров, положения, геометрии, определения
зон экрана, на которые могут повлиять жесты

Widget

Widget - это иммутабельное описание части пользовательского интерфейса. Виджет связан с элементом, который управляет
рендерингом. Виджеты образуют сруктуру, а не дерево

Element

Element - это мутабельное представление виджета в определенном месте дерева. Управляют жизненым циклом, связывают
виджеты и объекты рендеринга.

RenderObject

RenderObject - это мутабельный объект дерева визуализации. У него есть родительский объект, а также поле с данными,
которое родительский объект использует для хранения специфичной информации, касающейся самого этого объекта, например,
его позицию. Данный объект отвечает за отрисовку, учёт размеров и ограничений, прослушивание и обработку нажатий. При
необходимости перерисовки помечается как dirty. Перерисовывается, используя свой метод layer

Виды виджетов

Proxy - это виджеты, которые хранят некоторую информацию и делают её доступной для потомков. Эти виджеты не принимают
непосредственного участия в формировании пользовательского интерфейса, но используются для получения информации, которую
они могут предоставить.

InheritedWidget
ParentDataWidget (LayoutId, Flexible, KeepAlive и т.д.)
NotificationListener
Renderer - это виджеты, которые имеют непосредственное отношение к компоновке экрана, поскольку они определяют размеры,
положение, отрисовку

Row
Column
Stack
Padding
Align
Opacity
Component - это виджеты, которые предоставляют непосредственно не окончательную информацию, связанную с размерами,
позициями, внешним видом, а скорее данные (или подсказки), которые будут использоваться для получения той самой
финальной информации

RaisedButton
Scaffold
Text
GestureDetector
Container
Виды элементов

![Element Tree](images/element_tree.png)
ComponentElement - компоновочный элемент, который явно не содержит логику рисования/отображения. Есть метод build(),
который возвращает виджет. Образуется только при создании виджетов StatelessWidget, StatefulWidget, InheritedWidget.

ProxyElement
StatelessElement
StatefulElement
RenderObjectElement - отображающий элемент, явно участвующий в рисовании компонентов на экране. Содержит renderObject и
наследуется от класса Element. Образуется при создании виджетов Padding, Column, Row, Center и др.

LeafRenderObjectElement
ListWheelElement
MultiChildRenderObjectElement
RootRenderObjectElement
SingleChildRenderObjectElement
SliverMultiBoxAdaptorElement
SlottedRenderObjectElement
Жизненный цикл Element-а

Элемент создаётся посредством вызова метода Widget.createElement и конфигурируется экземпляром виджета, у которого был
вызван метод.
С помощью метода mount созданный элемент добавляется в заданную позицию родительского элемента. При вызове данного
метода также ассоциируются дочерние виджеты и элементам сопоставляются объекты дерева рендеринга.
Виджет становится активным и должен появиться на экране.
В случае изменения виджета, связанного с элементом (например, если родительский элемент изменился), есть несколько
вариантов развития событий. Если новый виджет имеет такой же runtimeType и key, то элемент связывается с ним. В
противном случае, текущий элемент удаляется из дерева, а для нового виджета создаётся и ассоциируется с ним новый
элемент.
В случае, если родительский элемент решит удалить дочерний элемент, или промежуточный между ними, это приведет к
удалению объекта рендеринга и переместит данный элемент в список неактивных, что приведет к деактивации элемента.
Когда элемент считается неактивным, он не находится на экране. Элемент может находиться в неактивном состоянии только до
конца текущего фрейма, если за это время он остается неактивным, он демонтируется, после этого считается несуществующим
и больше не будет включен в дерево.
При повторном включении в дерево элементов, например, если элемент или его предки имеют глобальный ключ, он будет удален
из списка неактивных элементов, будет вызван метод activate, и рендер объект, сопоставленный данному элементу, снова
будет встроен в дерево рендеринга. Это означает, что элемент должен снова появиться на экране.

Флаттер под капотом
![Flutter](images/flutter_structure.png)
Уровень фреймворка — всё, с чем мы работаем в момент написания приложения, и все служебные классы, позволяющие
взаимодействовать написанному нами с уровнем движка. Всё, относящееся к данному уровню написано на Dart. Flutter
Framework взаимодействует с Flutter Engine через слой абстракции, называемый Window

Уровень движка — более низкий уровень, чем уровень фреймворка, содержит классы и библиотеки, позволяющие работать уровню
фреймворка. В том числе виртуальная машина Dart, Skia и тд.

Уровень платформы — специфичные механизмы, относящиеся к конкретной платформе запуска.

Flutter Engine уведомляет Flutter Framework, когда:

Событие, представляющее интерес, происходит на уровне устройства (изменение ориентации, изменение настроек, проблема с
памятью, состояние работы приложения…)
Какое-то событие происходит на уровне стекла (жест)
Канал платформы отправляет некоторые данные
Но также и в основном, когда Flutter Engine готов к рендерингу нового кадра
Модель выполнения во Flutter

Создается и запускается новый процесс — Thread (Isolate). Это единственный процесс, в котором будет выполняться ваше
приложение.
Инициализируются две очереди с MicroTask и Event, тип очередей FIFO (прим.: first in first out, т.е. сообщение,
пришедшие раньше, будут раньше обработаны)
Исполняется функция main()
Запускается Event Loop. Он управлет порядком исполнения вашего кода, в зависимости от содержимого двух очередей:
MicroTask и Event. Представляет собой "бесконечный" цикл.
Event Loop с определённой частотой проверяет MicroTask и Event. Если есть что-то в MicroTask, то оно выполняется перед
очередью Event.

WidgetsFlutterBinding

WidgetsFlutterBinding — конкретная реализация привязки приложений на основе инфраструктуры виджетов. По сути своей — это
клей, соединяющий фреймворк и движок Flutter. WidgetsFlutterBinding состоит из множества связей: GestureBinding,
ServicesBinding, SchedulerBinding, PaintingBinding, SemanticsBinding, RendererBinding, WidgetsBinding.

Метод scheduleAttachRootWidget является отложенной реализацией attachRootWidget. Принадлежит данный метод
WidgetsBinding. В описании к нему сказано, что он присоединяет переданный виджет к renderViewElement — корневому
элементу дерева элементов.

Метод scheduleWarmUpFrame принадлежит SchedulerBinding и используется для того, чтобы запланировать запуск кадра как
можно скорее, не ожидая системного сигнала Vsync.

Bindings

![Bindings](images/binding.png)

Bindings - это классы для обмена данными между Flutter Framework и Flutter Engine. Каждая привязка отвечает за обработку
набора конкретных задач, действий, событий, сгруппированных по области деятельности.

BaseBinding — базовый абстрактный класс, давайте тогда рассмотрим конкретные реализации биндингов. Среди них мы увидим:

ServicesBinding отвечает за перенаправление сообщений от текущей платформы в обработчик данных сообщений (
BinaryMessenger);

PaintingBinding отвечает за связь с библиотекой отрисовки.

RenderBinding отвечает за связь между деревом рендеринга и движком Flutter.

WidgetBinding отвечает за связь между деревом виджетов и движком Flutter.

SchedulerBinding — планировщик очередных задач, таких как:

вызовы приходящих колбеков, которые инициирует система в Window.onBeginFrame — например события тикеров и контроллеров
анимаций;
вызовы непрерывных колбеков, которые инициирует система Window.onDrawFrame, например, события для обновления системы
отображения после того, как отработают приходящие колбеки;
посткадровые колбеки, которые вызываются после непрерывных колбеков, перед возвратом из Window.onDrawFrame;
задачи не связанные с рендерингом, которые должны быть выполнены между кадрами.
SemanticsBinding отвечает за связь слоя семантики и движком Flutter.

GestureBinding отвечает за работу с подсистемой жестов.

Каналы платформы

![Platform Channels](images/platfrom_channel.png)

(!) Платформенные взаимодействия возможны только в главном изоляте. Этот тот изолят, который создается при запуске
вашего приложения.

Канал платформы — это двусторонний канал связи между кодом на dart и нативом, который объединяет имя канала и кодек для
кодирования сообщений в двоичную форму и обратно. Вызовы асинхронны. Каждый канал должен иметь уникальный идентификатор.

Каналы сообщений - это каналы платформы, предназначенные для обмена сообщениями между нативным кодом и
flutter-приложением.
Кодеки сообщений:

BinaryCodec Реализуя сопоставление идентификаторов в байтовых буферах, этот кодек позволяет вам наслаждаться удобством
объектов канала в тех случаях, когда вам не требуется кодирование/декодирование. Каналы сообщений Dart с этим кодеком
имеют тип BasicMessageChannel.
JSONMessageCodec Работает с «JSON-подобными» значениями (строки, числа, логические значения, null, списки этих значений
и мапы строка-ключ с этими данными). Списки и мапы неоднородны и могут быть вложены друг в друга. Во время кодирования
значения преобразуются в строки JSON, а затем в байты с использованием UTF-8. Каналы сообщений Dart имеют тип
BasicMessageChannel с этим кодеком.
StandardMessageCodec Работает с несколько более обобщенными значениями, чем кодек JSON, поддерживая также однородные
буферы данных (UInt8List, Int32List, Int64List, Float64List) и мапы с нестроковыми ключами. Обработка чисел отличается
от JSON тем, что целые числа Dart поступают на платформу как 32- или 64-битные целые числа со знаком, в зависимости от
величины никогда как числа с плавающей запятой. Значения кодируются в специальном, достаточно компактном и расширяемом
двоичном формате. Стандартный кодек предназначен для выбора по умолчанию для канала связи во Flutter. Что касается JSON,
каналы сообщений Dart, созданные с использованием стандартного кодека, имеют тип BasicMessageChannel.
Каналы методов — это каналы платформы, предназначенные для вызова нативного кода из flutter-приложения.
Кодеки методов:

StandardMethodCodec делегирует кодирование значений полезной нагрузки (payload) в StandardMessageCodec. Поскольку
последний является расширяемым, то же самое можно сказать и о первом.
JSONMethodCodec делегирует кодирование значений полезной нагрузки (payload) в JSONMessageCodec.
Каналы событий — это специализированные каналы платформы, предназначенные для использования в случае представления
событий платформы Flutter в виде потока Dart. Работает как обычный Stream

## Анимации в Flutter

Этапы анимации

Ticker просит SchedulerBinding зарегистрировать обратный вызов и сообщить Flutter Engine, что надо разбудить его, когда
появится новый обратный вызов.
Когда Flutter Engine готов, он вызывает SchedulerBinding через запрос onBeginFrame.
SchedulerBinding обращается к списку обратных вызовов ticker и выполняет каждый из них.
Каждый tick перехватывается "заинтересованным" контроллером для его обработки.
Если анимация завершена, то ticker "отключён", иначе ticker запрашивает SchedulerBinding для планирования нового
обратного вызова.
...
Виды анимаций

Tween animation. Начало, конец, время, скорость заранее определенно
Physics-based animation. Имитируют реальное поведение
Что такое Tween

Tween - это объект, который описывает между какими значениями анимируется виджет и отвечает за вычисление текущего
значения анимации

Tween анимации

Implicit Animations - это набор Implicitly Animated Widgets, которые анимируются самостоятельно при их перестройке с
новыми аргументами. (AnimatedAlign, AnimatedContainer, AnimatedPadding и т.д.)
Explicit Animations - это набор элементов управления анимационными эффектами. Предоставляют куда больше контроля над
анимацией, чем Implicit Animations. Для использования необходимо подмешать к стейту вашего виджета
SingleTickerProviderStateMixin / TickerProviderStateMixin, создать AnimationController и зависящие от него Animation,
передать анимацию в Transition Widget (AlignTransition, DecoratedBoxTransition, SizeTransition и т.д.)
SingleTickerProviderStateMixin / TickerProviderStateMixin создает Ticker
Ticker вызывает callback на каждый фрейм анимации
AnimationController пределяет все фреймы анимации - управляет анимацией (forward, reverse, repeat, stop, reset и т.д.)
Animation отдает текущее значение анимации, а также позволяет подписаться на обновления значения/статуса анимации
Построение кадра

Некоторые внешние события приводят к необходимости обновления отображения.
Schedule Frame отправляется к Flutter Engine
Когда Flutter Engine готов приступить к обновлению рендеринга, он создает Begin Frame запрос
Этот Begin Frame запрос перехватывается Flutter Framework, который выполняет задачи, связанные в основном с Tickers (
например, анимацию)
Эти задачи могут повторно создать запрос для более поздней отрисовки (пример: анимация не закончила своё выполнение, и
для завершения ей потребуется получить еще один Begin Frame на более позднем этапе)
Далее Flutter Engine отправляет Draw Frame, который перехватывается Flutter Framework, который будет искать любые
задачи, связанные с обновлением макета с точки зрения структуры и размера
После того, как все эти задачи выполнены, он переходит к задачам, связанным с обновлением макета с точки зрения
отрисовки
Если на экране есть что-то, что нужно нарисовать, то новая сцена для визуализации отправляется в Flutter Engine, который
обновит экран
Затем Flutter Framework выполняет все задачи, которые будут выполняться после завершения рендеринга (PostFrame
callbacks), и любые другие последующие задачи, не связанные с рендерингом
…

Расчёт макета

Ограничения спускаются вниз по дереву, от родителей к детям.
Размеры идут вверх по дереву от детей к родителям.
Родители устанавливают положение детей.
BuildOwner

BuildOwner — менеджер сборки и обновления дерева элементов. Он активно участвует в двух фазах — сборки и завершения
сборки. Поскольку BuildOwner управляет процессом сборки дерева, в нем хранятся списки неактивных элементов и списки
элементов, нуждающихся в обновлении.
Методы:

scheduleBuildFor даёт возможность пометить элемент как нуждающийся в обновлении.
lockState защищает элемент от неправильного использования, утечек памяти и пометки на обновления в процессе уничтожения.
buildScope осуществляет пересборку дерева. Работает с элементами, которые помечены как нуждающиеся в обновлении.
finalizeTree завершает построение дерева. Удаляет неиспользуемые элементы и осуществляет дополнительные проверки в
режиме отладки — в том числе на дублирование глобальных ключей.
reassemble обеспечивает работу механизма HotReload. Этот механизм позволяет не пересобирать проект при изменениях, а
отправлять новую версию кода на DartVM и инициировать обновление дерева.
PipelineOwner

PipelineOwner — менеджер сборки, который занимается работой с деревом отображения.

Garbage Collector

Garbage Collector - это алгоритм, наблюдает за ссылками и очищает память с целью предотвращения её переполнения.

(!) В процессе сборки мусора слой Dart Framework создает канал взаимодействия со слоем Flutter Engine, посредством
которого узнает о моментах простоя приложения и отсутствия пользовательского взаимодействия. В эти моменты Dart
Framework запускает процесс оптимизации памяти, что позволяет сократить влияния на пользовательский опыт и стабильность
приложения.

Сборщик молодого мусора
![Garbage Collector](images/master_young_trash.png)

Используемый объём памяти можно разделить на два пространства: активное и неактивное. Новые объекты располагаются в
активной части, где по мере её заполнения, живые объекты переносятся из активной области памяти в неактивную, игнорируя
мёртвые объекты. Затем неактивная половина становится активной. Этот процесс имеет цикличный характер.

Сборщик старого мусора (Parallel Marking and Concurrent Sweeping)
![Garbage Collector](images/master_old_trash.png)

Осуществляется обход дерева объектов, используемые объекты помечаются специальной меткой.
Во время второго этапа происходит повторный проход по дереву объектов, в ходе которого непомеченные в первом этапе
объекты перерабатываются
Все метки стираются

## Тестирование

### Виды тестов

- **Модульный тест** тестирует одну функцию, метод или класс. Его цель - проверить правильность работы определенной
  функции, метода или класса. Внешние зависимости для тестируемого модуля обычно передаются как параметр.
- **Виджет тест** тестирует один виджет. Цель такого теста — убедиться, что пользовательский интерфейс виджета выглядит
  и взаимодействует, как запланировано. Тестирование виджета происходит в тестовой среде, которая обеспечивает контекст
  жизненного цикла виджета. Также тестируемый виджет должен иметь возможность получать действия и события пользователя и
  отвечать на них.
- **Интеграционный тест** тестирует все приложение или его большую часть. Цель интеграционного теста — убедиться, что
  все тестируемые виджеты и сервисы работают вместе, как ожидалось. Кроме того, вы можете использовать интеграционные
  тесты для проверки производительности вашего приложения. Как правило, интеграционный тест выполняется на реальном
  устройстве или эмуляторе.

### Что такое TDD?

**TDD** — это методика разработки приложений, где сначала пишется тест, покрывающий желаемое изменение, а затем — код,
который позволит пройти тест.

## Паттерны разработки

1. **Порождающие**. Отвечают за удобное и безопасное создание новых объектов или даже целых семейств объектов.

    - **Factory Method (Фабричный Метод)**. Порождающий паттерн проектирования, который определяет общий интерфейс для
      создания объектов в суперклассе, позволяя подклассам изменять тип создаваемых объектов.
    - **Abstract Factory (Абстрактная Фабрика)**. Порождающий паттерн проектирования, который позволяет создавать
      семейства
      связанных объектов, не привязываясь к конкретным классам создаваемых объектов.
    - **Builder (Строитель)**. Порождающий паттерн проектирования, который позволяет создавать сложные объекты пошагово.
      Строитель даёт возможность использовать один и тот же код строительства для получения разных представлений
      объектов.
    - **Prototype (Прототип)**. Порождающий паттерн проектирования, который позволяет копировать объекты, не вдаваясь в
      подробности их реализации.
    - **Singleton (Одиночка)**. Порождающий паттерн проектирования, который гарантирует, что у класса есть только один
      экземпляр, и предоставляет к нему глобальную точку доступа.

2. **Структурные**. Отвечают за построение удобных в поддержке иерархий классов.

    - **Adapter (Адаптер)**. Структурный паттерн проектирования, который позволяет объектам с несовместимыми
      интерфейсами работать вместе.
    - **Bridge (Мост)**. Структурный паттерн проектирования, который разделяет один или несколько классов на две
      отдельные иерархии — абстракцию и реализацию, позволяя изменять их независимо друг от друга.
    - **Composite (Компоновщик)**. Структурный паттерн проектирования, который позволяет сгруппировать множество
      объектов в древовидную структуру, а затем работать с ней так, как будто это единичный объект.
    - **Decorator (Декоратор)**. Структурный паттерн проектирования, который позволяет динамически добавлять объектам
      новую функциональность, оборачивая их в полезные «обёртки».
    - **Facade (Фасад)**. Структурный паттерн проектирования, который предоставляет простой интерфейс к сложной системе
      классов, библиотеке или фреймворку.
    - **Flyweight (Легковес)**. Паттерн проектирования, который позволяет вместить бóльшее количество объектов в
      отведённую оперативную память. Легковес экономит память, разделяя общее состояние объектов между собой, вместо
      хранения одинаковых данных в каждом объекте.
    - **Proxy (Заместитель)**. Структурный паттерн проектирования, который позволяет подставлять вместо реальных
      объектов специальные объекты-заменители. Эти объекты перехватывают вызовы к оригинальному объекту, позволяя
      сделать что-то до или после передачи вызова оригиналу.

3. **Поведенческие**. Решают задачи эффективного и безопасного взаимодействия между объектами программы.

    - **Chain of Responsibility (Цепочка Обязанностей)**. Поведенческий паттерн проектирования, который позволяет
      передавать запросы последовательно по цепочке обработчиков. Каждый последующий обработчик решает, может ли он
      обработать запрос сам и стоит ли передавать запрос дальше по цепи.
    - **Command (Команда)**. Поведенческий паттерн проектирования, который превращает запросы в объекты, позволяя
      передавать их как аргументы при вызове методов, ставить запросы в очередь, логировать их, а также поддерживать
      отмену операций.
    - **Iterator (Итератор)**. Поведенческий паттерн проектирования, который даёт возможность последовательно обходить
      элементы составных объектов, не раскрывая их внутреннего представления.
    - **Mediator (Посредник)**. Поведенческий паттерн проектирования, который позволяет уменьшить связанность множества
      классов между собой, благодаря перемещению этих связей в один класс-посредник.
    - **Memento (Снимок)**. Поведенческий паттерн проектирования, который позволяет сохранять и восстанавливать прошлые
      состояния объектов, не раскрывая подробностей их реализации.
    - **Observer (Наблюдатель)**. Поведенческий паттерн проектирования, который создаёт механизм подписки, позволяющий
      одним объектам следить и реагировать на события, происходящие в других объектах.
    - **State (Состояние)**. Поведенческий паттерн проектирования, который позволяет объектам менять поведение в
      зависимости от своего состояния. Извне создаётся впечатление, что изменился класс объекта.
    - **Strategy (Стратегия)**. Поведенческий паттерн проектирования, который определяет семейство схожих алгоритмов и
      помещает каждый из них в собственный класс, после чего алгоритмы можно взаимозаменять прямо во время исполнения
      программы.
    - **Template Method (Шаблонный Метод)**. Поведенческий паттерн проектирования, который определяет скелет алгоритма,
      перекладывая ответственность за некоторые его шаги на подклассы. Паттерн позволяет подклассам переопределять шаги
      алгоритма, не меняя его общей структуры.
    - **Visitor (Посетитель)**. Поведенческий паттерн проектирования, который позволяет добавлять в программу новые
      операции, не изменяя классы объектов, над которыми эти операции могут выполняться.