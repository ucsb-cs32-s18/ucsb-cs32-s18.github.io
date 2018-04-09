---
layout: lab
num: lab01	
ready: true
desc: "C++ class review, TDD review"
assigned: 2018-04-11 08:00:00.00-7
due: 2018-04-15 23:59:00.00-7
---

# Goals

By the time you have finished this lab, you should have demonstrated
your ability to use a simple test-driven development framework
(familar from last week's lab, and possibly from CS16 and 24 labs) to write
the methods of a simple C++ class with getters.

This C++ class will be used as the basis of next week's lab where we
will work with both insertion sort and selection sort.

# Step by Step 

## Step 0: Getting Started

This lab may be done solo, or in pairs.

Before you begin working on the lab, please decide if you will work solo or with a partner.

As stated in Lab00, there are a few requirements you must follow if you decide to work with a partner. I will re-iterate them here:

* Your partner must be enrolled in the same lab section as you.
* You and your partner must agree to work together outside of lab section in case you do not finish the lab during your lab section. You must agree to reserve at least two hours outside of lab section to work together if needed (preferrably during an open lab hour where you can work in Phelps 3525 and ask a mentor for help). You are responsible for exchanging contact information in case you need to reach your partner.
* If you choose to work with a partner for a future lab where pair programming is allowed, then you must choose a partner you have not worked with before.
* You MUST add your partner on Gradescope when submitting your work <strong>*<u>EACH TIME</u>*</strong> you submit a file(s). After uploading your file(s) on Gradescope, there is a "Group Members" link at the bottom (or "Add Group Member" under "Groups") where you can select the partner you are working with. Whoever uploaded the submission must make sure your partner is part of your Group. Click on "Group Members" -> "Add Member" and select your partner from the list.
* <b> You must</b> write your Name(s) and Perm number on each file submitted to Gradescope.

Once you and your partner are in agreement, choose an initial driver and navigator, and have the driver log into their account.

## Step 1: Copying some programs from my directory

Visit the following web link—you may want to use "right click" (or "control-click" on Mac) to bring up a window where you can open this in a new window or tab:

<http://cs.ucsb.edu/~richert/cs32/misc/lab01/>

You should see a listing of several C++ programs. We are going to copy those into your<tt>~/{{site.course | downcase}}/{{page.num}}</tt> directory all at once with the following command:

<div>
<tt>cp ~richert/public_html/cs32/misc/lab01/* ~/cs32/lab01</tt>
</div>

Note: If you get the error message:


<div>
<tt>cp: target '/cs/student/youruserid/{{site.course | downcase}}/{{page.num}}' is not a directory</tt>
</div>

then it probably means you didn't create a <tt>~/{{site.course | downcase}}/{{page.num}}</tt> directory yet. So do that first.

The `*` symbol in this command is a "wildcard"—it means that we want all of the files from the source directory copy be copied into the destination directory namely <tt>~/{{site.course | downcase}}/{{page.num}}</tt>.

After doing this command, if you `cd` into <tt>~/{{site.course | downcase}}/{{page.num}}</tt> and use the `ls` command, you should see several files in your <tt>~/{{site.course | downcase}}/{{page.num}}</tt> directory&mdash;the same ones that you see if you visit the link <http://cs.ucsb.edu/~richert/cs32/misc/lab01/>


If so, you are ready to move on to the next step.

If you don't see those files, go back through the instructions and make sure you didn't miss a step. If you still have trouble, ask your TA for assistance.


## Step 2: Understanding the Starting Point Code

### Step 2a: Understanding the Makefile 

In this week's Makefile, you'll see a few things:

```make
CXXFLAGS = -Wall -Wextra -Wno-unused-parameter -Wno-unused-private-field

# Change to this before final submission:
# CXXFLAGS = -Wall -Wextra -Werror
```

These are the "flags" used when compiling.  The `-Wno-unused-parameter
-Wno-unused-private-field` flags are used here because we are doing
"test-driven development", and you are starting with "stub code".

Stub code is code that is the minimal amount of code needed to both
(a) compile and (b) definitely fail all of the tests.  It makes sure
that your tests report failure when the code is definitely broken. It
is a way of "testing the tests".

In stub code, you sometimes have unused parameters, and unused data
members (a.k.a. private fields).  We want the compiler to shut up
already about those, because we expect that.

Before you turn in your code though, you want to change up the
compiler flags to say: if there is ANY PROBLEM AT ALL, tell me about
it.  Treat warnings as hard errors that prevent compilation.  We WILL
BE DOING THAT when we check your code.  So, be sure to change this flag as indicated in the comments before you make your final submission.

NEXT: 

```
BINARIES=testStudent1 testStudent2 testStudent3
```

This is a variable that contains a list of the three test programs that we are running this week to test your code.  Note that the variable `BINARIES` is used in several places in the Makefile:

* In the `all:` to say that by default, we want to `make` all of these executable programs (i.e. binaries).
* After tests: to say that we want `make tests` to depend on those binaries being compiled and linked&mdash;note that we then run each of them in turn to actually test our code.
* In the `clean:` rule to say that `make clean` should remove all of the binaries in addition to removing all of the .o files.

There are other things in the Makefile such as the `$^` syntax, and the `$@` syntax. Notice all of these things, and figure out how this Makefile works. A good reference explaining some of the Makefile syntax seen here is <http://www.cs.colby.edu/maxwell/courses/tutorials/maketutor/>. Note that this focuses on compiling C programs, but is still (mostly) relevant for our purposes.

### Step 2b: Understanding the Student class: `Student.h` and `Student.cpp`

Then, look over the `Student.h` and `Student.cpp` files.   

You'll see that the `Student.h` file contains the specification of a
simple C++ class to represent a Student.  We will be using this class
in a future lab as the basis of a Roster of students, and we'll be
working with various sorting and hashing algorithms on this Student
class.

For this week's lab though, we just want to focus on simple
test-driven development of the constructor, getters and a toString
function.

The only file this week where you will be making changes is
`Student.cpp`

### Step 2c: Understanding the tests: `testStudent*.cpp` and `tddFuncs.*`

What you should do next is to look through the test cases in
`testStudent1.cpp`, `testStudent2.cpp` and `testStudent3.cpp`. These
files use a simple test-driven development framework defined in
`tddFuncs.h` and `tddFuncs.cpp`.

Look over these files and understand how they work.  Then, type `make
tests` to compile and run all of the tests.

You can also type, for example, `make testStudent1` and
`./testStudent1` to make and run these tests one at a time.

When you are ready, start editing `Student.cpp`, replacing the stubs for
the constructor first, and then each of the stubs for the other
functions.

<div class="tip">
<h4>Tip: A special note about the `toString` function</h4>
Note that in the case of the `toString` function, a correct implementation is already provided, but commented out.  

This example can be used as the basis for writing similar `toString` functions in future labs. This is the only time we will provide an example of this technique, so please study it well, and if you have questions about it, please ask.  
</div>

## Step 3: Make all the test cases pass 

Make the test cases pass by replacing the stubs in `Student.cpp` with working code.  This is the only file you should need to change.

## Step 4: Checking your work before submitting

When you are finished, you should be able to type `make clean` and then `make tests` and see the following output:

```bash
-bash-4.2$ make tests
clang++ -Wall -Wextra -Wno-unused-parameter -Wno-unused-private-field   -c -o testStudent1.o testStudent1.cpp
clang++ -Wall -Wextra -Wno-unused-parameter -Wno-unused-private-field   -c -o Student.o Student.cpp
clang++ -Wall -Wextra -Wno-unused-parameter -Wno-unused-private-field   -c -o tddFuncs.o tddFuncs.cpp
clang++ testStudent1.o Student.o tddFuncs.o -o testStudent1
clang++ -Wall -Wextra -Wno-unused-parameter -Wno-unused-private-field   -c -o testStudent2.o testStudent2.cpp
clang++ testStudent2.o Student.o tddFuncs.o -o testStudent2
clang++ -Wall -Wextra -Wno-unused-parameter -Wno-unused-private-field   -c -o testStudent3.o testStudent3.cpp
clang++ testStudent3.o Student.o tddFuncs.o -o testStudent3
./testStudent1
Testing class Student...
PASSED: s1.getPerm()
./testStudent2
Testing class Student...
PASSED: s1.getLastName()
PASSED: s1.getFirstAndMiddleNames()
./testStudent3
Testing class Student...
PASSED: s1.getFullName()
PASSED: s1.toString()
-bash-4.2$ 
```

At that point, you are ready to try submitting on the Gradescope system.

## Step 5: Submitting via Gradescope

The lab assignment "Lab01" should appear in your Gradescope dashboard in CMPSC 32. If you haven't submitted anything for this assignment yet, Gradescope will prompt you to upload your files.

For this lab, you will need to upload your modified files (i.e. `Student.cpp`). You either can navigate to your file, "drag-and-drop" them into the "Submit Programming Assignment" window, or even use a GitHub repo to submit your work.

If you already submitted something on Gradescope, it will take you to their "Autograder Results" page. There is a "Resubmit" button on the bottom right that will allow you to update the files for your submission.

For this lab, if everything is correct, you'll see a successful submission passing all of the autograder tests.

**Remember to add your partner to Groups Members for this submission on Gradescope if applicable. At this point, if you worked in a pair, it is a good idea for both partners to log into Gradescope and check if you can see the uploaded files for Lab01.**

# Grading Rubric 

<b>(100 pts)</b> assigned from Gradescope autograding. The "secret tests" are ones that were not provided to the students. This prevents you from, for example, just "hard coding" values to pass the tests.

