---
Date (Made): 2024-05-14
tags:
  - cpp
  - iostream
  - input
  - output
  - cerr
  - cin
  - cout
  - clog
Linked Docs: 
sticker: ""
---


## iostream (Input/Output Stream)
- Contains:
	- cin: controls extractions from the standard input as a byte stream.
	- cout: controls insertions to the standard output as a byte stream.
	- cerr: controls unbuffered insertions to the standard error output as a byte stream
	- clog: controls buffered insertions to the standard error output as a byte stream.
- Extra: wide stream - wchar for Unicode
	- wcerr
	- wcin
	- wclog
	- wcout

## iostream Example
```cpp
// iostream_cerr.cpp
// compile with: /EHsc
#include <iostream>
#include <fstream>

using namespace std;

void TestWide( )
{
   int i = 0;
   wcout << L"Enter a number: ";
   wcin >> i;
   wcerr << L"test for wcerr" << endl;
   wclog << L"test for wclog" << endl;
}

int main( )
{
   int i = 0;
   cout << "Enter a number: ";
   cin >> i;
   cerr << "test for cerr" << endl;
   clog << "test for clog" << endl;
   TestWide( );
}
```
- Be aware of the direction of << (out) and  >> (in).
## C++ Input/Output
```cpp
import <iostream>;
using namespace std; 
// don't need to write it like std::cout, 
// can just write cout

int main () {
	int i = 0;
	cin >> i;
	cout << i << endl;
	cout << "Hello World" << endl; 
	// endl is the newline + flushes buffer to print
	
	return 0; //optional
}

```
- std::cout << ___ << ___ << ____ ← can add data to spaces


## I/O Operators
- <<: "Put into" Output
- >> "Get from" Input
```cpp
// READ EXAMPLE 
// 1: read 
// 2: ints into variables and print the sum of both

import <iostream>;
using namepsace std;

int main () {
	int x,y;
	cin >> x >> y;
	cout << x + y << endl;
}

```
- cin property
```cpp
//default cin >> ignores whitsepace such as space, tab, \n char to find next char

// input is separated by whitespace, 
// so if the input is:   1  2

// then x takes 1 and y takes 2

// Examples:
// input:  5     10    output: 15         
// -> because cin ignores whitespace

// input:  a   b  c    output: 0          
// -> because they are strings not int

// input:  1   2  6    output: 3          
// -> because only reads first 2 ints

```

## Cin fail and eof
- How do we know if read faild?
```cpp
// READ EXAMPLE 2: stop bad input
int main () {
	int i;
	while (true) {
		cin >> i;
		if (cin.fail()) break; 
		// will be true when there is bad input
			cout << i << endl;
		}
}
// e.g. 3.1415 -> will print 3 since after that we have a decmal point which is bad input so it will break
```
- use `cin.fail()` => True if fails
- If EOF, `cin.fail()` and `cin.eof()` will be true
- NOTE: there is an implicit conversion from cin’s type (istream) to bool
    - can use cin as a condition: 
	    - true unless the stream has a read failure

## Comparison with bit shift operators
- Don’t we already have >> or << operators? 
	→ bit shift operators
- >> right bit shift operator in C/C++
	- If a,b are ints, a >> b shifts a’s bits b spots to the right
		- e.g. $21_{10}$ = $10101_2$ 21 >> 3 = $10_2$ = 2 
			→ shift 21, 3 bits to the right
- How do we know not to use bit shift with cin/cout?
	- first example of overloading: 
		- when the same function/operator has multiple implementations
	- the compiler chooses the correct implementation based on the number and type of the arguments → done at compile time

## Properties of Operator >>
-  inputs: cin (istream)
    - placeholder for data
    - returns cin back (istream)

<u>cin >> x </u>>> y >> z
Returns cin
	<u>cin >> y </u>>> z
	Returns cin
		<u>cin</u>>> z
		Returns cin


## Examples
```cpp
// READ EXAMPLE 3: getting input and printing it to the screen

int main () {
	int i;
	while (true) {
	if (! (cin >> i)) break; // if we cannot get any more input, then break
		cout << i << endl;
	}
}
```

```cpp
// READ EXAMPLE 4

int main () {
	int i;
	while (cin >> i) { // if we cannot get anymore input, then cin >> i is false
		cout << i << endl;
	}
}
```

```cpp
// READ EXAMPLE 5: read all ints, ignore non-int data

int main () {
	int i;
	while (true) { // if false, then something bad happened -> EOF, bad input
		if (! (cin >> i)) {
			if (cin.EOF()) break;
				cin.clear(); // resets stream (must be cleared before another read)
				cin.ignore(); // removes offensive character from the stream
			} else {
				cout << i << endl; // will be default printed as a decimal
			}
		}
}

// OR

int main () {
	int i;
	while (true) {
		cin >> i;
		if (cin.eof()) {
			break;
		} else if (cin.fail()) {
			cin.clear();
			cin.ignore();
		} else {
			cout << i << endl;
		}
	}
}
// e.g. 3 a b 1 2 EOF -> would loop 5 times (it reads 1 & 2 together since it 
//                       reads the longest possible value
```