---
num: "Lecture 9"
desc: "Inheritance and Polymorphism"
ready: true
date: 2018-05-03 12:30:00.00-7:00
---

# Inheritance
* A way of extending the functionality and properties of an existing class.
	* Allows you to add new features.
	* Allows you to replace existing ones.

## Example (Person / Student Inheritance)
```
// Person.h
#ifndef PERSON_H
#define PERSON_H
class Person {
public:
	Person(std::string name, int age);
	std::string getName();
	int getAge();
	void setName(std::string name);
	void setAge(int age);
private:
	std::string name;
	int age;
};
#endif
```

* Every person should have some identifiable name and age.
* Potential classes that may inherit from a Person are specific type of people (i.e. Students, Soldiers, Artists, Bankers, Musicians, etc.).

```
// Student.h
#ifndef STUDENT_H
#define STUDENT_H
#include "Person.h"

class Student : public Person {
public:
	Student(std::string name, int age, int studentId);
	int getStudentId();
	void setStudentId(int id);
private:
	int studentId;
};
#endif
```
* We say that a Person is the base class (or parent class) of Student
* Student is a derived class (or subclass or child class) of Person.
* The ‘:’ operator here means the Student class inherits everything from a Person class.
	* <i>Public Inheritance</i>: Public members of base class become public members or derived class. Protected members of base class become protected members of derived class.
	* <i>Protected Inheritance</i>: Public and protected members of base class become protected members of derived class.
	* <i>Private Inheritance</i>: Public and protected members of base class become private members of derived class.

```
// Person.cpp
#include <string>
#include "Person.h"

using namespace std;

Person::Person(string name, int age) {
	this->name = name;
	this->age = age;
}

string Person::getName() { return name; }

int Person::getAge() { return age; }

void Person::setName(string name) { this->name = name; }

void Person::setAge(int age) { this->age = age; }
---------
// Student.cpp
#include <string>
#include "Student.h"

using namespace std;

Student::Student(string name, int age, int id) : Person(name, age){
	studentId = id;
}

int Student::getStudentId() { return studentId; }

void Student::setStudentId(int id) { studentId = id; }
```
Note:
* You can initialize your class variables using the initialization list notation.
* You must use this notation when calling the base class’ constructor.
* Even though memory for Person’s attributes are reserved in memory, a subclass cannot access a base class’ private variables by name.
* You must use the base class’ getters and setters.
* The “protected” qualifier can be used to do this.

## Note on constructors and inheritance
* A student is a Person AND a Student
	* Therefore, we must construct the Person first and then construct a Student.
	* This gets done automatically (using the base class’ default constructor) if no explicit base class constructor is used in the initialization list.
		* An error will occur if no default constructor is available in the base class.

# Redefining inherited functions
* If a class inherits a method, but there is specific functionality you want to include in the sub class, then you are able to redefine the function.
* For example, let’s say you want to prepend “STUDENT:” in the getName method for students

```
// in Student.h
std::string getName();

// in Student.cpp
string Student::getName() {
	return "STUDENT: " + name; //ERROR, name isn’t inherited
	return "STUDENT: " + Person::getName; // OK!
} 
```

# Inheritance Types
* We’ve been saying a Student IS A Person, but a Person <b>is not necessarily</b> a Student.
* We can think of class types in a similar way:

```
Person p1(“Chris Gaucho”, 21);
Student s1(“John Doe”, 22, 12345678);

Person p2  = s1; // Legal, a student is a person
Student s2 = p1; // illegal, a person may not be a student
```

# Memory Slicing
* Remember, C++ must reserve memory for each type… so what happens when a Person stores a Student that contains additional information… so how does C++ allocate the memory for a Student?
	* It doesn’t. “Memory slicing” happens where the Person member variables are copied but the Student member variables are not.

```
cout << p2.getName() << endl;
cout << p2.getAge() << endl;
cout << p2.getStudentId() << endl; // ERROR! p2 doesn’t have studentID
```

# Pointers of base types
* A Person pointer can point to Student objects.
* A Student pointer cannot point to a Person object
	* since a student is a Person, but a Person may not be a Student.

```
Person* p1 = new Person("R1", 10);
Student* s1 = new Student("JD", 21, 1234567);

// Student* s2 = p1; 	// Illegal!
Person* p2 = s1;		// OK.
cout << p2->getName() << endl;
cout << p2->getAge() << endl;
cout << p2->getStudentId() << endl;
```

# Destructors and Inheritance
* As far as destructing goes, the process works in reverse
	* Student’s destructor gets called first, then Person’s destructor.
	* Destructor calls are chained upwards (from derived to base)

## Example
```
// in Student.h
~Student();
-----
// in Student.cpp
Student::~Student() {
	cout << "in Student Destructor" << endl;
}
-----
// in Person.h
~Person();
-----
// in Person.cpp
Person::~Person() {
	cout << "in Person destructor" << endl;
}
-----
// in main.cpp
Person* p1 = new Person("R1", 10);
Student* s1 = new Student("JD", 21, 1234567);
delete p1;
cout << "---" << endl;
delete s1;
```

