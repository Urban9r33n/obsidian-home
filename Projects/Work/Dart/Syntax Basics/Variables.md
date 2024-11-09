---
Date (Made): 2024-05-19
tags:
  - Dart
  - variable
  - types
Linked Docs:
  - "[[Types]]"
---
## Type Inference example
```dart
var name = 'Bob';
```

## Explicit Type Declaration
```dart
String name = 'Bob';
```

## Object and Dynamic Types
- Sometimes, you might want a variable to hold values of different types. 
	- In such cases, you can use the `Object` type or the `dynamic` type.
	
```dart
Object name = 'Bob';
```
- **Object**: This is the root of all Dart objects. 
	- Any Dart object can be assigned to a variable of type `Object`, but you won't have access to type-specific methods directly without casting.
```dart
dynamic name = "Bob";
```
- **dynamic**: This type indicates that the variable can hold any type of value and allows dynamic typing, which means the type is determined at runtime.
	-  However, this sacrifices type safety.

## Null Safety
```dart
String? name  
// Nullable type. Can be `null` or string.

String name   
// Non-nullable type. Cannot be `null` but can be string.

```
1. When you specify a type for a variable, parameter, or another relevant component, you can control whether the type allows `null`. To enable nullability, you add a `?` to the end of the type declaration.
2. You must initialize variables before using them. Nullable variables default to `null`, so they are initialized by default. Dart doesn't set initial values to non-nullable types. It forces you to set an initial value. Dart doesn't allow you to observe an uninitialized variable. This prevents you from accessing properties or calling methods where the receiver's type can be `null` but `null` doesn't support the method or property used.
3. You can't access properties or call methods on an expression with a nullable type. The same exception applies where it's a property or method that `null` supports like `hashCode` or `toString()`.

## Default Value
### Nullable Variable
- Uninitialized variables that have a nullable type have an initial value of `null`. 
- Even variables with numeric types are initially null, because numbers—like everything else in Dart—are objects.
```dart
int? lineCount;
assert(lineCount == null);
```
### Null Safety Variable
- With null safety, you must initialize the values of non-nullable variables before you use them:
```dart
int lineCount = 0;
```

### Local Variable
- You don't have to initialize a local variable where it's declared, but you do need to assign it a value before it's used. 
- For example, the following code is valid because Dart can detect that `lineCount` is non-null by the time it's passed to `print()`:
```dart
int lineCount;

if (weLikeToCount) {
  lineCount = countLines();
} else {
  lineCount = 0;
}

print(lineCount);
```

## Late Variables
### Two Cases of using `late`
1. Declaring a non-nullable variable that's initialized after its declaration.
2. Lazily initializing a variable.

If you're sure that a variable is set before it's used, but Dart disagrees, you can fix the error by marking the variable as `late`:
```dart
late String description;

void main() {
  description = 'Feijoada!';
  print(description);
}
```

This lazy initialization is handy in a couple of cases:

- The variable might not be needed, and initializing it is costly.
- You're initializing an instance variable, and its initializer needs access to `this`.
```dart
// This is the program's only call to readThermometer().
late String temperature = readThermometer(); // Lazily initialized.
```
- In the example, if the `temperature` variable is never used, then the expensive `readThermometer()` function is never called:

## Final and const
### Final
```dart
final name = 'Bob'; // Without a type annotation
final String nickname = 'Bobby';
```
- You can't change the value of a `final` variable:
```dart
//static analysis: failure

name = 'Alice'; // Error: a final variable can only be set once.
```
### Const
```dart
const bar = 1000000; // Unit of pressure (dynes/cm2)
const double atm = 1.01325 * bar; // Standard atmosphere
```
- The `const` keyword isn't just for declaring constant variables. 
	- You can also use it to create constant _values_, as well as to declare constructors that _create_ constant values. 
	- Any variable can have a constant value.
```dart
var foo = const [];
final bar = const [];
const baz = []; // Equivalent to `const []`
```

- You can change the value of a non-final, non-const variable, even if it used to have a `const` value:
```dart
foo = [1, 2, 3]; // Was const []
```

- You can't change the value of a `const` variable:
```dart
// static analysis: failure

baz = [42]; // Error: Constant variables can't be assigned a value.
```

- You can define constants that use `type checks and casts` (is and as), `collection if`, and `spread operators` (... and ...?):
```dart
const Object i = 3; // Where i is a const Object with an int value...
const list = [i as int]; // Use a typecast.
const map = {if (i is int) i: 'int'}; // Use is and collection if.
const set = {if (list is List<int>) ...list}; // ...and a spread.
```
