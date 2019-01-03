---
layout: lab
num: lab00	
ready: true
desc: "Review of C++ basics, Makefiles, Gradescope"
assigned: 2019-01-07 08:00:00.00-7
due: 2019-01-14 23:59:00.00-7
---

Goals
=====

By the time you have finished this lab, you should have demonstrated
your ability to:

-   Join the Github Organization <https://github.com/ucsb-cs32-f18/>
-   Use some basic Unix commands, and learn about new Unix commands
-   Create a basic Makefile from scratch
-   Do some simple C++ programming as review of C++ basics, and as
    preliminary work towards understanding sorting algorithms
-   Learn how to submit work using the Gradescope system

Step by Step
============

Step 0: Getting Started
-----------------------

### Step 0a: Make sure you have a CSIL account and know how to use it

Ideally, before this lab begins, you will have been instructed to visit
the link below, and create your "College of Engineering" computer
account:

-   <https://accounts.engr.ucsb.edu/create>

<strong>You should already know the following from CS16 / CS24. If not, alert your TA/instructor immediately:</strong>

-   How to login with your CoE/CSIL account
-   How to use the Linux computers in
    -   <strong>Phelps 3525</strong> (where your discussion sections are scheduled), and
    -   <strong>CSIL</strong>, the Computer Science Instructional Lab on the first floor of Harold Frank Hall (accessed through an outside door on the side facing the ocean.), which have an identical setup.

### Q: Can I work on my own computer? A: MAYBE. MAYBE NOT.

It MIGHT, SOMETIMES, be possible to do SOME of the course work on your own computer that is connected to the Internet. In lecture, I will give VERY brief demonstrations of how to access the CSIL machines over the internet using Windows, Mac, and Linux.

But for some of the assignment, using CSIL is required. You might be able to access CSIL over the internet from your own machine rather than coming to CSIL in person.

At the links below, we a "best effort" introduction to "how to do work
on your own computer", and then YOU ARE ON YOUR OWN.

-   There is no guarantee that this will always work.
-   There are two many different OS versions, flavors, configurations, etc.for us to know the ins and outs of every single one.
-   If/when you run into difficulties there, WE CANNOT BE YOUR TECH SUPPORT. If you have a simple question and we know the answer, we'll tell you, but if you don't, our answer will be: "ok, then do your work in CSIL until you figure it out."

So, please be aware:

-   The primary computing environment for this course is the Phelps and CSIL labs.
-   The CSIL labs are open from early in the morning to late at night every day of the week.
-   Though many labs can be done from your own computer, there may be some that require you to work on CSIL (either over the internet, or coming in person.)

If you are working from your own computer at home or in your dorm, i.e. in not in Phelps 3525, or the CSIL Lab, you may need information on:

-   [how to access CSIL from Windows](https://ucsb-cs8.github.io/topics/csil_via_windows/) OR
-   [how to access CSIL from Mac or Linux via ssh](https://ucsb-cs8.github.io/topics/csil_via_macos/)

### Step 0b: Adding yourself to our GitHub organization

We will be using github.com in this course. We have created an organization on github.com <https://github.com/ucsb-cs32-f18> where you can create repositories (repos) for your assignments in this course. You may be familiar with GitHub organizations from CS 16 and 24 if you took it with Prof. Mirza. The advantage of creating private repos under that organization is that the course staff (your instructors, TAs and mentors) will be able to see your code and provide you with help, without you having to do anything special.

To join this organization, you need to do four things.

(1) If you don't already have a github.com account, create one on the "free" plan.
(2) If you don't already have your @umail.ucsb.edu email address associated with your github.com account, go to "settings", add that email, and confirm that email address.
(3) Visit <https://ucsb-cs-github-linker.herokuapp.com> and login with your github.com account. Click "Home", find this course, and click the "join course button". That will automatically send you an invitation to join the course organization. There is a link to the invitation for the GitHub organization for this course (<https://github.com/ucsb-cs32-f18>). 
(4) Click on the invitation link and accept it. You can also go straight to <https://github.com/ucsb-cs32-f18> and accept the invitation there.

If you are not familiar with git, I highly recommend learning this skill since this will be extremely valuable when collaborating on large software projects. More information on git can be found here: <https://ucsb-cs32.github.io/topics/git/>.

<b> IMPORTANT NOTE! </b>
You can create your own repos under this organization when working on your labs. However, be sure to create your repo as *private*, since if it's public, then anyone can view its contents. Since all students are responsible for their own work, having your solutions visible to everyone creates a situation that is considered to be a form of academic dishonesty.

If there are any issues or questions, please post them on Piazza and include any relevant screenshots, which may help us investigate any issues.

### Step 0c: Creating your Gradescope account

I have manually added everyone (using your @umail.ucsb.edu accounts) currently enrolled in the course to the Gradescope system. You should have received an email from the Gradescope system asking you to create a password. Once you follow the instructions to set your password, you should have access to the autograding system. You should see "CMPSC 32" in your Fall 2018 Courses.

The lab assignment "Lab00" should appear in your Gradescope dashboard in CMPSC 32. 

### Step 0d: Decide: Working solo or pair?

This lab may be done solo, or in pairs.

Before you begin working on the lab, please decide if you will work solo or with a partner.

If you decide to work with a partner:

* Review the following explanation on [pair programming and Falco's strong-style pair programming](https://tobeagile.com/2017/01/11/strong-style-pairing/).
* Make an agreement to be respectful and work together to maximize your learning benefit.
* There are many ways to do pair programming and we encourage you to:
    * Try and find a partner that is of a similar skill level (or similar confidence) with C++ programming.
    * Try and find a style that works best for you and your partner.
        * Many pairs find that switching roles is best done once per "step".
        * Others may find switching roles after 10, 15, or 20 minute increments works better.

The following arrangement is <strong>NOT OK</strong>.

* Student A and Student B form a pair.
* Student A works on the lab alone on Wednesday night.
* Student B obtains the work Student A did on Thursday night and works alone to finish the lab.

<strong>This is *NOT* how pair programming is done!</strong>

There are a few requirements you must follow if you decide to work with a partner:

* Your partner must be enrolled in the same lab section as you.
* You and your partner must agree to work together outside of lab section in case you do not finish the lab during your lab section. You must agree to reserve at least two hours outside of lab section to work together if needed (preferrably during an open lab hour where you can work in Phelps 3525 and ask a mentor for help). You are responsible for exchanging contact information in case you need to reach your partner.
* If you choose to work with a partner for a future lab where pair programming is allowed, then you must choose a partner you have not worked with before.
* You MUST add your partner on Gradescope when submitting your work <strong>*<u>EACH TIME</u>*</strong> you submit a file(s). After uploading your file(s) on Gradescope, there is a "Group Members" link at the bottom (or "Add Group Member" under "Groups") where you can select the partner you are working with. Whoever uploaded the submission must make sure your partner is part of your Group. Click on "Group Members" -> "Add Member" and select your partner from the list.
* <b> You must</b> write your Name(s) and Perm number on each file submitted to Gradescope.

Once you and your partner are in agreement, choose an initial driver and navigator, and have the driver log into their account.

### Step 0e: Create your \~/cs32/lab00 directory

Create a \~/cs32/lab00 directory and make it your current directory. You
should already know how to do this from previous courses, but in case you need a reminder:

    mkdir ~/cs32
    mkdir ~/cs32/lab00
    cd ~/cs32/lab00

You are responsible for knowing the `mkdir` and `cd` commands—though these should be review, so they will not be covered in detail. Questions about their use, however, appear on any exam in this course. So if, up to this point, you've just "followed the instructions" without really understanding what you are doing, the time for that has passed.

You are responsible for knowing the the "shell" is the program that you type Unix commands into—commands such as mkdir, cd, etc.

You are also responsible for knowing that the tilde symbol (`~`) stands for "the user's home directory", but only in the shell. There are many contexts where you cannot use the `~` symbol—in fact, almost everywhere other than the Unix command line that a filename is needed, you actually CANNOT use the tilde.

Step 1: Copying some programs
-----------------------------

Visit the following web link—you may want to use "right click" (or "control-click" on Mac) to bring up a window where you can open this in a new window or tab:
<http://cs.ucsb.edu/~richert/cs32/misc/lab00/>
You should see a listing of several C++ programs. We are going to copy those into your ~/cs32/lab00 directory all at once with the following command:
```
cp ~richert/public_html/cs32/misc/lab00/* ~/cs32/lab00
```
Note: If you get the error message:
```
cp: target '/cs/student/youruserid/cs32/lab00' is not a directory
```

then it probably means you didn't create a `~/cs32/lab00` directory yet. So do that first. The `*` symbol in this command is a "wildcard" — it means that we want all of the files from the source directory copy be copied into the destination directory namely `~/cs32/lab00.` After doing this command, if you `cd` into `~/cs32/lab00` and use the `ls` command, you should see several files in your `~/cs32/lab00` directory — the same ones that you see if you visit the link <http://cs.ucsb.edu/~richert/cs32/misc/lab00/> If so, you are ready to move on to the next step. If you don't see those files, go back through the instructions and make sure you didn't miss a step. If you still have trouble, ask your TA and/or mentor for assistance.

Step 2: Learn how to learn about some basic Linux commands
----------------------------------------------------------

The `man` program can be used to find out details about commands,
programs, standard library functions, and anything else for which a man page has been created. You just used `mkdir` and `cd` without any options, so why not learn more about those commands right now. First type:

    man mkdir

With `man`, the space key moves to the next page, and `q` quits. Notice that `mkdir` is a utility (program) to create directories, and it has three options available:

-   `-m` to set the new directory's permission bits (mode),
-   `-p` to create any necessary intermediate parent directories on the path
-   `-v` to be "verbose" about it.

Try making a directory tree without specifying the -p option, for example:

    bash-4.2$ mkdir one/two/three
    mkdir: cannot create directory `one/two/three': No such file or directory

Oops. Let's try it again with -p, and also use the -v option to hear the details:

    bash-4.2$ mkdir -p -v one/two/three
    mkdir: created directory `one'
    mkdir: created directory `one/two'
    mkdir: created directory `one/two/three'

Aaah ... much better, and so informative!

Now learn some more about `cd` as follows:

    man cd

Uh oh ... it seems that `cd` is a built-in shell command, not a program, and it does not have its own man page. If you spacebar down a ways though, you will find a section that starts out as follows:

    cd [-L|-P] [dir]
           Change  the  current directory to dir. ...

That's all you really need to know in this case, which is a good thing since the rest of the text for this command is not very helpful (-L and -P both relate to symbolic links). Some built-in commands do have their own pages though, and so man is usually a good place to start looking for information. By the way, before going to Step 3, learn more about man as follows:

    man man

Step 3: Reviewing Makefiles
---------------------------

We are now going to create a Makefile.

In many previous labs in CS16 and CS24, you may have copied your Makefile from the instructors directory. However, for this lab, you are going to make it yourself from scratch. This is because now that you are in CS32, it is finally time, if you haven't yet, to learn **completely** how a Makefile works—every *single part of it*—and to be able to create, modify and debug your own Makefiles as needed.

### Step 3a: Specifying which C++ compiler to use

The first thing we should do is edit our Makefile using emacs or vim, or whatever text editor you prefer. For example:

-   `emacs Makefile`, OR
-   `vim Makefile`

On the first line of the file, put this, substituting your name (and that of your pair partner(s) if applicable, for YOUR NAME(S) HERE, as appropriate:

    # Makefile for lab00, YOUR NAME(S) HERE, CS32, F18

Then, leave a blank line, and add the following two lines shown here, so that you end up with this as the first four lines of your Makefile:

    # Makefile for lab00, YOUR NAME(S) HERE, CS32, F18

    CXX=clang++
    # CXX=g++

<div style="margin:5px; border: 8px inset #ccc; padding:3px; font-size:80%;">
What is a *toolchain*

A *toolchain* refers to a set of tools that you use in some programming environment to get your work done. It typically includes a compiler, but may also include:

-   an editor
-   a linker for creating executables
-   a tool for creating libraries (combining compiled code from multiple
    files into a single file)
-   when compiling on one system and running on another (e.g. development for the Arduino, Android, iPhone, etc.), a tool to transfer the compiled software to the target device.
-   a debugger
-   a profiler (tool to help find where your program is spending most of its cpu time ("hotspots"), or to find memory leaks).

Both GNU and LLVM provide toolchains for working with C++ on Unix. The iOS products (iPhone/iPad/iPod) have their own toolchain, as do platforms such as Android and Arduino.

</div>
There are at least four important concepts about Makefiles to take away here:

1.  The pound sign (`#`) is used to start a comment in a Makefile. That comment extends from the pound sign to the end of the line.
2.  Anytime you have `VARIABLE_NAME=value` in a Makefile, you are defining a variable.
3.  The variable `CXX` is special—it is the variable that by default, indicates which compiler should be used for compiling C++ programs.
4.  There are two commonly used C++ compilers that you should be aware of: g++ (the C++ compiler from the GNU *toolchain*) and clang++ (the C++ compiler that is part of the LLVM *toolchain*). For more information on what a toolchain is, see the discussion at the right hand side of the page.

So what these lines of code do is this:

| Makefile code | Explanation |
| -- | -- |
|  `# Makefile for lab00...`   | comment documenting what the Makefile is for |
| `CXX=clang++`                | The clang++ compiler will be used to compile C++ programs |
|  `# CXX=g++`                 | If you want to switch to the g++ compiler for some reason, you can uncomment this line and comment out the `CXX=clang++` line. |

### Step 3b: Add a rule to link a helloWorld program

In the step of this lab where you copied files into your directory, one
of the files you copied in was a simple HelloWorld.cpp program. Take a
moment to look at the source code of that program, using the Unix `more`
command:

    -bash-4.2$ more helloWorld.cpp

The only reason this simple program is here is so we can practice
setting up a rule in the Makefile, from scratch, to compile a simple
program. Here is what that rule will look like. Add it below the lines
we already have, as shown here.

Two important things:

-   Note that the first of the two lines that we are adding MUST start
    in the leftmost column.
-   The second of the two lines MUST start with a TAB character, NOT
    spaces.
-   Because of the TAB vs. Spaces thing, copying and pasting this WILL
    NOT WORK. At the very least, if you copy and paste, you need to
    delete the spaces in front of `${CXX}` and replace them with a
    single TAB character.

<!-- -->

    # Makefile for lab00, YOUR NAME(S) HERE, CS32, F18

    CXX=clang++
    # CXX=g++

    helloWorld: helloWorld.o
            ${CXX} helloWorld.o -o helloWorld

What do these two lines mean?

-   The first part of the first line, `helloWorld: helloWorld.o` defines
    the start of a <em>target</em>. The part that comes before the
    colon, `helloWorld` is the name of the target, and is a file that we
    want to <b>make</b>. We make this file by typing <b>make
    helloWorld</b> at the Unix command line. The file `helloWorld` is
    going to be our executable program.
-   The second part of the second line, the part <em>after</em> the
    colon, `helloWorld.o`, indicates a list of files that the target
    depends on. In this case, the executable program `helloWorld`
    depends only on the file `helloWorld.o`.
-   `${CXX}` is replace with the name of the C++ compiler (either
    clang++ or gnu++) by dereferencing the symbol `CXX`. We call this
    <em>dereferencing</em> because like the `*` operator used with
    pointers in C/C++, the `$` in a Makefile indicates that instead of
    using the letters `CXX`, the Makefile should use <em>what they refer
    to</em>, i.e. the value of the variable `CXX`.
-   The command `${CXX} helloWorld.o -o helloWorld` therefore turns into
    either `clang++ helloWorld.o -o helloWorld` or
    `g++ helloWorld.o -o helloWorld` depending on the value of the
    symbol `${CXX}`,

### Step 3c: Adding a rule to compile helloWorld.cpp to helloWorld.o

Now it turns out that helloWorld.o is a file we do not have in our
directory at the moment. The following rule is one that will create
that, so add this to our Makefile next. Remember that you need to use a
TAB character on the indented lines, not spaces; so copying and pasting
this WILL NOT WORK.

Leave a blank line after your rule for the `helloWorld` target, and add
these two lines to your Makefile:

    helloWorld.o: helloWorld.cpp
            ${CXX} -c helloWorld.cpp

Now we are ready to test this all out. That's what we'll do in the next
step.

### Step 3d: Testing our Makefile so far

To test what we have so far:

\(1) Save your Makefile, and return to the Unix prompt.

\(2) At the Unix prompt, type `make helloWorld` and you should see output
like the following:

    -bash-4.2$ make helloWorld
    clang++ -c helloWorld.cpp
    clang++ helloWorld.o -o helloWorld
    -bash-4.2$ 

\(3) You can now run the helloWorld program by typing `./helloWorld` as
we have done all along throughout CS16 and CS24. Try that now:

    -bash-4.2$ ./helloWorld
    Hello, World!
    -bash-4.2$ 

\(4) Now, if type `make helloWorld` again, we should see the following
output. Do that now. Notice it is different from before:

    -bash-4.2$ make helloWorld
    make: `helloWorld' is up to date.
    -bash-4.2$ 

\(5) Now, edit your helloWorld.cpp program, changing the program by
adding a comment with your name(s) between the first two comments:

    // helloWorld.cpp  R. Wang for UCSB CS32 F18
    // Edited by: YOUR NAME(S) HERE
    // minimal Hello World! program for testing Makefiles

Save the change.

\(6) Although this change doesn't really affect the program, it is enough
for the Make utility to see that the file has been changed. If we now
type `make helloWorld` again, we'll see that the program is recompiled:

    -bash-4.2$ make helloWorld
    clang++ -c helloWorld.cpp
    clang++ helloWorld.o -o helloWorld
    -bash-4.2$ 

\(7) <b>Here is what you need to understand, both to work with make, and
for your <em>exams</em> in this course:</b>

-   The make utility works from timestamps and dependencies to figure
    out what does—or does not—need to be relinked and/or compiled.

So, based on the rules:

    helloWorld: helloWorld.o
            ${CXX} helloWorld.o -o helloWorld

    helloWorld.o: helloWorld.cpp
            ${CXX} -c helloWorld.cpp

We have this chain of dependencies:
`helloWorld.cpp`→`helloWorld.o`→`helloWorld`.

-   Here, I'm showing an arrow pointing in the direction in which make
    needs to make the files.
-   For example, if the makefile has `b: a` it means b depends on a, and
    we write a→b to show that we need a's timestamp to be earlier than
    b's timestamp. If a has a later timestamp than b, it means that b is
    "out of date" and needs to be remade.
-   Another case is the case where if b does not exist at all (e.g. if
    if has never been made at all, or if has been deleted since it was
    last made.) In that case, we also need to remake b, typically using
    a as the input file.

After constructing the dependencies, the make program then looks to see
which files already exist (or not), and what the time stamps are, and
executes the necessary commands in the order needed.

That is why the result, when we make a change to helloWorld.cpp is that
the rules are done in this order:

| what we see |                            explanation |
| -- | -- |
|`-bash-4.2$ make helloWorld` |           we type `make helloWorld` to make the executable, and make constructs the dependency chain `helloWorld.cpp`→`helloWorld.o`→`helloWorld` |
| `clang++ -c helloWorld.cpp`  |          From the dependency chain, this is the first thing that must be done. It must be done because helloWorld.cpp is "newer" than helloWorld.o. The command recompiles `helloWorld.cpp` into `helloWorld.o`—the `-c` flag indicates "compile only; do not link", so we get a helloWorld.o file as the result. |
| `clang++ helloWorld.o -o helloWorld`  | This is the link step. It is done because NOW helloWorld.o, which is newly remade from the previous step, is NOW newer than the executable helloWorld. The command relinks the helloWorld.o code (the machine language version of ONLY the code from the helloWorld.cpp file) with the machine language versions of the code in the standard libaries (e.g. the code for the iostream library that provides cout, endl, among other things.) The result of this command is a new version of the executable file `helloWorld` |
 | `-bash-4.2$`                 |          The bash prompt indicates that the command is complete and the shell is ready for our next command.|

So what should you know from this for your exams? These items suggest
a few of things you might be asked about.

-   Be able to explain the difference between Makefile commands that
    compile, vs. commands that link.
-   From this step of this lab, be able to write the syntax of Makefiles
    commands for compiling and/or linking a simple standalong C++
    program. (Later we'll also learn how to write Makefiles for complex
    program consisting of multiple source files.)
-   Be able to explain how Makefiles construct a chain of dependencies
    based on timestamps to determine what needs to be recompiled or
    relinked.
-   Be able to explain the variables such as `CXX` are dereferenced when
    the `$` is put in front of them, and they are surrounded by braces.

### Step 3e: Adding a rule for `make clean`

Sometimes we may want to remove all of the executable and .o files from
our directory. As you may recall from Makefiles that were supplied to
you in CS16 and CS24, that is traditionally done with a `clean` target
that allows us to type `make clean`.

Here are some examples of when that is appropriate:

-   When we are switching from one compiler to another, e.g. from
    clang++ to g++—the .o files produced by one compiler are not
    compatible with the other.
-   When we have made signficant changes to the interface between
    multiple parts of a program that uses separate compilation, i.e.
    multiple .cpp files (and hence .o files). By "interface", here we
    typically mean the .h files that specify definitions of structs,
    classes, and function prototypes. If those have changed, a "make
    clean" may be a good idea.
-   If we are about to copy the files to another directory (e.g. to
    share with a pair partner), or if we are finished with a project and
    want to save disk space. We really only need the source files (.h,
    .cpp and Makefile). The .o and executable files can always be remade
    if/when they are needed.

A clean rule looks like this, and is typically at or near the end of
your Makefile. Add this to your Makefile now. Note that the second line
starts with a tab, and that there should be a blank line after your
rule.

    clean: 
            /bin/rm -f *.o helloWorld

`make clean` <b>almost</b> always runs the `clean` rule. In general, any
Makefile target with no files specified after the colon is always run
when it is invoked. Technically, there is one exception: when there is a
file that has exactly the same name as the rule in the file. So it is
best to avoid having any executable or other file with the exact name
`clean`. In such a case, the `make clean` rule would <em>never</em> be
invoked. That's what we call a <em>corner case</em>—it rarely happens in
practice, but is possible in theory, so its good to keep in mind.)

The fact that this rule has `clean:` as the first line with
<em>nothing</em> after the colon (`:`) means that `clean` does not
depend on anything. That has a special meaning in a Makefile—it means
that <em>every</em> time we invoke `make clean`, the commands following
the first line of the rule will <em>always</em> be executed. (Well,
almost always. See the note at right for an exception.)

So `make clean` always results in the command
`/bin/rm -f *.o helloWorld` being executed, which removes all .o files
(the `*` being a <em>wildcard</em> that matches any filename.

Why`/bin/rm -f` rather than just `rm`?

-   `/bin/rm` specifies exactly what version of the rm program (the Unix
    delete program) to use. This is generally safer, in case someone has
    redefined `rm` to do something different than we might expect.
-   The `-f` option stands for <em>force</em> and says "do this even if
    there is a problem". A problem might be, for example, that there
    aren't any .o files or helloWorld files to remove. Without the `-f`
    option, the `/bin/rm` command might given an error message. With
    that option, it just works and doesn't complain.

### Step 3f: Testing the `make clean` rule

    -bash-4.2$ make clean
    /bin/rm -f *.o helloWorld
    -bash-4.2$ make helloWorld
    clang++ -c helloWorld.cpp
    clang++ helloWorld.o -o helloWorld
    -bash-4.2$ make helloWorld
    make: `helloWorld' is up to date.
    -bash-4.2$ 

Now let's test it out. Run `make clean`, then run `make helloWorld`
twice.

Your output should look like what you see at right.

-   You will see that when we type `make clean`, the
    `/bin/rm -f *.o helloWorld` command is executed.
-   When we type `make helloWorld` the <em>first</em> time, the commands
    to compile and link are executed.
-   When we type `make helloWorld` the <em>second</em> time, we get a
    message that `` `helloWorld' is up to date. ``. This is because make
    examined the whole dependency chain
    (`helloWorld.cpp`→`helloWorld.o`→`helloWorld`), and found that
    nothing needed to be done—all of the files needed were present, and
    all the timestamps were in the correct sequence.

Be able to predict how typing `make clean` will affect what happens when
make commands are invoked, and be able to explain why.

Step 4: Adding rules to support separate compilation
----------------------------------------------------

Now that we have practiced a bit on some simple Makefile rules for a
"Hello, World!" progam, we are ready to put in some Makefile rules for
something a bit more complex. In this weeks program, we are working with
some code that is basically review from CS16, but will set us up for
some of the advanced material we'll be covering in CS32. This code deals
with simple arrays in C++, finding min and max, and differentiating
between index and value. So, nothing too complicated.

The code is in the following source files:

```
+-----------------------+-----------------------+-----------------------+
| Filename              | Purpose               | Do I need             |
|                       |                       | to modify             |
|                       |                       | this file?            |
+=======================+=======================+=======================+
|                       | Function definitions  | YES                   |
|                       | for five functions.   |                       |
|   arrayFuncs.cpp      | Two are complete,     |                       |
|                       | three are stubs       |                       |
|                       | Your job in this      |                       |
|                       | lab is to replace the |                       |
|                       | stubs with working    |                       |
|                       | code                  |                       |
+-----------------------+-----------------------+-----------------------+
|                       | function prototypes   | NO                    |
|    arrayFuncs.h       | for five functions    |                       |
|                       | defined in            |                       |
|                       | arrayFuncs.cpp        |                       |
+-----------------------+-----------------------+-----------------------+
|                       | test cases for        | NO                    |
|                       | functions defined in  |                       |
|                       | arrayFuncs.cpp        |                       |
|    lab00Test.cpp      | This is the only      |                       |
|                       | file in this lab with |                       |
|                       | a main()              |                       |
|                       | function              |                       |
|                       | (other than           |                       |
|                       | helloWorld.cpp)       |                       |
+-----------------------+-----------------------+-----------------------+
|                       | definitions for       | NO                    |
|                       | functions that        |                       |
|     tddFuncs.cpp      | support test-driven   |                       |
|                       | development:          |                       |
|                       | assertEquals,         |                       |
|                       | assertTrue, etc.      |                       |
+-----------------------+-----------------------+-----------------------+
|                       | function prototypes   | NO                    |
|    tddFuncs.h         | for functions defined |                       |
|                       | in tddFuncs.cpp       |                       |
+-----------------------+-----------------------+-----------------------+
```

### Step 4a: Adding a rule to link lab00Test

The file lab00Test.cpp is the one with a main function in it. So that is
the one that we make an executable from.

We make an executable from it by linking its .o version together with
the .o versions of the other .cpp files. The first line of the rule
looks like this:

    lab00Test: lab00Test.o tddFuncs.o arrayFuncs.o

That says that the executable for lab00Test <em>depends on</em> the .o
files lab00Test.o, tddFuncs.o and arrayFuncs.o, which are in turn, the
compiled machine code versions of lab00Test.cpp, tddFuncs.cpp and
arrayFuncs.cpp.

The line that follows this one is the command to link these .o files
into the executable. Remember that the second line here MUST START WITH
A TAB, not with spaces. You CANNOT JUST COPY AND PASTE FROM THIS WEB
PAGE.

    lab00Test: lab00Test.o tddFuncs.o arrayFuncs.o
            ${CXX} lab00Test.o tddFuncs.o arrayFuncs.o -o lab00Test

Put that in your Makefile, and then try running `make lab00Test`

Now, you might think that we need to create a rule such as this one
next:

    lab00Test.o: lab00Test.cpp
            ${CXX} -c lab00Test.cpp 

That is what we would do to tell the make utility how to create
lab00Test.o from lab00Test.cpp, with the -c flag (compile only; don't
link). The output file is automatically named by removing the .cpp and
replacing it with .o. BUT WE DON'T HAVE TO DO THAT. (See the tip below
for an explanation as to why)

Instead, just try typing `make lab00Test` and it should work:

    -bash-4.2$ make lab00Test
    clang++    -c -o lab00Test.o lab00Test.cpp
    clang++    -c -o arrayFuncs.o arrayFuncs.cpp
    clang++    -c -o tddFuncs.o tddFuncs.cpp
    clang++ lab00Test.o arrayFuncs.o tddFuncs.o -o lab00Test
    -bash-4.2$ 

So read the tip now to understand why we didn't need those extra rules:

We can actually omit the rules for `lab00Test.o`, etc.

The reason we can omit this rule is that it follows the pattern of an
implicit rule that the Make utility already has in place. That default
rule looks like this—it is NOT important (at this point)
for you to fully understand all the symbols in this default rule—it is
only important that you understand the idea that it replaces the
specific rule for `helloWorld.o`. Later in the course, we will cover the
meaning of the various symbols (`%`, `$<`, `$@`).

    %.o : %.cpp
            $(CXX) -c $(CFLAGS) $(CPPFLAGS) $< -o $@

Implicit rules are explained more in this section of the [GNU Make
documentation](ftp://ftp.gnu.org/old-gnu/Manuals/make-3.79.1/html_chapter/make_toc.html#TOC93)

As it turns out, we didn't need the rule for helloWorld.o either. Try
commenting it out, and doing a `make clean`, then a `make helloWorld`
and you'll see that everything still works just fine. We typically DO
needs rules for the linking steps, because Make cannot guess which .o
files need to be linked together to create an executable. But we often
do NOT need the rules for compiling, if our compile is following the
normal naming conventions.

### Step 4b: Adjusting the clean rule

So now, we are <em>almost</em> ready to run our `./lab00Test` program
and start working on getting test cases to pass. BUT FIRST, we need to
adjust our make clean rule.

Here's how it looks now:

    clean: 
            /bin/rm -f *.o helloWorld

Here is how it needs to look instead:

    clean: 
            /bin/rm -f *.o helloWorld lab00Test

We need to add the lab00Test executable to the make clean rule. In a
future lab, we'll see how we can factor out parts of this to make
keeping a Makefile up to date less tedious.

Step 5: Make your the code in arrayFuncs.cpp pass its tests
-----------------------------------------------------------

Here you need to follow the instructions inside the file arrayFuncs.cpp
to replace the stubs with working code.

The instructions there should be self-explanatory, and the assignment
should be super easy—this is essentially review from CS16, laying a
foundation for a discussion of sorting algorithms.

We need to be sure we understand how to find the index of a minimum and
maximum element, and how to swap two elements in an array.

With those concepts down, we are ready (next week) to move on to both
selection sort and insertion sort.

When your code passes the tests, you are ready to try submitting it to
Gradescope.

Step 6: Checking your work before submitting
--------------------------------------------

When you are finished, you should be able to type `make clean` and then
`make lab00Test` then `./lab00Test` and see the following output:

``` {.bash}
-bash-4.2$ ./lab00Test
arrayToString(a,sizeA)={3,14,15,92,65,35,89}
PASSED: arrayToString(a,sizeA)
PASSED: indexOfMin(a,sizeA)
PASSED: indexOfMax(a,sizeA)
PASSED: arrayToString(a,sizeA); after swap(a,0,1)
PASSED: arrayToString(a,sizeA); after swap(a,0,2)
arrayToString(b,sizeB)={79,32,38,46}
PASSED: arrayToString(b,sizeB)
PASSED: indexOfMin(b,sizeB)
PASSED: indexOfMax(b,sizeB)
PASSED: arrayToString(b,sizeB); after swap(b,1,3)
PASSED: arrayToString(b,sizeB); after swap(b,0,2)
arrayToString(c,sizeC)={40,30,20,10}
PASSED: arrayToString(c,sizeC)
PASSED: indexOfMin(c,sizeC)
PASSED: indexOfMax(c,sizeC)
arrayToString(d,sizeD)={11,21,22,23}
PASSED: arrayToString(d,sizeD)
PASSED: indexOfMin(d,sizeD)
PASSED: indexOfMax(d,sizeD)
arrayToString(e,sizeE)={79,32,32,38,46}
PASSED: arrayToString(e,sizeE)
PASSED: indexOfMin(e,sizeE)
PASSED: indexOfMax(e,sizeE)
arrayToString(f,sizeF)={5,32,32,31,6,4,4}
PASSED: arrayToString(f,sizeF)
PASSED: indexOfMin(f,sizeF)
PASSED: indexOfMax(f,sizeF)
arrayToString(g,sizeG)={32,32,38,46,46,4,4}
PASSED: arrayToString(g,sizeG)
PASSED: indexOfMin(g,sizeG)
PASSED: indexOfMax(g,sizeG)
-bash-4.2$
```

At that point, you are ready to try submitting to the Gradescope system.

### An important word about academic honesty

We will test your code against other data files too—not just these. So
while you might be able to pass the tests on Gradescope now by just doing
a hard-coded "cout" of the expected output, that will NOT receive
credit.

To be very clear, code like this will pass on Gradescope, BUT REPRESENTS
A FORM OF ACADEMIC DISHONESTY since it is an attempt to just "game the
system", i.e. to get the tests to pass without really solving the
problem.

I would hope this would be obvious, but I have to say it so that there
is no ambiguity: hard coding your output is a form of cheating, i.e. a
form of "academic dishonesty". Submitting a program of this kind would
be subject not only to a reduced grade, but to possible disciplinary
penalties. If there is <em>any</em> doubt about this fact, please ask
your TA and/or your instructor for clarification.

Step 7: Submitting via Gradescope
--------------------------------

The lab assignment "Lab00" should appear in your Gradescope dashboard in CMPSC 32. If you haven't submitted anything for this assignment yet, Gradescope will prompt you to upload your files.

For this lab, you will need to upload your modified files (i.e. **`Makefile`** and **`arrayFuncs.cpp`**). You either can navigate to your file(s), "drag-and-drop" them into the "Submit Programming Assignment" window, or even use a GitHub repo to submit your work.

If you already submitted something on Gradescope, it will take you to their "Autograder Results" page. There is a "Resubmit" button on the bottom right that will allow you to update the files for your submission.

For this lab, if everything is correct, you'll see a successful submission passing all of the autograder tests.

**Remember to add your partner to Groups Members for this submission on Gradescope if applicable. At this point, if you worked in a pair, it is a good idea for both partners to log into Gradescope and see if you can see the uploaded files for Lab00.**


Grading Rubric
==============

This lab is based entirely on the grade assigned by Gradescope. There
WILL be labs this quarter where code style is assessed, but this is not
one of those labs.

Gradescope automated
-------------------

-   (80 pts) lab00Test passed Gradescope tests
-   (20 pts) helloWorld passed Gradescope tests

Acknowledgements
================

Some material in this lab is based on work originally written by Mike
Costanzo and edited by Phill Conrad, and Richert Wang (F18). Other parts are original work of Phill Conrad.
