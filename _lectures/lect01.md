---
num: "Lecture 1"
desc: "Introduction, Compilation Basics"
ready: true
date: 2018-04-03 12:30:00.00-7:00
---

# Course Syllabus

Be sure to read the course syllabus for information on the logistics of this course.

<https://ucsb-cs32-s18.github.io/info/syllabus/>

# Makefiles (a simple example)

```
// main.cpp
#include <iostream>

using namespace std;

int main() {
	cout << "Hello CS 32!" << endl;
	return 0;
}
```

## Can compile this with g++ or clang++:

```
$ g++ main.cpp
$ ls
a.out		main.cpp
$ ./a.out
Hello CS 32!
```

* Note that the executable is called `a.out`. This is the default name of the executable.

## Using `make` command

```
$ make main
c++     main.cpp   -o main
```

* This default behavior of `make` tries to compile the .cpp with that name and output the executable to that name.
* Works well for very simple programs that exist in one file.

## Change the output of the executable with the `-o` flag
```
$ g++ -o main main.cpp
$ ls
functions.cpp	functions.h	main		main.cpp
$ ./main
Hello CS 32!
```
* Changes the executable name from `a.out` to `main`

# C++ Build Process

1. Preprocessor: Text-based program that runs before the compilation step. Looks for statements such as #include and modifies the source which is the input for compilation.

2. Compiler: A program that translates source code into “object code,” which is a lower-level representation optimized for executing instructions on the specific platform. Lower level representations are usually stored in a .o (object) file.

3. Linker: Resolves dependencies and maps appropriate functions located in various object files. The output of the linker is an executable file for the specific platform.

# Compiling multiple files example
```
--------
// functions.h

int doubleInt(int x);
--------
// functions.cpp

int doubleInt(int x) {
	return 2 * x;
}
--------
// main.cpp
#include <iostream>
#include “functions.h”

using namespace std;

int main() {
	cout << doubleInt(12) << endl;
return 0;
}
--------
```
* We can't just compile main.cpp anymore...
```
$ g++ main.cpp
Undefined symbols for architecture x86_64:
  "doubleInt(int)", referenced from:
      _main in main-7c4a04.o
ld: symbol(s) not found for architecture x86_64
clang: error: linker command failed with exit code 1 (use -v to see invocation)
```
* we see a "linker" error.
* The linker doesn't know where to find the `doubleInt()` function definition.
* We need to compile `functions.cpp` so `main.cpp` knows where to find the `doubleInt()` function.
```
$ g++ -o main main.cpp functions.cpp
$ ls
functions.cpp	functions.h	main		main.cpp
$ ./main
24
```
* Makefiles are useful since writing commands with many files is tedious and error-prone.
* Makefiles are used to define compilation rules and dependencies so we can simply type `make [some_target]` and not have to type everything out all the time.

# General format of a Makefile
```
[target]: [dependencies]
	[commands]

Example:
--------
# Makefile

main: functions.cpp main.cpp
	g++ -o main main.cpp functions.cpp
--------

$ make main
g++ -o main main.cpp functions.cpp
$ make main
make: `main' is up to date.

```
* In this case, `make` uses timestamps to determine if something needs to be recompiled.
* If a recent change occurred, then it will recompile. If nothing changes, then nothing is done since everything is `up to date`

## Note:
* The object (.o) files are not explicitly generated.
* You will need to use the `-c` (compile only) flag.
* Having make use .o files as a dependency is useful for maintenance reasons.
	* Forces recompilation of source (.cpp) files

```
# Makefile

main: functions.o main.o
	g++ -o main main.o functions.o

$ make main
c++    -c -o functions.o functions.cpp
c++    -c -o main.o main.cpp
g++ -o main main.o functions.o
$ ls
Makefile	functions.h	main		main.o
functions.cpp	functions.o	main.cpp
```
## Variables in Makefiles
```
# Makefile
#CXX=clang++
CXX=g++
DEPENDENCIES=functions.o main.o

main: ${DEPENDENCIES}
	${CXX} -o main ${DEPENDENCIES}

clean:
	rm -f *.o main
```

## make clean
```
--------
# Makefile
main: functions.o main.o
	g++ -o main main.o functions.o

clean:
	rm -f *.o main
--------
```
* If we want to "start fresh" and recompile everything, it's nice to have a "clean" target to remove all object files and the executable

