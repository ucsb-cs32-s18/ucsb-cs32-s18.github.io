---
num: "Lecture 10"
desc: "Inheritance and Polymorphism cont."
ready: true
date: 2018-05-08 12:30:00.00-7:00
---

# Polymorphism (Dynamic Binding) - Read PS 15.3

* When a function is called on a base type object pointing to a subtype, then the appropriate function of the subtype is called.
	* In simpler terms, objects behave appropriately given their constructed type even if assigned to a base-class type.

## Example: Adding a `toString` function to both Person and Student

```
class Person {
public:
…
	std::string toString();
…
};

string Person::toString() {
	return “Person - Name: “ + name + “, age: “ + to_string(age);
}

class Student {
public:
…
	std::string toString();
…
};

string Student::toString() {
	return “Student – ID: “ + to_string(id);
}

// main.cpp
Person p1(“Richert”, 32);
cout << p.toString() << endl;

Student s1(“John Doe”, 21, 12345678);
cout << s.toString() << endl;

Person* p2 = new Person(“Some dude”, 18);
cout << p2->toString() << endl;

Student* s2 = new Student(“Jane Doe”, 19, 23456789);
cout << s2->toString() << endl;

Person* p3 = new Student(“Person Student”, 21, 11111111);
cout << p3->toString() << endl;//uses Person::toString(). Not polymorphic
```

The above example uses Person's toString function instead of Student's even though p3 points to a Student object.
	* Polymorphism isn't used here because you need to explicitly state which functions are polymorphic using the keyword <b>virtual.</b>

```
// add the keyword "virtual" to the toString functions
class Person {
public:
	virtual std::string toString();
…
};

class Student {
public:
	virtual std::string toString();
…
};
```

<b>Note:</b> Technically, we don't need to word "virtual" in Student since the virtual property of the function is inherited as well. However, it's good style to state any virtual function as virtual in the function declaration.
	* By declaring the toString functions as virtual, the previous example will use Student's toString function.

* Notes:
	* Constructors cannot be virtual.
		* They never need to be. The compiler knows exactly what object you're creating and what constructor needs to be called.
	* Destructors can be virtual.
		* If a Person pointer is pointing to a Student, we want to call the destructor for the Student as well. If not, there can be potential memory leaks.


# Pure Virtual Functions and Abstract Classes

There are times where it doesn't make sense for a base class to have a virtual function.

## Example

```
class Shape {
public:
	virtual double area();
};
```

* How would we know how to compute the area of a general Shape? We would need to know what type of shape it is...
* We can make Shape an <b><i>abstract class</i></b> since it can contain fields that all shapes have in common and can inherit from.
* An abstract class is defined as having one or more <i><b>pure virtual functions.</b></i>
* A <b>virtual function</b> can be overridden with an inheriting class by a function with the same signature.
* A <b>pure virtual function</b> is REQUIRED to be implemented by a derived class that is not abstract.
* You cannot create objects of abstract classes (for good reqson since it wouldn't make sense to call `area()` on a general Shape).

## Example (defining a pure virtual function)

```
class Shape {
public:
	virtual double area() = 0;
};
```

You can have references or pointers to abstract classes (i.e. Shape* s is legal and can point to objects of any child class).

```
class Rectangle : public Shape {
public:
	Rectangle() {}
	Rectangle(double length, double width);
	virtual double area();
private:
	double length;
	double width;
};

Rectangle::Rectangle(double length, double width) {
	this->length = length;
	this->width = width;
}

double Rectangle::area() {
	cout << “In Rectangle::area()” << endl;
	return length * width;
}

class Square : public Shape {
public:
	Square(double side);
	virtual double area();
private:
	double side;
};

Rectangle::Square(double side) {
	this->side = side;
}

double Rectangle::area() {
	cout << “In Square::area()” << endl;
	return side * side;
}
```

# Array of Pointers

* The following won't work since abstract classes cannot be instantiated:

```
Shape shapes[2]; // ERROR
```

* But we can <i>point</i> abstract classes to sub classes that inherit and implement the pure virtual function:

```
Shape* shapes[2]; // OK

shapes[0] = new Square(10);
shapes[1] = new Rectangle(3, 4);

cout << shapes[0]->area() << endl;
cout << shapes[1]->area() << endl;
```

The correct area() function will be called on a sub class object if that object is pointed to by Shape* even if Shape does not have an area() definition.

## Example with various scenarios

```
	Rectangle* r = new Rectangle[100]; // Rectangle array on the heap
	//r[0] = new Rectangle(2,2); // ERROR, expects objects, not pointers
	r[0] = Rectangle(2,2); // OK, r[0] is an object

	//Rectangle* r1 = new Rectangle*[100]; // ERROR
	Rectangle** r1 = new Rectangle*[100]; // OK, r1 is a pointer to an array of pointers
	r1[0] = new Rectangle(2,3); // r1[0] is a pointer
	cout << r1[0]->area() << endl;

	Shape* s = new Rectangle(5,5);
	cout << s->area() << endl; // Works as expected.

	Shape* s1[100]; // Array declared on the stack
	s1[0] = new Rectangle(6,6);
	cout << s1[0]->area() << endl; // Works as expected.

	Shape* s2 = new Rectangle[100];
	s2[0] = Rectangle(7,7);
	cout << s2[0].area() << endl;
	// OK, but not what's expected.
	// Memory slicing... Shape doesn't know what length and width are

	delete [] r;	// OK, deletes the array of Rectangles on heap
	delete [] r1;
	// OK, deletes array of Rectangle pointers on heap
	// Be careful, Rectangle objects that elements in r1
	// point to may still be on the heap.
	// You may need to manually delete these as well.

	delete s1[0];
	// OK, deleting a Rectangle object on the heap
	// may receive a warning if Shape does not have a virtual destructor

	//delete [] s1;	// ERROR. Trying to delete something on the stack.
	//delete s2[0];	// ERROR. Trying to delete an object

	delete [] s2;
	// OK, deleting array of Rectangles on heap
	// may receive a warning if Shape does not have a virtual destructor

```







