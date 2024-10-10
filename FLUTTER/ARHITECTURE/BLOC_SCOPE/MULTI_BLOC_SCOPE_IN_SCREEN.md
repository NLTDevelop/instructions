# Множество Business Logic of Component в одном экране

## Введение

Периодически возникает проблема когда в одном экране необходимо использовать несколько `BLoC` элементов. Пример такого
экрана может быть экран, который состоит из двух частей: список комментариев и детальная информация об элементе. В такой
ситуации возникает проблема как отобразить условный один `CircularProgressIndicator` для двух частей экрана, а в случае
если одна из частей загружена, а другая нет, то отобразить только для той части экрана, которая требует загрузки.

## Решение

Есть несколько типов решений этой проблемы:

1. Использовать один `BLoC` элемент для всего экрана. Но это не всегда удобно, так как в одном `BLoC` элементе
   собирается много различной логики, которая может быть разделена на несколько частей.
2. Слушать оба компонента в отельном `BLoC` элементе. Но это влечет за собой проблемы с тем, что у нас появляются лишние
   слушатели, которые могут быть не нужны.
3. Создание прослойки между слоем `отображения` и `бизнес-логики`, который будет иметь информацию о состоянии каждого
   `BLoC` элемента. Это решение является наиболее оптимальным, так как мы можем управлять состоянием каждого `BLoC` не
   вовлекая в это другие компоненты `бизнес-логики`.

Мы воспользуемся последним вариантом решения проблемы. Кроме того, данная прослойка будет отвечать в нашем случае за
взаимодействия между слоем `отображения` и `бизнес-логики`, так как мы подготовим для каждого `BLoC` элемента свой
интерфейс с необходимым набором методов, который требуется на конкретном экране.

## Реализация

Для реализации данного подхода нам потребуется следующие библиотеки:

```yaml
dependencies:
  bloc: ^8.1.4
  equatable: ^2.0.5
  flutter_bloc: ^8.1.6
```

Для работы блока мы будем использовать библиотеку `bloc`, а для удобной работы с состояниями - `equatable`.

Для начала создадим два `BLoC` элемента, которые будут отвечать за отображение списка комментариев и детальной
информации об элементе.

## Ключевые моменты реализации

Для работы нашей логики необходимо дать информацию для базового класса состояния, так как в дальнейшем мы будем получать
он них информацию о состоянии каждого `BLoC` элемента. Данная реализация возможна, как в виде `sealed class`, так и в
виде `freezed`. В нашем случае мы будем использовать `sealed class`, что позволит нам ограничить зону создания новых
классов-наследников, и даст возможность перебора всех возможных состояний при помощи `switch`. Нам необходимо создать
`get` методы для получения информации о состоянии каждого `BLoC` элемента. В случае нашего примера для нас ключевой
метод это `isProcessing` и `hasData`, который позволит нам определить, что один из `BLoC` элементов находится в
состоянии загрузки и есть ли у него данные.

```dart
sealed class NewsDetailsState extends Equatable {
  const NewsDetailsState({
    this.news,
    this.message = '',
  });

  final NewsEntity? news;
  final String message;

  const factory NewsDetailsState.processing({
    NewsEntity? news,
  }) = _NewsDetailsProcessing;

  const factory NewsDetailsState.successful({
    required NewsEntity news,
  }) = _NewsDetailsSuccessful;

  const factory NewsDetailsState.failure({
    NewsEntity? news,
  }) = _NewsDetailsFailure;

  const factory NewsDetailsState.idle({
    NewsEntity? news,
  }) = _NewsDetailsIdle;

  @override
  List<Object?> get props => [news, message];

  bool get isProcessing => switch (this) {
        _NewsDetailsProcessing() => true,
        _ => false,
      };

  bool get hasData => news != null;
}
```

Аналогичным способом нам необходимо создать состояние для списка комментариев. Как и в случае с детальной информацией,
нам необходимо создать методы для получения информации о состоянии, а если быть точнее в состоянии загрузки ли и есть ли
данные. Аналогично и с `sealed class` для списка комментариев.

```dart
part of 'news_comment_bloc.dart';

sealed class NewsCommentState extends Equatable {
  const NewsCommentState({
    this.comments = const [],
    this.message = '',
  });

  final List<CommentEntity> comments;
  final String message;

  @override
  List<Object> get props => [comments, message];

  factory NewsCommentState.processing() => const _NewsCommentProcessing();

  factory NewsCommentState.successful(comments) =>
      _NewsCommentSuccessful(comments: comments);

  factory NewsCommentState.failure() => const _NewsCommentFailure();

  factory NewsCommentState.idle() => const _NewsCommentIdle();


  bool get isProcessing => switch (this) {
        _NewsCommentProcessing() => true,
        _ => false,
      };

  bool get hasData => _currentComments.isNotEmpty;
}
```

Дальнейшая наша работа будет заключаться в создании прослойки между слоем `отображения` и `бизнес-логики`. Но прежде
создадим расширение для класса `BuildContext`. Данное расширение позволит нам получить доступ к любому `InheritedWidget`
в дереве виджетов.

```dart
import 'package:flutter/material.dart';

extension ContextExtension on BuildContext {
  T? inhMaybeOf<T extends InheritedWidget>({bool listen = true}) =>
      listen ? dependOnInheritedWidgetOfExactType<T>() : getInheritedWidgetOfExactType<T>();

  T inhOf<T extends InheritedWidget>({bool listen = true}) =>
      inhMaybeOf<T>(listen: listen) ??
      (throw ArgumentError(
        'Out of scope, not found inherited widget '
            'a $T of the exact type',
        'out_of_scope',
      ));

  T? maybeInheritFrom<A extends Object, T extends InheritedModel<A>>({
    A? aspect,
  }) =>
      InheritedModel.inheritFrom<T>(this, aspect: aspect);

  T inheritFrom<A extends Object, T extends InheritedModel<A>>({A? aspect}) =>
      maybeInheritFrom(aspect: aspect) ??
      (throw ArgumentError(
        'Out of scope, not found inherited model '
            'a $T of the exact type',
        'out_of_scope',
      ));
}
```

Теперь перейдем к созданию самого `scope-a` для наших `BLoC` элементов. Состоять он будет из следующих частей:

- Интерфейс контроллеров для блока детальной информации. В нем мы определим методы для получения информации о новости,
  состоянии загрузки и наличии данных.

```dart
abstract interface class NewsDetailsScopeController {
  NewsEntity? get news;
  bool get isDetailsProcessing;
  bool get hasDetailsData;
  void getNews(Completer? completer);
}
```

- Интерфейс контроллера для блока списка комментариев. В нем у нас будет получение списка комментариев, состояние
  загрузки и наличие данных.

```dart
abstract interface class NewsCommentsController {
    List<CommentEntity> get comments;
    bool get isCommentsProcessing;
    bool get hasCommentsData;
    void getComments(Completer? completer);
}
```

- Так же к ним будет добавлен интерфейс для общего контроллера, который будет содержать в себе методы для получение
  информации о наличии загрузки и данных в контроллерах выше.

```dart
abstract interface class NewsScopeController implements NewsDetailsScopeController, NewsCommentsController {
    bool get isProcessing;
    bool get hasData;
}
```

- Кроме того, создадим `enum` для выбора одного из контроллеров.

```dart
enum _NewsScopeAspect {details, comments}
```

- Далее идет наш `scope` в который мы будем передавать дочерние элементы. Он будет использовать `StatefulWidget`, что
  дает нам возможность управлять состоянием виджета. В виджете мы создадим два контроллера, которые нам доступ к нашим
  данным, а третий будет отвечать за работу обоих.

```dart
class NewsScope extends StatefulWidget {
    const NewsScope({
        required this.child,
        super.key,
    });

    final Widget child;

    static NewsScopeController of(
        BuildContext context, {
        bool listen = true,
    }) => context.inhOf<_InheritedNewsScope>(listen: listen).controller;
    
    @override
    State<NewsScope> createState() => _NewsScopeState();
}
```

- В классе, который отвечает за состояние виджета, мы создадим два блока, которые будут отвечать за детальную информацию
  и список комментариев и сделаем имплементацию наших контроллеров. В методе `initState` мы инициализируем наши блоки и
  запускаем загрузку данных. В методе `dispose` мы закрываем наши блоки. Далее мы реализуем методы для получения
  информации о состоянии каждого блока и передаем их в `InheritedWidget`.

```dart
class _NewsScopeState extends State<NewsScope> implements NewsScopeController {
    late final NewsDetailsBloc _newsDetailsBloc;
    late final NewsCommentBloc _newsCommentBloc;

    @override
    void initState() {
    super.initState();
        _newsDetailsBloc = NewsDetailsBloc()..add(NewsDetailsEvent.fetch());
        _newsCommentBloc = NewsCommentBloc()..add(NewsCommentEvent.fetch());
    }
    
    @override
    void dispose() {
        _newsDetailsBloc.close();
        _newsCommentBloc.close();
        super.dispose();
    }
    
    @override
    List<CommentEntity> get comments => _newsCommentBloc.state.comments;
    
    @override
    void getComments(Completer? completer) => _newsCommentBloc.add(NewsCommentEvent.fetch(completer: completer));
    
    @override
    void getNews(Completer? completer) => _newsDetailsBloc.add(NewsDetailsEvent.fetch(completer: completer));
    
    @override
    NewsEntity? get news => _newsDetailsBloc.state.news;
    
    @override
    bool get hasData => hasDetailsData && hasCommentsData;
    
    @override
    bool get hasDetailsData => _newsDetailsBloc.state.hasData;
    
    @override
    bool get hasCommentsData => _newsCommentBloc.state.hasData;
    
    @override
    bool get isProcessing => isCommentsProcessing && isDetailsProcessing && !hasData;
    
    @override
    bool get isCommentsProcessing => _newsCommentBloc.state.isProcessing;
    
    @override
    bool get isDetailsProcessing => _newsDetailsBloc.state.isProcessing;
    
    @override
    Widget build(BuildContext context) =>
        BlocBuilder<NewsDetailsBloc, NewsDetailsState>(
            bloc: _newsDetailsBloc,
            builder: (context, newsDetailsState) => BlocBuilder<NewsCommentBloc, NewsCommentState>(
                bloc: _newsCommentBloc,
                builder: (context, newsCommentState) => _InheritedNewsScope(
                    controller: this,
                    commentState: newsCommentState,
                    detailsState: newsDetailsState,
                    child: widget.child,
            ),
        ),
    );
}
```

- Далее мы создадим `InheritedWidget`, который будет содержать в себе информацию о состоянии каждого блока. В методе
  `updateShouldNotify` мы определяем, что виджет должен обновиться, если состояние одного из блоков изменилось. В методе
  `updateShouldNotifyDependent` мы определяем, что виджет должен обновиться, если изменилось состояние конкретного
  блока.

```dart
class _InheritedNewsScope extends InheritedModel<_NewsScopeAspect> {
    const _InheritedNewsScope({
        required this.controller,
        required this.detailsState,
        required this.commentState,
        required super.child,
    });

    final NewsScopeController controller;
    final NewsDetailsState detailsState;
    final NewsCommentState commentState;

    @override
    bool updateShouldNotify(_InheritedNewsScope oldWidget) => 
        detailsState != oldWidget.detailsState ||
        commentState != oldWidget.commentState;
    
    @override
    bool updateShouldNotifyDependent(
        covariant _InheritedNewsScope oldWidget,
        Set<_NewsScopeAspect> dependencies,
    ) {
        var shouldNotify = false;
    
        if (dependencies.contains(_NewsScopeAspect.comments)) {
          shouldNotify = shouldNotify || commentState.comments != oldWidget.commentState.comments;
        }
        if (dependencies.contains(_NewsScopeAspect.details)) {
          shouldNotify = shouldNotify || detailsState.news != oldWidget.detailsState.news;
        }
        return shouldNotify;
    }
}
```

- Внедряется данный `scope` в дерево виджетов мы можем следующим образом:

```dart
const NewsScope(child: NewsScreen()),
```

- Теперь у нас в `NewsScreen` доступ к нашему `scope` и мы можем получить информацию о состоянии каждого блока и в том
  числе загружаются ли они и есть ли данные, как в целостности, так и по отдельности.

```dart
import 'dart:async';

import 'package:flutter/material.dart';
import 'package:multi_bloc_scope/feature/news/widget/news_scope.dart';

class NewsScreen extends StatelessWidget {
  const NewsScreen({super.key});

  @override
  Widget build(BuildContext context) {
    final newsScope = NewsScope.of(context);
    return Scaffold(
      body: newsScope.isProcessing
          ? const Center(
              child: CircularProgressIndicator(),
            )
          : RefreshIndicator(
              onRefresh: () async {
                final newsCompleter = Completer();
                final commentsCompleter = Completer();
                newsScope.getNews(newsCompleter);
                newsScope.getComments(commentsCompleter);
                await Future.wait(
                    [newsCompleter.future, commentsCompleter.future]);
              },
              child: CustomScrollView(
                slivers: <Widget>[
                  const SliverAppBar(
                    title: Text('News'),
                  ),
                  if (newsScope.isDetailsProcessing && !newsScope.hasData)
                    const SliverToBoxAdapter(
                      child: Center(child: CircularProgressIndicator()),
                    ),
                  if (newsScope.isCommentsProcessing &&
                      !newsScope.hasCommentsData)
                    const SliverToBoxAdapter(
                      child: Center(child: CircularProgressIndicator()),
                    ),
                ],
              ),
            ),
    );
  }
}

```

## Источники

- [Flutter BLoC](https://bloclibrary.dev)
- [Business Logic Component](https://plugfox.dev/business-logic-component-3/)
- [Sizzle Starter](https://sizzle.lazebny.io)