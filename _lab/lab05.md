---
layout: lab
num: lab05
ready: true
desc: "Hash Tables cont."
assigned: 2018-05-09 08:00:00.00-7
due: 2018-05-13 23:59:00.00-7
---

# Goals

This is a <em>continuation</em> of the previous lab. You will add the "Big Three" member functions (copy constructor, assigment operator, and destructor) to your <code>Table</code> class. You will need a slightly revised <code>Entry</code> class, which counts the number of <code>Entry</code> objects that are created and destroyed, so we can test your destructor.

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

In this step, we are going to copy the {{page.num}} starter files from the instructors directory into your <tt>~/cs32/{{page.num}}</tt> directory.

The files are in the instructors directory at 

<tt>~richert/public_html/cs32/misc/lab05/*</tt>

and also accessible via the URL

<http://cs.ucsb.edu/~richert/cs32/misc/lab05/>

You want to copy these files into your <tt>~/cs32/{{page.num}}</tt> directory.

## Step 2: Update your Table's header file

* Add the <em>declarations</em> (not the definitions) to `table.h`.

* Both your copy constructor and assignment  operator must take a constant reference to a <code>Table</code> object as the only parameter.
  
* Your assignment operator must return the calling object as a reference.

## Step 3: Update your Tables implementation file

* Add the <em>definitions</em> (not the declarations) to  <code>table.cpp</code>. You may use tools from any of the standard libraries except `<map>`, `<set>`, `<unordered_map>` and `<unordered_set>`.
    
* Both the copy constructor and the assignment operator must make completely independent copies of the source `Table`. In other words, if `Table x` is a copy of `Table y`, then future changes to `x` will not affect `y`, and vice-versa.
    
* Your destructor must release all memory allocated via the operator <code>new</code> or calls to `malloc()`.

* If your get, remove or output functions did not pass the time tests for Lab04, then you should improve them now.

## Step 4: Testing

Compile and test your program at CSIL (by connecting remotely is okay). Create your own testing program(s) to do so. After you think that all parts are working properly, you should verify that your implementation compiles and executes correctly with the demonstration program from the previous lab.

## Step 5: Submitting via Gradescope
  
You will turn in both `table.h` and `table.cpp`.

The lab assignment "Lab05" should appear in your Gradescope dashboard in CMPSC 32. If you haven't submitted anything for this assignment yet, Gradescope will prompt you to upload your files.

For this lab, you will need to upload your modified files (i.e. `table.h` and `table.cpp`). You either can navigate to your file, "drag-and-drop" them into the "Submit Programming Assignment" window, or even use a GitHub repo to submit your work.

If you already submitted something on Gradescope, it will take you to their "Autograder Results" page. There is a "Resubmit" button on the bottom right that will allow you to update the files for your submission.

For this lab, if everything is correct, you'll see a successful submission passing all of the autograder tests.

**Remember to add your partner to Groups Members for this submission on Gradescope if applicable. At this point, if you worked in a pair, it is a good idea for both partners to log into Gradescope and check if you can see the uploaded files for Lab05.**

