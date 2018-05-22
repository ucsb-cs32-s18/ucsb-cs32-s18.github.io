---
num: "Lecture 13"
desc: "Basic OS Concepts / Midterm 2 Review"
ready: true
date: 2018-05-22 12:30:00.00-7:00
---

## Operating System
* "A program that facilitates easy, efficient, fair, orderly, and secure use of various software and hardware resources"
* Can be viewed as a resource manager
* Can manage and share hardware resources with multiple applications
* Operating Systems manage hardware such as
	* mouse, keyboard, monitor, Hard Disk, RAM, Network Interface Card, CPU, Printer...
* Operating Systems provides an interface for programmers to use in the form of libraries / system calls.
	* <b>OS kernel</b> is the "core" of the OS that manages resources.
	* Exists in <b>kernel space</b>, which is separate from user-space where application memory exists.

```
Midterm 2 Review
Logistics
- Bring StudentID and writing utensil
	- Preferably ink or dark led
	- PLEASE WRITE LEGIBLY!!
- No electronic devices
- No book
- No notes

Rooms
- Check email, you were assigned either CHEM 1171 or Phelps 2510
- Multiple versions of the exam
- Seating chart will be posted on the door

Format
- Mix of questions
	- Short answer (briefly describe / define)
	- Write some code
	- True / False (if False, explain why)
	- Fill in the blank
	- Designed exam to take ~ one hour
	- Will cover broad range of topics (cummulative with an emphasis of post-midterm 1 material)

Topics
- Basically everything up to and including last Thursday's lecture (5/17 - Testing)

Hash Tables
- Know basics of hash functions and performance
- Open-address hashing
- Double-hashing
- Chained Hashing
- STL map / unordered_map

Mergesort and Quicksort
- Know the algorithm and how to implement it
- Understand the main ideas and how the arrays are manipulated as the algorithms execute.
- Know the runtime analysis (best / average / worst) and why.

Inheritance
- Understand main concepts and how to implement it
- How to construct / destruct base / sub classes
- Understand memory concepts (base / sub classes and how they are allocated in various scenarios)
- Understand inheritance hierarchy and what valid types
- Pointers to heap / memory on stack / memory slicing

Polymorphism
- What is polymorphism and when you may want to use it
- How to enable polymorphism with "virtual"
- What are Pure virtual functions and abstract classes
- How does it behave in various cases
- How does destructors behave polymorphically

Exceptions
- try / catch mechanism and flow control
- Throwing exceptions
- Exceptions and inheritance

Testing
- Don't need to know the details of googletest framework
- Understand main ideas
	- Unit Test
	- Test Framework
	- Test-Driven development
	- Various cases (normal / boundary / error)
```