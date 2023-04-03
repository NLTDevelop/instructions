# React Native Folder Structure

When starting a new React Native project, one of the first things you should do is establish a folder structure that will help organize your code and assets. Having a well-organized folder structure can help you and your team maintain the code and make it more readable and reusable. In this section, we'll look at a suggested folder structure for your React Native project.


- `assets`
- `src`
    - `entities`
    - `hooks`
    - `libs`
    - `modules`
        - `module1`
            - `presenter`
            - `ui`
        - `module2`
            - `presenter`
            - `ui`
            - `useCases`
        - ...
    - `navigation`
        - `rootNavigator`
        - `stackNavigator`
        - `tabNavigator`
    - `UIKit`
    - `UIProvider`
    - `utils`
    - `App.tsx`
- `index.js`


In conclusion, establishing a well-organized folder structure is an important part of setting up a new React Native project. By following the suggested folder structure outlined above, you can keep your code and assets organized, make your code more readable and reusable, and make it easier for other developers to understand and contribute to your project. Having separate folders for assets, source code, business data models, reusable hooks, third-party library implementations, modules, navigation, reusable components, UI context, and utility functions can help keep your codebase manageable and maintainable.

## assets

The `assets` folder is where you will keep all of your static assets, such as images, fonts, and other media files. Having a separate folder for assets can help you quickly find the files you need and keep your code organized.

## src

The `src` folder is where you will keep all of your source code. Inside the `src` folder, you can create additional folders for different parts of your application. For example, you might create a `modules (screens)` folder for all of your application screens, a `UIKit (components)` folder for reusable components, and a `entities (repository)` folder for your data access layer. Avoid putting all of your code in one folder, as it can quickly become disorganized and difficult to maintain.

## entities (repository)

The `entities (repository)` folder is an important part of your project where you can keep all of your business data models. This is where you would store all of your models, reducers, entity interface and any other data-related files. By having all of your data-related files in one folder, you can easily find and modify data-related code. This can be especially useful when you have a large project with many files and you need to keep everything organized. Additionally, having a clear and organized file structure can make it easier for other developers to understand your code and contribute to your project if needed. 

## hooks

The `hooks` folder is where you will keep all of your reusable hooks. These are hooks that you will use across multiple components in your application. Each hook should have its own file.

## libs

The `libs` folder is where you will keep all of your implementation of third party libraries. For example, you might create a `requestor` folder for `axios` or other network request libraries, a `storage` folder for `AsyncStorage` or other storage-related libraries, and so on. Keeping all of your third-party library implementation files in one folder can help you quickly find and modify the code related to a specific library.

## modules

The `modules` folder is where we keep all the different modules of our app, such as authentication flow containing (authorization, registration, and password restoration screens), profile, settings, etc. Each module should have its own folder, containing two subfolders: `ui` and `presenter` and sometimes `useCases`.

The `ui` folder is where we keep all of the screens and UI components which use only this module.

The `presenter` folder is where we keep the presentation logic for each screen. This can include state management and calling business logic from `useCases`. 

The `useCases` folder can also be included in this folder for additional business logic.

## navigation

The `navigation` folder is where you will keep `rootNavigator` and other navigators which we are using in our projects like stack or tab navigator

## UIKit (components)

The `UIKit (components)` folder is where you will keep all of your reusable components. These are components that you will use across multiple screens in your application. Each component should have its own folder, with the component file, any related stylesheets.

## UIProvider

The `UIProvider` folder is where we keep all the context related to UI. This can include context for localisation and color scheme.

## utils

The `utils` folder is where you will keep all of your utility functions. These are functions that you will use across multiple parts of your application.


In conclusion, establishing a well-organized folder structure is an important part of setting up a new React Native project. By following the suggested folder structure outlined above, you can keep your code and assets organized, make your code more readable and reusable, and make it easier for other developers to understand and contribute to your project. Having separate folders for assets, source code, business data models, reusable hooks, third-party library implementations, modules, navigation, reusable components, UI context, and utility functions can help keep your codebase manageable and maintainable.