## Using Libraries
```dart
import 'dart:html';
import 'package:test/test.dart';
```

## Specifying a library prefix
```dart
import 'package:lib1/lib1.dart';
import 'package:lib2/lib2.dart' as lib2;

// Uses Element from lib1.
Element element1 = Element();

// Uses Element from lib2.
lib2.Element element2 = lib2.Element();
```

## Importing only part of a library
```dart
// Import only foo.
import 'package:lib1/lib1.dart' show foo;

// Import all names EXCEPT foo.
import 'package:lib2/lib2.dart' hide foo;
```

## Lazily loading a library
_Deferred loading_ (also called _lazy loading_) allows a web app to load a library on demand, if and when the library is needed. Use deferred loading when you want to meet one or more of the following needs.

- Reduce a web app's initial startup time.
- Perform A/B testing—trying out alternative implementations of an algorithm, for example.
- Load rarely used functionality, such as optional screens and dialogs.

That doesn't mean Dart loads all the deferred components at start time. The web app can download deferred components via the web when needed.

The `dart` tool doesn't support deferred loading for targets other than web. If you're building a Flutter app, consult its implementation of deferred loading in the Flutter guide on [deferred components](https://docs.flutter.dev/perf/deferred-components).

To lazily load a library, first import it using `deferred as`.

```dart
import 'package:greetings/hello.dart' deferred as hello;

//When you need the library, invoke `loadLibrary()` using the library's identifier.

Future<void> greet() async {
  await hello.loadLibrary();
  hello.printGreeting();
}
```

## Implementing Libraries
See [Create Packages](https://dart.dev/guides/libraries/create-packages) for advice on how to implement a package, including:

- How to organize library source code.
- How to use the `export` directive.
- When to use the `part` directive.
- How to use conditional imports and exports to implement a library that supports multiple platforms.