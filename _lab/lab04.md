---
layout: lab
num: lab04
ready: true
desc: "Hash Tables"
assigned: 2018-05-02 08:00:00.00-7
due: 2018-05-06 23:59:00.00-7
---

# Goals

By the end of this lab, you will be able to:
* Write your own hash table implementation
	* Both the interface (.h) and its implementation (.cpp)
* Write a sorting algorithm in O(nlogn)

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

<tt>~richert/public_html/cs32/misc/lab04/*</tt>

and also accessible via the URL

<http://cs.ucsb.edu/~richert/cs32/misc/lab04/>

You want to copy these files into your <tt>~/cs32/{{page.num}}</tt> directory.

## Step 2: Write the table.h header file

Write <font color="red"><b>table.h</b></font> to define <code>class Table</code> as it is used in the demonstration program named <code>tabledemo.cpp</code>. Your Table must hold <code>Entry</code> objects as defined in <code>entry.h</code> (and implemented in <code>entry.cpp</code>). For the demonstration program to compile successfully, your table.h must define at least the following public functions:

<ul type = "circle">
  <li style='margin-bottom:2em;'>One constructor that builds an empty Table designed to hold a maximum number of entries equal to the only parameter. This parameter should have a default value of 100:
  <br><code>&nbsp;&nbsp;&nbsp;Table(unsigned int max_entries = 100)</code></li>

  <li style='margin-bottom:2em;'>Another constructor that builds a Table designed to hold the number of entries
  specified by the first parameter, and puts that many entries into the Table by reading
  them one at a time from the input stream that is the second parameter:
  <br><code>&nbsp;&nbsp;&nbsp;Table(unsigned int entries, std::istream&amp; input)</code>
  <br><em>Do not input more than the specified number of entries.</em> If you always read all of input, you will lose points for not satisfying this requirement.</li>

  <li style='margin-bottom:2em;'>Two (overloaded) member functions named put, each of which puts a new Entry into the Table:
  <br><code>&nbsp;&nbsp;&nbsp;void put(unsigned int key, std::string data)</code>
  <br><code>&nbsp;&nbsp;&nbsp;void put(Entry e)</code>
  <br>The first of these functions creates a new Entry to put in the Table. The second
  one puts a copy of the parameter in the Table. In cases where the Table already
  contains an Entry with the given key, these functions act to update the Entry for that key.
  The Table is not allowed to contain duplicate keys.</li>

  <li style='margin-bottom:2em;'>A constant member function named get that returns the string associated with the
  parameter:
  <br><code>&nbsp;&nbsp;&nbsp;std::string get(unsigned int key) const</code>
  <br>This function returns an empty string if the Table has no Entry with the given key.</li>

  <li style='margin-bottom:2em;'>A member function named remove that removes the Entry containing the given key:
  <br><code>&nbsp;&nbsp;&nbsp;bool remove(unsigned int key)</code>
  <br>This function returns true if it removes an Entry, or false if the Table has no such Entry.</li>

  <li>A non-member output function that overloads the &lt;&lt; operator to print the Table:
  <br><code>&nbsp;&nbsp;&nbsp;std::ostream&amp; operator&lt;&lt; (std::ostream&amp; out, const Table&amp; t)</code>
  <br>This function is expected to print each Entry in the Table to a separate line of
  the given output stream <em>in the order of their key values</em>.</li>
</ul>
   
Your class may define other functions too, either public or private ones. In particular, you will probably want to add a hashing function to transform the key values - in our version, function hashkey is a private function. And of course, your class must define the private data a Table object stores.

HINT: You will want to use chained hashing for this lab. That means that each row in your <code>Table</code> will be of type <code>std::vector&lt;Entry&gt;</code>. It is often convenient to typedef that type to some shorter name, so your method signatures don't get clunky.

## Step 3: Write the Table class to implement the header from Step 2

Write <font color="red"><b>table.cpp</b></font> to implement your class Table. You may use tools from any of the standard libraries <b>except</b> &lt;map&gt;, &lt;set&gt;, &lt unordered_map&gt; and &lt;unordered_set&gt;. 

Hint: write stub code for each method, and get your class to compile. Then filling in the methods is a SMOP (Simple Matter of Programming).

In planning your implementations, keep in mind the following requirements:
<ul type="circle">
  <li>Each of the functions put, get and remove must execute in constant O(1) time. That means your implementation must be a hash table. By the way, you should carefully choose the size of the table you create in the constructors - our version makes the size of the table equal to twice the maximum number of entries.</li>
  <li>Your output function must output the entries in the order of the key values, and it must execute in no more than O(n log n) time, and certainly not O(n<sup>2</sup>) time.</li></ul>
      
<table border="1">
 <tr align="left">
   <td><b>Clarification about Big-O restrictions:</b>
   <br>It is important that you store and manipulate Entry objects (i.e., instances of class Entry), and not separately handle the integer keys and string data. That is because we assess the efficiency of your functions by using the Entry::access_count() function before and after various operations. The time tests used by Gradescope will fail if they detect impossibly small counts of Entry accesses. Do notice that sorting Entry objects is no more complicated than sorting numbers, thanks to the operator conversion function that allows an Entry object to be treated like an int when appropriate. So, for example, if e1 and e2 are both entry objects, then (e1 &lt; e2) will evaluate to true if e1.key() is less than e2.key(). All of the other relational operators work too! The power of overloading.</td>
 </tr>
</table>
   
## Step 4: Testing
   
Compile and test your program at CSIL. Create your own testing program(s) to do so. After you think that all parts are working properly, you should verify that your implementation compiles and executes correctly with the demonstration program too. Use the following command to compile it:

<pre>g++ -std=c++11 -o tabledemo tabledemo.cpp table.cpp entry.cpp</pre>

The demonstration also requires a copy of the file <code>fips.txt</code>(Federal Information Processing Standard codes for all U.S. counties) to reside in your current working directory. (This file is provided along with the other ones.) 
      
## Step 5: Submitting via Gradescope
  
  You will turn in both <code>table.h</code> and <code>table.cpp</code>.

The lab assignment "Lab04" should appear in your Gradescope dashboard in CMPSC 32. If you haven't submitted anything for this assignment yet, Gradescope will prompt you to upload your files.

For this lab, you will need to upload your modified files (i.e. `table.h` and `table.cpp`). You either can navigate to your file, "drag-and-drop" them into the "Submit Programming Assignment" window, or even use a GitHub repo to submit your work.

If you already submitted something on Gradescope, it will take you to their "Autograder Results" page. There is a "Resubmit" button on the bottom right that will allow you to update the files for your submission.

For this lab, if everything is correct, you'll see a successful submission passing all of the autograder tests.

**Remember to add your partner to Groups Members for this submission on Gradescope if applicable. At this point, if you worked in a pair, it is a good idea for both partners to log into Gradescope and check if you can see the uploaded files for Lab04.**