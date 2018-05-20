---
num: "Lecture 12"
desc: "Testing"
ready: true
date: 2018-05-17 12:30:00.00-7:00
---

# Testing

For additional details and context on Testing, refer to pages 147 - 214 in the CS32 Reader.

## Complete Test
* Testing every possible path in every possible situation.
* Complete tests are infeasible!
* The best we can hope for is trying to approximate a Complete Test by testing various types of cases.
* The more rigorous testing a program can “pass”, the more confidence is gained that the program is “bulletproof” (handles every error as expected).

## Unit Testing
* Testing individual pieces (units) of a program (small and large) to ensure correct behavior.
* Good software practice is structuring your program into modular units.
* Good tests generally cover interesting cases including:
	* Normal Cases: Cases where the input is generally what we expect.
	* Boundary Cases: Cases that test the edge values of possible inputs.
	* Error Cases: Invalid cases (like passing a string instead of an int).
		* C++ catches most of these types of errors during the compilation process.
		* Other languages, such as Python, may need to rigorously check invalid input cases.

## Test Suite
* A program containing various tests confirming certain behavior.
* A good way to <i>automate</i> tests.
	* Very important for large-scale projects where other engineers may make a change that affects functionality of other existing (or new) functionality.
* We've seen testing programs in several of our lab assignments testing students' submissions throughout the quarter.

## Example: Writing our own simple program testing a function that takes four integers and returns the largest

```
// main.cpp
#include <iostream>
#include <string>

using namespace std;

int biggest(int a, int b, int c, int d) {
	if (a >= b && a >= c && a >= d)
		return a;
	else if (b >= a && b >= c && b >= d)
		return b;
	else if (c >= a && c >= b && c >= d) // comment out and see
		return c;						 // an error
	else
		return d;
}
void runTestCase(int a, int b, int c, int d, int expected) {
	int result = biggest(a, b, c, d);
	if (result != expected)
		cout << "ERROR: " << result << " != " << expected << endl;
	else
		cout << "PASSED: " << result << " == " << expected << endl;
}
int main() {
	// Write some interesting tests
	runTestCase(1,2,3,4,4);
	runTestCase(3,3,3,3,3);
	runTestCase(1,2,5,4,5);
	//...

	return 0;
}
```

## Test-Driven Development
* Write test cases that describe what the intended behavior of a unit of software should BEFORE implementing the functionality.
	* Defines the requirements of your piece of software.
* Implement the details of the functionality with the intention of passing the tests.
* Repeat until the tests pass.
* Imagine large software products where dozens of engineers are trying to add new features / implement optimizations all at the same time.
	* Having a “suite” of tests before deploying software to the public is essential.
	* Someone may modify changes that work for a current version, but breaks functionality in another version
	* Rigorous tests enable confidence in the stability in software.

## Testing Frameworks
* Many languages have their own testing frameworks to support software unit testing.
	* Java has JUnit
	* Python has pytest
	* C++ has several frameworks, but googletest is a popular choice.
		* A good page explaining how to install googletest for MacOS: http://www.deanbodenham.com/learn/cpp-googletest.html

## Example of Unit Testing a `House` class implementation
```
// House.h
#ifndef HOUSE_H
#define HOUSE_H

class House {
public:
	House();
	House(House& house);
	int getSize() const;
	double getPrice() const;
	void setSize(int size);
	void setPrice(double price);
	double increasePrice(double percentage);
private:
	int size;
	double price;
};

#endif
--------
// House.cpp

#include "House.h"

House::House() {
	size = 0;
	price = 0;
}

House::House(House& house) {
	size = house.size;
	price = house.price;
}

int House::getSize() const { return size; }

double House::getPrice() const { return price; }

void House::setSize(int size) { this->size = size; }

void House::setPrice(double price) { this->price = price; }

double House::increasePrice(double percentage) {
	price += price * percentage;
	return price;
}
--------
// main.cpp (test program)
#include <iostream>
#include <string>

#include "House.h"
#include <gtest/gtest.h> // assuming googletest is installed

using namespace std;

// Test Default Constructor
TEST(testConstructor, ConstructorTests) {
	House h;
	ASSERT_EQ(h.getPrice(), 0);
	ASSERT_EQ(h.getSize(), 0);
}

// Test set / get Price
TEST(testGetterSetter, getterSetterTests) {
	House h;
	h.setPrice(100);
	ASSERT_EQ(h.getPrice(), 100);
	h.setPrice(-10);
	ASSERT_EQ(h.getPrice(), -10);
	h.setPrice(1000000);
	ASSERT_EQ(h.getPrice(),1000000);
}

// Test increasePrice
TEST(testIncreasePrice, increasePriceTests) {
	House h;
	h.setPrice(100);
	ASSERT_EQ(h.increasePrice(1), 200);
	ASSERT_EQ(h.increasePrice(-0.2), 160);
	ASSERT_EQ(h.increasePrice(-1), 0);
}

int main(int argc, char* argv[]) {
	testing::InitGoogleTest(&argc, argv);
	return RUN_ALL_TESTS();
}
--------
// build command (assuming ~/.bash_profile is configured as mentioned
// in the installation instructions above)
$ googletest main.cpp House.cpp
```

For more information on usage of googletest, see `https://github.com/google/googletest/blob/master/googletest/docs/Primer.md`

