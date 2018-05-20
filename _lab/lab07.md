---
layout: lab
num: lab07
ready: true
desc: "Exceptions and Template Classes"
assigned: 2018-05-23 08:00:00.00-7
due: 2018-05-27 23:59:00.00-7
---

# Goals

* This lab will review some concepts like a templated container class (SimpleList).
* This lab will cover implementing a class that supports Exceptions - your functionality of the class will throw an Exception to the caller under certain conditions.
* Your template class implementation will support pointer types and should deallocate memory on the heap properly in order to avoid memory leaks.

# Step by Step

## Step 0: Getting Started

This lab may be done solo, or in pairs.

Before you begin working on the lab, please decide if you will work solo or with a partner.

As stated in previous labs, there are a few requirements you must follow if you decide to work with a partner. I will re-iterate them here:

* Your partner must be enrolled in the same lab section as you.
* You and your partner must agree to work together outside of lab section in case you do not finish the lab during your lab section. You must agree to reserve at least two hours outside of lab section to work together if needed (preferably during an open lab hour where you can work in Phelps 3525 and ask a mentor for help). You are responsible for exchanging contact information in case you need to reach your partner.
* If you choose to work with a partner for a future lab where pair programming is allowed, then you must choose a partner you have not worked with before.
* You MUST add your partner on Gradescope when submitting your work <strong>*<u>EACH TIME</u>*</strong> you submit a file(s). After uploading your file(s) on Gradescope, there is a "Group Members" link at the bottom (or "Add Group Member" under "Groups") where you can select the partner you are working with. Whoever uploaded the submission must make sure your partner is part of your Group. Click on "Group Members" -> "Add Member" and select your partner from the list.
* <b> You must</b> write your Name(s) and Perm number on each file submitted to Gradescope.

Once you and your partner are in agreement, choose an initial driver and navigator, and have the driver log into their account.

## Step 1: Get the {{page.num}} starter code into your repository directory

In this step, we are going to copy the {{page.num}} starter files from the instructor's directory into your <tt>/cs32/{{page.num}}</tt> directory.

The files are in the instructors directory at 

<tt>~richert/public_html/cs32/misc/lab07/*</tt>

and also accessible via the URL

<http://cs.ucsb.edu/~richert/cs32/misc/lab07/>

You want to copy these files into your <tt>~/cs32/{{page.num}}</tt> directory.

## Step 2: Implement the SimpleList.cpp functionality.

* `SimpleList.h` is given in the starter code, and your task is to provide the proper implementation for the `SimpleList` class.

A few notes about this specific implementation (as described in `SimpleList.h`):

* This class will use templates and a SimpleList can store any type.
* Your container will be an array (elements) of a templated type.
	* This array will be allocated on the heap.
* You may assume that your list capacity is 10 elements (defined as CAPACITY).
* You will need to keep track of the current number of items in your SimpleList using the numElements variable.

A few notes about throwing Exceptions:

Your implementation will need to implement the following functions, and throw Exceptions in certain cases:

`template <class T>`
* `SimpleList();`
	* SimpleList constructor that sets numElements to 0 (i.e. the SimpleList is constructed with 0 elements). Also allocates the array elements with a size of CAPACITY.
* `~SimpleList();`
	* SimpleList destructor must delete the dynamically allocated array on the heap as well as deleting any elements in SimpleList that exist on the heap.
* `T at(int index) const throw (InvalidIndexException);`
	* Returns the element at index location. Throws a InvalidIndexException if there is no element at index.
* `bool empty() const;`
	* Returns true if the list is empty, false otherwise.
* `T first() const throw (EmptyListException);`
	* Return the element at index 0. Throws an EmptyListException if the list is empty.
* `T last() const throw (EmptyListException);`
	* Return the last element in the SimpleList. Throws an EmptyListException if the list is empty.
* `int getNumElements() const;`
	* Returns the number of items currently stored in the SimpleList.
* `void insert(T item) throw (FullListException);`
	* Inserts at item at the first possible slot towards the end of the list. Throws a FullListException if the list is at Capacity.
* `void remove(int index) throw (InvalidIndexException, EmptyListException);`
	* Removes the element at index. You will need to shift all elements inserted after the index position down slot in the array in order to prevent any "holes" in the SimpleList.
	* First checks if the SimpleList is empty - throws an EmptyListException if the SimpleList is empty.
	* Throws an InvalidIndexException if there is no element at the index position.

Another note on checking if a template type is a pointer:

* You may find the following std functionality handy if you want to determine if a Template type is a pointer or not:
	* `std::is_poiner<T>::value` in `<type_traits>`.
	* This will return true if `T` is a pointer type, and false otherwise.
* You may also encounter a compilation issue when attempting to delete a Template pointer type `T` (and not `T*`).
	* C++ is kinda finicky about this, but there are ways to destruct elements of Templated pointer types.
	* C++ isn't happy when trying calling `delete` on a template type that is a pointer, but is not <i>explicitly</i> declared as a pointer in the parameter argument (even if it passes the `is_pointer<T>::value` check).
	* You can get around it by overloading functions declaring `T` specifically as a pointer type (or not). For example, here is a simple proof-of-concept illustrating this point:

```
template<class T>
void destroy(T element) {
	// do nothing
}

template <class T>
	void destroy(T* element) {
	// delete the pointer type
	delete element;
}

template <class T>
void function1(vector<T> x) {
	if (is_pointer<T>::value) {
		//delete x[0]; // may not compile even if T is a pointer type

		// Will call destroy(T* element)
		destroy(x[0]);
	} else {
		// will call destroy(T element)
		destroy(x[0]);
	}
}

int main() {
	vector<int*> x;
	int* y = new int;
	x.push_back(y);
	function1(x);
	return 0;
}
```

## Step 3: Testing

The following executables will be generated by typing `make all`:

* `testSimpleList1`
* `testSimpleList2`
* `testSimpleList3`

You can test each executable separately by executing each individual binary file or you can run all tests by typing `make tests`.

There will also be a memory test for testSimpleList3 that will check for memory leaks. This will use testSimpleList3 to see if your code is deallocating memory properly. You can run this memory test after `testSimpleList3` is compiled with:

`make lt01`

## Step 4: Submitting via Gradescope

You will turn in `SimpleList.cpp` for this lab.

The lab assignment "Lab07" should appear in your Gradescope dashboard in CMPSC 32. If you haven't submitted anything for this assignment yet, Gradescope will prompt you to upload your files.

For this lab, you will need to upload your modified files (i.e. `SimpleList.cpp`). You either can navigate to your file, "drag-and-drop" them into the "Submit Programming Assignment" window, or even use a GitHub repo to submit your work.

If you already submitted something on Gradescope, it will take you to their "Autograder Results" page. There is a "Resubmit" button on the bottom right that will allow you to update the files for your submission.

For this lab, if everything is correct, you'll see a successful submission passing all of the autograder tests.

**Remember to add your partner to Groups Members for this submission on Gradescope if applicable. At this point, if you worked in a pair, it is a good idea for both partners to log into Gradescope and check if you can see the uploaded files for Lab07.**

