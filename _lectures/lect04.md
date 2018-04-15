---
num: "Lecture 4"
desc: "Dynamic Array Allocation, Structs, Padding, and Namespaces"
ready: true
date: 2018-04-12 12:30:00.00-7:00
---
 
# Dynamically Allocating Arrays

* Statically allocating an array needs to know the array size DURING compilation…. USUALLY.
* In many cases, we may not know what the size of an array needs to be until runtime.
* Arrays should be dynamically allocated on the heap.
* Some compilers may offer extensions and behave differently.

## Example
```
int x;
cout << “Enter a positive number: “;
cin >> x;
// int intArray[x]; // ERROR IN VisualStudio, NOT g++ / clang++
int* intArray = new int[x]; // LEGAL IN BOTH
for (int i = 0; i < x; i++) {
	intArray[i] = i;
	cout << intArray[i] << endl;
}
// Note: to delete an array on the heap, use delete [] intArray;
```
# Structs
* Even in C, there was a way to represent complex data types called a “Structure” or struct
* A struct brings together a set of heterogeneous members, similar to a class.
* Structs consist of zero or more members of various types.
	* In C, having a struct without any members is illegal, but in C++ it’s fine.
	* The sizeof an empty struct is 1 byte. Why?
		* Because it ensures two different objects will have different addresses when dealing with pointer arithmetic
	* <b>Note:</b> No difference between class / struct except struct defaults variables to public and classes default to private
	* Once a struct is defined, you can declare variables, use them as return types, pass them in parameters, assign them to another struct of the same type… basically treat them like any type!

# Memory Organization of classes / structs
* Strictly typed languages enable the compiler to allocate the appropriate memory for functions and types before runtime.
* In memory, the members are stored sequentially and space is allocated to it based on the type.
* Therefore, the size of the struct seems like it should be the summation of sizes for all of its members… but not exactly.

## Padding
* The concept of leaving <b>blank space</b> when allocating memory in order to improve access speeds for data.
* Behavior is compiler / system dependent. In most cases (such as g++) 4 bytes are fetched every read operation.
* Compilers optimize speed by <b>cramming</b> in as many types as possible into 4 byte "words" starting in order.
* Time vs. space tradeoff.

## Example
```
class X {
	int a;
	short b;
	char c;
	char d;
};
```
![Padding X](PaddingX.png)

```
class Y {
	char a;
	int b;
	char c;
	short d;
};
```
![Padding Y](PaddingY.png)

```
int main() {
	X x;
	Y y;
	cout << "size x " << sizeof(x) << endl; // 8 bytes
	cout << "size y " << sizeof(y) << endl; // 12 bytes???
	return 0;
}
```


# Namespaces
* The purpose of a namespace is to avoid <b>naming collisions</b>.

A high-level scenario:
* std::string is a class in the standard library
* We've seen how we can specify the this by using `std::string` or `using namespace std`.
* But what if we are writing a sewing simulator and we want to write our own class called `string` that represents an actual string with a length.
* The C++ compiler might be confused if we don't specify between our string implementation and the standard library's string implementation.

## Example
```
// F1.h
#ifndef F1_H
#define F1_H
#include <iostream>
namespace CS_32_F1 {
	void someFunction() {
		std::cout << "F1.someFunction()" << std::endl;
	}
}
#endif
------------
// F2.h
#ifndef F2_H
#define F2_H
#include <iostream>
namespace CS_32_F2 {
	void someFunction() {
		std::cout << "F2.someFunction()" << std::endl;
	}
}
#endif
------------
#include "F1.h"
#include "F2.h"
int main() {
	using namespace CS_32_F1;
	someFunction(); // F1.someFunction()
	return 0;
}
-----
# Makefile
CXX=g++

# note F1.h and F2.h are not required, but can list them
# to make sure the files exist.
main: main.o F1.h F2.h
	${CXX} -o main -std=C++11 main.o
clean:
	rm -f *.o main
```
<b>Notes:</b>
* using namespace CS_32_F1 prints “F1.someFunction()”
* using namespace CS_32_F2 prints “F2.someFunction()”
* using namespace CS_32_F1; using namespace CS_32_F2;
// ERROR - naming collision!
* using CS_32_F1::someFunction prints “F1.someFunction()”
* using CS_32_F2::someFunction prints “F2.someFunction()”

## Global Namespace
* By default, all variables and functions are defined in a global namespace if no namespace is explicitly defined.

## Appending to existing namespaces
* Namespace definitions can span multiple files (it adds on to the namespace if it already exists).
* Imagine if the standard library had to be defined in a single namespace block!!

## Example - Namespaces spanning multiple files
```
// F1.h
#ifndef F1_H
#define F1_H
#include <iostream>

namespace CS_32_F1 {
	class string {
	public:
		void someFunction();
	};
}
#endif
------------
// F2.h
#ifndef F2_H
#define F2_H
#include <iostream>

namespace CS_32_F2 {
	class string {
	public:
		void someFunction();
	};
}
#endif
------------
// F1.cpp
#include <iostream>
#include "F1.h"

using namespace std;

namespace CS_32_F1 {
	void string::someFunction() {
		cout << "F1.someFunction()" << endl;
	}
}
------------
// F2.cpp
#include <iostream>
#include "F2.h"

using namespace std;

namespace CS_32_F2 {
	void string::someFunction() {
		cout << "F2.someFunction()" << endl;
	}
}
------------
// main.cpp
#include "F1.h"
#include "F2.h"
int main() {
	CS_32_F2::string x;
	x.someFunction(); // prints “F2.someFunction()”
	return 0;
}-------------------------
# Makefile

#CXX=g++

main: main.o Person.o F1.o F2.o
	${CXX} -o main -std=C++11 main.o Person.o F1.o F2.o

clean:
	rm -f *.o main
```
## Specifying something in the global namespace.
* It’s possible that local definitions have namespace conflicts if using namespace … has a naming conflict.
* You can specify the global namespace by prepending “::” to indicate the global namespace.

## Example
```
// main.cpp
using namespace CS_32_F1;
…
void someFunction() {
	cout << "in some function (global namespace)" << endl;
}

int main() {
	// someFunction(); // which one?? – won’t compile.
	::someFunction(); // knows it’s someFunction in global namespace
}
```


