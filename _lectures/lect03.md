---
num: "Lecture 3"
desc: "Class Design"
ready: true
date: 2018-04-10 12:30:00.00-7:00
---
 
# Classes

* Classes are a representation of a custom-defined type.
* Classes consist of:
	* An <i>interface</i>: What operations and variables are available when using this class.
	* An <i>implementation</i>: The definition of how things are done.

## Example - definition of a class representing a Person
```
-------
# Makefile

CXX=g++

main: main.o
	${CXX} -o main -std=C++11 main.o

clean:
	rm -f *.o main
-------
// main.cpp
// Let's define the class in one file for now...

#include<iostream>
using namespace std;

// A class Person interface
class Person {
	public:
		Person(); 				// default constructor
		Person(string name, int age);
		Person(Person& person);		// copy constructor
		string getName() const; 	// accessor / getter
		int getAge() const; 		// accessor / getter
		void setName(string name); 	// mutator / setter
		void setAge(int age);		// mutator / setter

	private:
		string name;
		int age;
};

// default constructor
Person::Person() {
	name = "-";
	age = 0;
}

// constructor overloading
Person::Person(string name, int age) {
	this->name = name;
	this->age = age;
}

// copy constructor
Person::Person(Person& person) {
	name = person.getName();
	age = person.getAge();
	cout << "copy constructor" << endl;
}

string Person::getName() const { return name; }

int Person::getAge() const { return age; }

void Person::setName(string name) { this->name = name; }

void Person::setAge(int age) { this->age = age; }

int main() {
	Person p;
	return 0;
}
```
## Public vs. Private
* The variables and functions declared as private cannot be referenced anywhere except within the class’ functions.
* The variables and functions declared as public can be referenced anywhere.
	* Why is this good?
		* Prevents unintended side-effects.
		* Hides complex details consumers of the class may not be concerned with.

## Abstract Data Types (ADTs):
* A data type where the programmers who use this class do not have access to the details of how the values and operations are implemented.
	* Also known as data hiding, data abstraction, and encapsulation.
	* Typically, a consumer of the class only needs to be aware of all the public fields.
	* Imagine needing to know / manipulate buffers in iostream in order to print "Hello World"!

## Scope Resolution Operator
* When a member function is defined, the definition must include the class name because there may be two or more classes that have member functions with the same name.
* Without it, the compiler does not know which class’ member function the definition is for.

## Accessor and Mutator Functions
* A function that simply returns private members’ values are called accessor (getter) functions (i.e. they access the data).
* A function that simply sets private members’ values are called mutator (setter) functions (i.e. they change the data).

## Constructors
* A special kind of function with the same class name that it’s defined in.
* A constructor is called when an object of that class is declared.
* Constructors are the only functions that do not have a return type.
* Default constructors can be defined by you (which is good style).
* If a default constructor is not defined, the compiler will generate one if no other constructor is defined! <b>Otherwise it will not.</b>

## Copy Constructor
* Take in an existing Object in a constructor's parameter and set all of its fields to the fields of the object, thus copying one object's fields to the current object.
* Copy constructors must pass its parameter by reference…
* If a copy constructor is not defined, then the compiler will generate one. However, this copy constructor only does a SHALLOW copy.
	* Think of it as copying the reference of memory, not the memory contents.
	* Two references may now share the same memory of an object…
* Try it: Comment out the defined copy constructor and note that
```
Person s;
Person t = s;
```
still works. If the copy constructor is defined, then the assignment operator `=` will call the defined copy constructor. If the copy constructor is not defined, the default copy constructor is used.

### Shallow Copy illustration
```
// modify class definition with vector v
public:
vector<int>* getVector() const;

private:
vector<int>* v;

// modify constructor to initialize vector and push 100 into it
Person::Person() {
	name = "default name";
	age = 0;
	v = new vector<int>();
	v->push_back(100);
}

// Accessor function for the vector v
vector<int>* Person::getVector() const {
	return v;
}

// function to print out contents of the vector
template<class T>
void printVector(vector<T> v) {
	for (int i = 0; i < v.size(); i++) {
		cout << v[i] << endl;
	}
}


s.getVector()->push_back(200);
printVector(*s.getVector()); // 100 200
printVector(*t.getVector()); // 100 200
```

Vector is shared between two objects due to the shallow copy!

One way to do a "deep copy" of the vector is
```
Person::Person(Person& person) {
	name = person.getName();
	age = person.getAge();
	v = new vector<int>();
	
	// DEEP COPY
	for (int i = 0; i < person.getVector()->size(); i++) {
		v->push_back(person.getVector()->at(i));
	}
	cout << "copy constructor" << endl;
}
```
## Destructor
* A special member function that is called when a reference to an object
	* Goes out of scope.
	* Or a pointer to the object is called with <b>delete</b>.

# Example of separating the Person class into multiple files
```
// Person.h
#ifndef PERSON_H
#define PERSON_H

#include <string>
#include <vector>

// A class interface
class Person {
	public:
		Person(); // default constructor
		Person(std::string name, int age);
		Person(Person& person);
		~Person(); 					// destructor
		std::string getName() const; 	// accessor / getter
		int getAge() const; 		// accessor / getter
		std::vector<int>* getVector() const; 
		void setName(std::string name); 	// mutator / setter
		void setAge(int age);		// mutator / setter

	private:
		std::string name;
		int age;
		std::vector<int>* v;
};

#endif
---------------------
// Person.cpp
#include <iostream>
#include "Person.h"

using namespace std;

Person::Person() {
	name = "default name";
	age = 0;
	v = new vector<int>();
	v->push_back(100);
}

Person::Person(string name, int age) {
	this->name = name;
	this->age = age;
}

Person::Person(Person& person) {
	name = person.getName();
	age = person.getAge();
	
	v = new vector<int>();
	
	// deep copy
	for (int i = 0; i < person.getVector()->size(); i++) {
		v->push_back(person.getVector()->at(i));
	}

	cout << "copy constructor" << endl;
}

Person::~Person() {
 	delete v;
 	cout << "DELETED: v" << endl;
 }

vector<int>* Person::getVector() const {
	return v;
}

string Person::getName() const {
	return name;
}

int Person::getAge() const {
	return age;
}

void Person::setName(string name) {
	this->name = name;
}

void Person::setAge(int age) {
	this->age = age;
}
-------------
// main.cpp

#include <iostream>
#include "Person.h"

using namespace std;

template<class T>
void printVector(vector<T> v) {
	for (int i = 0; i < v.size(); i++) {
		cout << v[i] << endl;
	}
}

// just illustrating destructor gets called when out of scope…
void f() {
	Person* p = new Person();
	delete p;
}

int main() {
	f();
	cout << "exiting main..." << endl;
	return 0;
}
----
# Makefile

CXX=g++

main: main.o Person.o
	${CXX} -o main -std=C++11 main.o Person.o

clean:
	rm -f *.o main
```

<b>Note:</b> You should not use `using namespace ...` in your header files. This can have unintended side-effects for consumers of this class that are not expecting to use the namespace.














