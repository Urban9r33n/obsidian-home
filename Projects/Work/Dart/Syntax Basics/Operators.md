## Operators

| Description                                                               | Operator                                                                                        | Associativity |
| ------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------- | ------------- |
| unary postfix                                                             | _`expr`_`++`    _`expr`_`--`    `()`    `[]`    `?[]`    `.`    `?.`    `!`                     | None          |
| unary prefix                                                              | `-`_`expr`_    `!`_`expr`_    `~`_`expr`_    `++`_`expr`_    `--`_`expr`_      `await` _`expr`_ | None          |
| multiplicative                                                            | `*`    `/`    `%`  `~/`                                                                         | Left          |
| additive                                                                  | `+`    `-`                                                                                      | Left          |
| shift                                                                     | `<<`    `>>`    `>>>`                                                                           | Left          |
| bitwise AND                                                               | `&`                                                                                             | Left          |
| bitwise XOR                                                               | `^`                                                                                             | Left          |
| bitwise OR                                                                | `\|`                                                                                            | Left          |
| relational and type test                                                  | `>=`    `>`    `<=`    `<`    `as`    `is`    `is!`                                             | None          |
| equality                                                                  | `\==`    `!=`                                                                                   | None          |
| logical AND                                                               | `&&`                                                                                            | Left          |
| logical OR                                                                | `\|`                                                                                            | Left          |
| if-null                                                                   | `??`                                                                                            | Left          |
| conditional                                                               | _`expr1`_    `?`    _`expr2`_    `:`    _`expr3`_                                               | Right         |
| cascade                                                                   | `..`    `?..`                                                                                   | Left          |
| assignment                                                                | `=`    `*=`    `/=`   `+=`   `-=`   `&=`   `^=`   _etc._                                        | Right         |
| spread ([See note](https://dart.dev/language/operators#spread-operators)) | `...`    `...?`                                                                                 | None          |

### Examples
```dart
a++
a + b
a = b
a == b
c ? a : b
a is T
```

### Operator Precedence Example
```dart
// Parentheses improve readability.
if ((n % i == 0) && (d % i == 0)) ...

// Harder to read, but equivalent.
if (n % i == 0 && d % i == 0) ...

```

## Arithmetic Operators
| Operator    | Meaning                                                                  |
| ----------- | ------------------------------------------------------------------------ |
| `+`         | Add                                                                      |
| `-`         | Subtract                                                                 |
| `-`_`expr`_ | Unary minus, also known as negation (reverse the sign of the expression) |
| `*`         | Multiply                                                                 |
| `/`         | Divide                                                                   |
| `~/`        | Divide, returning an integer result                                      |
| `%`         | Get the remainder of an integer division (modulo)                        |
### Examples
```dart
assert(2 + 3 == 5);
assert(2 - 3 == -1);
assert(2 * 3 == 6);
assert(5 / 2 == 2.5); // Result is a double
assert(5 ~/ 2 == 2); // Result is an int
assert(5 % 2 == 1); // Remainder

assert('5/2 = ${5 ~/ 2} r ${5 % 2}' == '5/2 = 2 r 1');
```

## Prefix and Postfix inc,dec operators
|Operator|Meaning|
|---|---|
|`++`_`var`_|_`var`_  `=`  _`var`_ `+ 1` (expression value is _`var`_ `+ 1`)|
|_`var`_`++`|_`var`_  `=`  _`var`_ `+ 1` (expression value is _`var`_)|
|`--`_`var`_|_`var`_  `=`  _`var`_ `- 1` (expression value is _`var`_ `- 1`)|
|_`var`_`--`|_`var`_  `=`  _`var`_ `- 1` (expression value is _`var`_)|
### Examples
```dart
int a;
int b;

a = 0;
b = ++a; // Increment a before b gets its value.
assert(a == b); // 1 == 1

a = 0;
b = a++; // Increment a after b gets its value.
assert(a != b); // 1 != 0

a = 0;
b = --a; // Decrement a before b gets its value.
assert(a == b); // -1 == -1

a = 0;
b = a--; // Decrement a after b gets its value.
assert(a != b); // -1 != 0
```

## Equality and relational operators
| Operator | Meaning                     |
| -------- | --------------------------- |
| `\==`    | Equal; see discussion below |
| `!=`     | Not equal                   |
| `>`      | Greater than                |
| `<`      | Less than                   |
| `>=`     | Greater than or equal to    |
| `<=`     | Less than or equal to       |

```dart 
assert(2 == 2);
assert(2 != 3);
assert(3 > 2);
assert(2 < 3);
assert(3 >= 3);
assert(2 <= 3);
```

## Type test operators
|Operator|Meaning|
|---|---|
|`as`|Typecast (also used to specify [library prefixes](https://dart.dev/language/libraries#specifying-a-library-prefix))|
|`is`|True if the object has the specified type|
|`is!`|True if the object doesn't have the specified type|
### Example
```dart
(employee as Person).firstName = 'Bob';

if (employee is Person) {
  // Type check
  employee.firstName = 'Bob';
}

```

## Assignment Operators
```dart
// Assign value to a
a = value;
// Assign value to b if b is null; otherwise, b stays the same
b ??= value;
```

### Compound assignment operators 
`\=`|`*=`|`%=`|`>>>=`|`^=`|
|`+=`|`/=`|`<<=`|`&=`|`\|=`|
|`-=`|`~/=`|`>>=`|

|   |   |   |
|---|---|---|
|**For an operator _op_:**|`a` _`op`_`= b`|`a = a` _`op`_ `b`|
|**Example:**|`a += b`|`a = a + b`|

```dart
var a = 2; // Assign using =
a *= 3; // Assign and multiply: a = a * 3
assert(a == 6);
```

## Logical Operators
|Operator|Meaning|
|---|---|
|`!`_`expr`_|inverts the following expression (changes false to true, and vice versa)|
|`\|`|logical OR|
|`&&`|logical AND|
### Examples
```dart
if (!done && (col == 0 || col == 3)) {
  // ...Do something...
}
```


## Bitwise and Shift Operators
|Operator|Meaning|
|---|---|
|`&`|AND|
|`\|`|OR|
|`^`|XOR|
|`~`_`expr`_|Unary bitwise complement (0s become 1s; 1s become 0s)|
|`<<`|Shift left|
|`>>`|Shift right|
|`>>>`|Unsigned shift right|
### Examples
```dart
final value = 0x22;
final bitmask = 0x0f;

assert((value & bitmask) == 0x02); // AND
assert((value & ~bitmask) == 0x20); // AND NOT
assert((value | bitmask) == 0x2f); // OR
assert((value ^ bitmask) == 0x2d); // XOR

assert((value << 4) == 0x220); // Shift left
assert((value >> 4) == 0x02); // Shift right

// Shift right example that results in different behavior on web
// because the operand value changes when masked to 32 bits:
assert((-value >> 4) == -0x03);

assert((value >>> 4) == 0x02); // Unsigned shift right
assert((-value >>> 4) > 0); // Unsigned shift right
```

## Conditional Expressions
_`condition`_ `?` _`expr1`_ `:` _`expr2`_

If _condition_ is true, evaluates _expr1_ (and returns its value); otherwise, evaluates and returns the value of _expr2_.

_`expr1`_ `??` _`expr2`_

If _expr1_ is non-null, returns its value; otherwise, evaluates and returns the value of _expr2_.

### Examples
```dart
var visibility = isPublic ? 'public' : 'private';

String playerName(String? name) => name ?? 'Guest';

// Slightly longer version uses ?: operator.
String playerName(String? name) => name != null ? name : 'Guest';

// Very long version uses if-else statement.
String playerName(String? name) {
  if (name != null) {
    return name;
  } else {
    return 'Guest';
  }
}

```

## Cascade Notation
Cascades (`..`, `?..`) allow you to make a sequence of operations on the same object. In addition to accessing instance members, you can also call instance methods on that same object. This often saves you the step of creating a temporary variable and allows you to write more fluid code.
```dart
var paint = Paint()
  ..color = Colors.black
  ..strokeCap = StrokeCap.round
  ..strokeWidth = 5.0;
```

### Example
The constructor, `Paint()`, returns a `Paint` object. The code that follows the cascade notation operates on this object, ignoring any values that might be returned.

The previous example is equivalent to this code:
```dart
var paint = Paint();
paint.color = Colors.black;
paint.strokeCap = StrokeCap.round;
paint.strokeWidth = 5.0;

```
If the object that the cascade operates on can be null, then use a _null-shorting_ cascade (`?..`) for the first operation. Starting with `?..` guarantees that none of the cascade operations are attempted on that null object.
```dart
querySelector('#confirm') // Get an object.
  ?..text = 'Confirm' // Use its members.
  ..classes.add('important')
  ..onClick.listen((e) => window.alert('Confirmed!'))
  ..scrollIntoView();
```
This is equivalent to the following:
```dart
var button = querySelector('#confirm');
button?.text = 'Confirm';
button?.classes.add('important');
button?.onClick.listen((e) => window.alert('Confirmed!'));
button?.scrollIntoView();
```

### Nesting Cascades Example
```dart
final addressBook = (AddressBookBuilder()
      ..name = 'jenny'
      ..email = 'jenny@example.com'
      ..phone = (PhoneNumberBuilder()
            ..number = '415-555-0100'
            ..label = 'home')
          .build())
    .build();
```
However This fails:
```dart
var sb = StringBuffer();
sb.write('foo')
  ..write('bar'); // Error: method 'write' isn't defined for 'void'.
```


## Spread Operations
Spread operators evaluate an expression that yields a collection, unpacks the resulting values, and inserts them into another collection.

**The spread operator isn't actually an operator expression**. The `...`/`...?` syntax is part of the collection literal itself. So, you can learn more about spread operators on the [Collections](https://dart.dev/language/collections#spread-operators) page.

Because it isn't an operator, the syntax doesn't have any "[operator precedence](https://dart.dev/language/operators#operators)". Effectively, it has the lowest "precedence" — any kind of expression is valid as the spread target, such as:

```dart
[...a + b]
```


## Other Operators
|Operator|Name|Meaning|
|---|---|---|
|`()`|Function application|Represents a function call|
|`[]`|Subscript access|Represents a call to the overridable `[]` operator; example: `fooList[1]` passes the int `1` to `fooList` to access the element at index `1`|
|`?[]`|Conditional subscript access|Like `[]`, but the leftmost operand can be null; example: `fooList?[1]` passes the int `1` to `fooList` to access the element at index `1` unless `fooList` is null (in which case the expression evaluates to null)|
|`.`|Member access|Refers to a property of an expression; example: `foo.bar` selects property `bar` from expression `foo`|
|`?.`|Conditional member access|Like `.`, but the leftmost operand can be null; example: `foo?.bar` selects property `bar` from expression `foo` unless `foo` is null (in which case the value of `foo?.bar` is null)|
|`!`|Non-null assertion operator|Casts an expression to its underlying non-nullable type, throwing a runtime exception if the cast fails; example: `foo!.bar` asserts `foo` is non-null and selects the property `bar`, unless `foo` is null in which case a runtime exception is thrown|