## List
- Ordered group of objects
### List examples
```dart
var list = [1, 2, 3];
```

```dart
var list = [
	'Car',
	'Boat',
	'Plane', //trailing comma doesn't affect, help copy-paste errors
	];
```
### Accessing the value of list
```dart
var list = [1 ,2, 3];
assert(list.length == 3);
assert(list[1] == 2);

list[1] = 1;
assert(list[1] == 1);
```

### Compile-time constant
```dart
var constantList = const [1, 2, 3];
//constantList[1] = 1; This will cause an error
```


## Sets
- <u>Unordered</u> collection of <u>unique</u> items
```dart
var halogens = {'fluorine', 'chlorine', 'bromine', 'iodine', 'astatine'};
```
### Creating Empty sets
```dart
var names = <String>{};
// Set<String> names = {}; // This works, too.
// var names = {}; // Creates a map, not a set.
```
### Add, Remove, Length, Const
```dart
var elements = <String>{};
elements.add('fluorine');
elements.addAll(halogens);

var elements = <String>{};
elements.add('fluorine');
elements.addAll(halogens);
elements.remove('fluorine');
assert(elements.length == 5);

final constantSet = const {
  'fluorine',
  'chlorine',
  'bromine',
  'iodine',
  'astatine',
};
// constantSet.add('helium'); // This line will cause an error.
```

## Maps
- A map is an object that associates keys and values
```dart
var gifts = {
  // Key:    Value
  'first': 'partridge',
  'second': 'turtledoves',
  'fifth': 'golden rings'
};

var nobleGases = {
  2: 'helium',
  10: 'neon',
  18: 'argon',
};
```
### Using map constructor
```dart
var gifts = Map<String, String>();
gifts['first'] = 'partridge';
gifts['second'] = 'turtledoves';
gifts['fifth'] = 'golden rings';

var nobleGases = Map<int, String>();
nobleGases[2] = 'helium';
nobleGases[10] = 'neon';
nobleGases[18] = 'argon';

```
### Using Assignment operator ([]=)
```dart
var gifts = {'first': 'partridge'};
gifts['fourth'] = 'calling birds'; // Add a key-value pair
```
### Using Subscript Operator ([])
```dart
var gifts = {'first': 'partridge'};
assert(gifts['first'] == 'partridge');

```
### Getting Null in return (doesn't exist in the map)
```dart
var gifts = {'first': 'partridge'};
assert(gifts['fifth'] == null);
```
### Length
```dart
var gifts = {'first': 'partridge'};
gifts['fourth'] = 'calling birds';
assert(gifts.length == 2);
```
### Constant
```dart
final constantMap = const {
  2: 'helium',
  10: 'neon',
  18: 'argon',
};

// constantMap[2] = 'Helium'; // This line will cause an error.
```

## Set or Map?
> The syntax for map literals is similar to that for set literals. Because map literals came first, `{}` defaults to the `Map` type. If you forget the type annotation on `{}` or the variable it's assigned to, then Dart creates an object of type `Map<dynamic, dynamic>`.

## Operators
### Spread Operators
- Dart supports the **spread operator** (`...`) and the **null-aware spread operator** (`...?`) in list, map, and set literals.
```dart
var list = [1, 2, 3];
var list2 = [0, ...list];
assert(list2.length == 4);
```
If the expression to the right of the spread operator might be null, you can avoid exceptions by using a null-aware spread operator (`...?`):
```dart
var list2 = [0, ...?list];
assert(list2.length == 1);
```
### Control-flow Operators
- Dart offers **collection if** and **collection for** for use in list, map, and set literals. 
- You can use these operators to build collections using conditionals (`if`) and repetition (`for`).
#### Collection if
```dart
var nav = ['Home', 'Furniture', 'Plants', if (promoActive) 'Outlet'];
```
#### if-case inside collection literals
```dart
var nav = ['Home', 'Furniture', 'Plants', if (login case 'Manager') 'Inventory'];
```
#### Collection for
```dart
var listOfInts = [1, 2, 3];
var listOfStrings = ['#0', for (var i in listOfInts) '#$i'];
assert(listOfStrings[1] == '#1');
```