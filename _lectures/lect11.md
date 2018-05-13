---
num: "Lecture 11"
desc: "Exception Handling"
ready: true
date: 2018-05-15 12:30:00.00-7:00
---

# Exceptions

* <i>Exception handling</i> is a mechanism for specifying and handling error conditions that can occur.
* The code that deals with the error condition (called the <i>exception handler</i>) is said to catch the exception.

## Example

```
int main() {
	int value;
	try {
		cout << “Enter a positive number: “;
		cin >> value;

		if (value < 0)
			throw value;

		cout << “The number entered is: “ << value << endl;
	} catch (int e) {
		cout << “The number entered is not positive.” << endl;
	}
	
	cout << “Statement after try/catch block” << endl;
	return 0;
}
```

* Everything executes within the try block if execution is normal. Only when value < 0 do we throw something.
* We can literally throw any value (basic types, structs, classes, ...).
* The code within the catch block is called the <i>exception handler</i>

# Throwing / Catching Multiple Exceptions

## Example

```
class NegativeValueException {};
class EvenValueException {};

// …
if (value < 0)
	throw NegativeValueException();
if (value % 2 == 0)
	throw EvenValueException();
// …

catch(NegativeValueException e) {
	cout << “The number entered is not positive.” << endl;
} catch (EvenValueException e) {
	cout << “The number entered is even.” << endl;
}
```

* The exceptions are checked one-by-one until the first match occurs.
* If we don't want to (or wouldn't know how) to handle the exception where it occurred, we can "pass it up" to the caller and let them handle the exception.

## Another Example

```
class DivideByZeroException {};

double divide(int numerator, int denominator) throw (DivideByZeroException) {
	if (denominator == 0)
		throw DivideByZeroException();
	return numerator / (double) denominator;
}

int main() {
	try {
		cout << divide(1,1) << endl;
		cout << divide(1,0) << endl;
		cout << divide(2,2) << endl;
	} catch (DivideByZeroException) { // variable name is optional
		cout << “Error: cannot divide by zero” << endl;
	}
}
```

* The function can throw many types of exceptions back to the caller (separated by ',').
* If an exception is never caught, then the program terminates if it isn't caught / handled in main().

# Inheritance and Exceptions

* We can create a hierarchy of exceptions that inherit from a base class.
* If an object is thrown and a catch block with on of its base classes is reached,
	* then the exception handler within the base class' catch block is executed.

## Example:

```
class A {};
class B : public A {};
class C {};

int main() {
	int value;
	try {
		cout << “Enter a positive number: “;
		cin >> value;
	
		if (value < 0)
			throw B();
	} catch (C) {
		cout << “Exception of type C caught.” << endl;
	} catch (A) {
		cout << “Exception of type A caught.” << endl;
	} catch (B) { // maybe compiler error or warning?
		cout << “Exception of type B caught.” << endl;
	}
	return 0;
}
```

Note: Exceptions are checked top-to-bottom. The compiler may provide a warning if A exists before B since an exception of type B will never get caught if thrown in this case.
