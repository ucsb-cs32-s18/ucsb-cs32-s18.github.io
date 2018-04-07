---
num: "Lecture 2"
desc: "STL, Vectors"
ready: true
date: 2018-04-05 12:30:00.00-7:00
---

# Standard Template Library

It’s really rare if a programming language provides all of the necessary tools to accomplish a task “out of the box”
* Programmers usually use provided building blocks to create something specific to fit their needs
* Programmers are also able to build additional building blocks to build upon as well

These libraries usually come standard with the language
* You don’t have to download separate components
* The libraries should be cross-platform compatible (you shouldn’t have to code differently based on running it with Windows, Mac, or Linux)

Implementing and maintaining libraries come with a cost
* Python has a dedicated organization called the Python Software Foundation
* Java was developed and maintained by Sun Microsystems, which has been bought by Oracle
* C++ isn't "owned" by anyone really

Since C++ isn’t a product of a large organization, and is kinda organized like opensource
* <http://isocpp.org/>, <http://www.open-std.org/>
* Individual c++ compilers are then implemented based on the specifications
	* g++ / clang++ for UNIX
	* Visual Studio for Microsoft
	* ... there isn't any guarantee that these behave EXACTLY the same, but do for the most part based on the specifications
* In this class, we'll assume we're using the C++11 specification unless stated otherwise.

# Standard Libarary Containers
There are many implementations of containers.
* Containers are data abstractions where you can store a sequence of elements.
… and iterators…
* Iterators are a common part of these containers, which allow you to “iterate” through the components
* Depending on the container, you can even read / write from / to these elements

## std::Vector
* A vector is a sequence of objects that are conceptually stored one after the other
* Vectors are implemented with templates, so you can store one kind of object type in the vector container

```
# Makefile
CXX=g++

main: main.o
        ${CXX} -o main -std=C++11 main.o

clean:
        rm -f *.o main
------------
// main.cpp
#include<vector>

using namespace std;

int main() {
	vector<int> v; // a vector containing int elements
return 0;
}
```
Under-the-hood, vectors are implemented using arrays and behave similar to arrays.
* Vectors can be indexed starting from 0 to size – 1
Yet they’re different than arrays…
* Vectors are dynamically-resizable
* Vectors have a size associated with it.
	*Arrays do not know their size and the programmer must be aware of it.

## Adding to a vector example
```
// main.cp
#include<vector>

using namespace std;

template <class T>
void printVector(vector<T> &v) {
	for (int i = 0; i < v.size(); i++) {
		cout << "v[" << i << "] = " << v[i] << endl;

	// range-based for loop example
	// int index = 0;
	// for (int i : v) {
	// 	cout << "v[" << index << "] = " << i << endl;
	// }

	}
}

int main() {
	vector<int> v;
	for (int i = 0; i < 5; i++) // it could be any reasonable size…
		v.push_back(i);

	printVector(v);
	return 0;
}
```
* Like arrays, if you index a vector element that is out of range, you will probably get junk data or make your program crash.
* You can also use the .at() function to access an element.
* Unlike [ ], if .at() references an element that the vector doesn’t contain, an exception is thrown (more on exceptions later).

## Example
```
cout << v.at(4) << endl;
cout << v.at(5) << endl; // EXCEPTION THROWN
cout << v1[5] << endl; // JUNK
```
Other supported operations are:
* front() – returns the first element
* back() – returns the last element
* pop_back() – delete the last element
```
cout << “v.front() = “ << v.front() << endl;
cout << “v.back() = “ << v.back() << endl;
v.pop_back();
printVector(v);
```

## Vector Initialization
`push_back()` is one way to create elements in a vector. Though it’s not the only way
* You can declare a vector with a size initially
* You can also initialize a vector with a size and default values.

## Example:
```
vector<int> v1(100); // initializes vector with 100 elements.
vector<int> v2(100, 1); //initializes vector with 100 elements = 1
```

## Example creating a vector on the heap with a pointer reference to the vector contents on the heap
```
vector<int>* v = new vector<int>(10,1); // vector with 10 elements = 1
cout << v->size() << endl;
printVector(*v);
```

# Iterators
* An iterator is an abstraction for a position in a collection of objects.
* Container classes in the C++ standard library support iterators.
* It’s common to think of an iterator as a pointer to an element’s position
* Though technically it’s not a pointer, but most likely uses a pointer in its implementation.
* Even though iterators are supported between different types of containers, an iterator can only be used with its own container type.

## Example
```
vector<string> v2;

v2.push_back(“Hello.”);
v2.push_back(“My”);
v2.push_back(“name”);
v2.push_back(“is”);
v2.push_back(“Batman”);

for (vector<string>::iterator i = v2.begin(); i < v2.end(); i++) {
	cout << *i << “ “; // string value
	cout << i->size() << endl; // prints the size of the strings
}
```
In the above example, we’ve seen vector functions that deal specifically with iterators.
* begin() – returns an iterator that points to the first element
* end() – returns an iterator that points to the last element
* ++ increments the iterator to the next element
* < compares positions of the iterator
* `*` dereferences an iterator to get the object

## Example (Showing different ways to index elements using iterators):
```
vector<string>::iterator i = x.begin();
cout << vector[4] << endl; 	// Batman
cout << i[4] << endl;		// Batman
cout << *(i + 4) << endl;	// Batman
```

In order to erase items in the vector, there is an `erase` method that requires iterators to do this

## Example of erasing elements
```
// Removing 2nd element of the vector
// v2.erase(v2.begin() + 2); // remove "name"
// printVector(v2);

// Removing 1st and 2nd element - [1,3)
v2.erase(v2.begin() + 1, v2.begin() + 3);
printVector(v2);
```
