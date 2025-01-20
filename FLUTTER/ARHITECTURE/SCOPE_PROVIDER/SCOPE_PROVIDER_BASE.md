## IDEA

This is a collection of how everything works under the hood to understand the logic of the Scope 
Provider's operation.


```dart
import 'package:equatable/equatable.dart';
import 'package:flutter/cupertino.dart';
import 'package:flutter_bloc/flutter_bloc.dart';
import 'package:scope_provider/scope/extension.dart';

/// BlocState is an abstract class that all states of a Bloc must extend.
/// It uses the Equatable package to ensure states can be compared
/// by value rather than by reference, which is useful in the Bloc pattern.
abstract class BlocState extends Equatable {}

/// BlocEvent is an abstract class that all events of a Bloc must extend.
/// Events in the Bloc pattern represent actions that trigger state changes.
abstract class BlocEvent {}

/// ScopeController is an abstract class that serves as a controller
/// for a Bloc (a pattern that separates business logic from UI).
/// It provides a way to create or retrieve a Bloc instance.
///
/// All controllers should extend this class.
abstract class ScopeController<BL extends Bloc<BlocEvent, BlocState>> {
  /// Abstract getter that requires subclasses to provide a way
  /// to create a Bloc instance.
  BL get createBloc;

  /// Method to retrieve a Bloc instance from the widget context.
  /// The context.read<BL>() method is used to access the provided Bloc.
  BL getBloc(BuildContext context) {
    return context.read<BL>();
  }
}

/// _ScopeBuilder is a StatelessWidget that is responsible for
/// building the Bloc and using it with the provided ScopeController.
/// It's an internal helper widget.
class _ScopeBuilder<BL extends Bloc<BlocEvent, BlocState>>
    extends StatelessWidget {
  /// The ScopeController instance responsible for creating the Bloc.
  final ScopeController<BL> controller;

  /// A builder function that constructs the widget tree using the created Bloc and controller.
  /// It provides the BuildContext, the Bloc instance, and the ScopeController to the builder.
  final Widget Function(
    BuildContext context,
    BL bloc,
    ScopeController controller,
  ) builder;

  /// Constructor that requires a controller and builder function.
  const _ScopeBuilder({
    super.key,
    required this.controller,
    required this.builder,
  });

  @override
  Widget build(BuildContext context) {
    /// Calls the createBloc getter from the controller to get the Bloc instance.
    final bloc = controller.createBloc;

    /// Passes the Bloc, controller, and context to the builder function.
    return builder(context, bloc, controller);
  }
}

/// ScopeProvider is an abstract class that acts as a base for any StatefulWidget
/// that wants to provide a ScopeController, Bloc, and listen to state changes.
///
/// It takes four generic parameters:
/// - SF: The type of StatefulWidget.
/// - BS: The type of BlocState (the state managed by the Bloc).
/// - BL: The type of Bloc that handles BlocEvent and emits BlocState.
/// - SC: The type of ScopeController that creates or manages the Bloc.
abstract class ScopeProvider<
    SF extends StatefulWidget,
    BS extends BlocState,
    BL extends Bloc<BlocEvent, BS>,
    SC extends ScopeController<BL>> extends State<SF> {
  /// Method that subclasses must implement to create their specific ScopeController.
  @protected
  SC createController();

  /// Callback method that subclasses can override to respond to Bloc state changes.
  /// This is called when the BlocListener detects a new state.
  @protected
  void onListen(
    final BuildContext context,
    final BS state,
    final SC controller,
  );

  /// Abstract method for building the widget's UI. It will be wrapped inside
  /// a BlocListener and BlocBuilder to react to state changes and rebuild the UI.
  @protected
  Widget onBuild(final BuildContext context);

  /// Static helper method that retrieves the ScopeController of type T from the widget tree.
  /// It uses the InheritedWidget pattern to locate the nearest _ScopeInherited widget,
  /// which contains the controller.
  ///
  /// If the controller is not found in the widget tree, it throws a FlutterError.
  static T of<T extends ScopeController>(BuildContext context,
      {bool listen = true}) {
    /// Retrieve the _ScopeInherited widget containing the controller.
    final _ScopeInherited<T> inherited =
        context.inhOf<_ScopeInherited<T>>(listen: listen);

    /// Return the controller casted to the expected type.
    return inherited.controller as T;
  }

  @override
  Widget build(BuildContext context) => _ScopeBuilder<BL>(
        /// Create the ScopeController using the abstract createController method.
        controller: createController(),

        /// The builder function passed to _ScopeBuilder.
        /// It provides the created Bloc and controller for use within the widget.
        builder: (context, bloc, controller) {
          /// BlocProvider provides the created Bloc to the widget tree.
          return BlocProvider<BL>(
            create: (_) => bloc,

            /// BlocBuilder rebuilds the UI when the Bloc's state changes.
            child: BlocBuilder<BL, BS>(
              builder: (context, state) {
                /// Wraps the widget with a _ScopeInherited widget, which contains
                /// the controller and the current state. This allows descendants
                /// to access the controller and react to state changes.
                return _ScopeInherited<SC>(
                  controller: controller,
                  state: state,

                  /// BlocListener listens for state changes and triggers the
                  /// onListen callback when the state changes.
                  child: BlocListener<BL, BS>(
                    listener: (context, state) => onListen(
                      context,
                      state,
                      controller as SC,
                    ),

                    /// Build the actual UI by calling the onBuild method,
                    /// which is implemented by subclasses.
                    child: onBuild(context),
                  ),
                );
              },
            ),
          );
        },
      );
}

/// _ScopeInherited is a custom InheritedWidget that holds the ScopeController
/// and the current BlocState.
///
/// This widget allows its descendants to access the controller and the current
/// state, and it decides whether to notify listeners when the state changes.
final class _ScopeInherited<T extends ScopeController> extends InheritedWidget {
  /// The ScopeController instance that controls the Bloc.
  final ScopeController controller;

  /// The current BlocState that the widget tree is reacting to.
  final BlocState state;

  /// Constructor that takes the child widget, the controller, and the state.
  const _ScopeInherited({
    required super.child,
    required this.controller,
    required this.state,
  });

  /// Determines whether to notify dependent widgets when the state changes.
  /// It compares the current state with the previous state to decide whether
  /// the widget should rebuild.
  @override
  bool updateShouldNotify(covariant _ScopeInherited oldWidget) =>
      state != oldWidget.state;
}
```