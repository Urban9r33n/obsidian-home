---
Date (Made): 2024-05-22
tags: 
Linked Docs:
  - "[[Collections]]"
---

## Why use Generics?
- If you look at the API documentation for the basic array type, [`List`](https://api.dart.dev/stable/dart-core/List-class.html), [[Collections#List]], you'll see that the type is actually `List<E>`
### Advantages
- required for type safety
- Properly specifying generic types results in better generated code.
- You can use generics to reduce code duplication.

- If you intend for a list to contain only strings, you can declare it as `List<String>` (read that as "list of string"). 
- That way you, your fellow programmers, and your tools can detect that assigning a non-string to the list is probably a mistake. 
- Here's an example - FAILURE!:
```dart
//✗ static analysis: failuredart!!
var names = <String>[];
names.addAll(['Seth', 'Kathy', 'Lars']);
names.add(42); // Error
```

## Reducing code duplication with generics
- Generics let you share a single interface and implementation between many types
	- While still taking advantage of static analysis.
- Example) You create an interface for caching an object
```dart
abstract class ObjectCache {
  Object getByKey(String key);
  void setByKey(String key, Object value);
}
```
- You discover that you want a string-specific version of this interface, so you create another interface:
```dart
abstract class StringCache {
  String getByKey(String key);
  void setByKey(String key, String value);
}
```
- Later, you decide you want a number-specific version of this interface... You get the idea.

- Generic types can save you the trouble of creating all these interfaces. Instead, you can create a single interface that takes a type parameter:
```dart
abstract class Cache<T> {
  T getByKey(String key);
  void setByKey(String key, T value);
}
```


## Using Collection Literals


