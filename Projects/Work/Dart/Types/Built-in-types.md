## Types lists
- [Numbers](https://dart.dev/language/built-in-types#numbers) (`int`, `double`)
- [Strings](https://dart.dev/language/built-in-types#strings) (`String`)
- [Booleans](https://dart.dev/language/built-in-types#booleans) (`bool`)
- [Records](https://dart.dev/language/records) (`(value1, value2)`)
- [Lists](https://dart.dev/language/collections#lists) (`List`, also known as _arrays_)
- [Sets](https://dart.dev/language/collections#sets) (`Set`)
- [Maps](https://dart.dev/language/collections#maps) (`Map`)
- [Runes](https://dart.dev/language/built-in-types#runes-and-grapheme-clusters) (`Runes`; often replaced by the `characters` API)
- [Symbols](https://dart.dev/language/built-in-types#symbols) (`Symbol`)
- The value `null` (`Null`)

## Types with special roles
- `Object`: The superclass of all Dart classes except `Null`.
- `Enum`: The superclass of all enums.
- `Future` and `Stream`: Used in [asynchrony support](https://dart.dev/language/async).
- `Iterable`: Used in [for-in loops](https://dart.dev/libraries/dart-core#iteration) and in synchronous [generator functions](https://dart.dev/language/functions#generators).
- `Never`: Indicates that an expression can never successfully finish evaluating. Most often used for functions that always throw an exception.
- `dynamic`: Indicates that you want to disable static checking. Usually you should use `Object` or `Object?` instead.
- `void`: Indicates that a value is never usedㅋ. Often used as a return type.

## How to turn a string into a number, or vice versa
```dart
// String -> int
var one = int.parse('1');
assert(one == 1);

// String -> double
var onePointOne = double.parse('1.1');
assert(onePointOne == 1.1);

// int -> String
String oneAsString = 1.toString();
assert(oneAsString == '1');

// double -> String
String piAsString = 3.14159.toStringAsFixed(2);
assert(piAsString == '3.14');
```