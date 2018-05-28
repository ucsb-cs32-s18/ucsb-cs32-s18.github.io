---
layout: lab
num: lab08
ready: true
desc: "Polymorphism"
assigned: 2018-05-30 08:00:00.00-7
due: 2018-06-03 23:59:00.00-7
---

# Goals

* This lab will cover implementing classes that support polymorphism with a base class and sub classes.
* You will need to implement the `.cpp` and `.h` files to enable polymorphism correctly.

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

<tt>~richert/public_html/cs32/misc/lab08/*</tt>

and also accessible via the URL

<http://cs.ucsb.edu/~richert/cs32/misc/lab08/>

You want to copy these files into your <tt>~/cs32/{{page.num}}</tt> directory.

## Step 2: Understanding the starter code and inheritance hierarchy

The purpose of this lab is to write classes and subclasses representing an ice cream item orders that can be sold in an ice cream shop. There are many ways ice cream can be sold, and we will implement a specific way according to the description below:

* An ice cream order can consist of many ice cream items.
* An ice cream item can either be `small`, `medium`, or `large`. These sizes are represented as `string` types and used when constructing the ice cream items (see `IceCreamItem.h`).
* There are two types of ice cream items that may be purchased and added to an ice cream order:

## `CustomItem` inherits from `IceCreamItem`
* In addition to the functions inherited from `IceCreamItem.h`, you will need to implement the following specifically for a `CustomItem`:
* `CustomItem(std::string size);`
	* Constructs a custom ice cream order with a size. The only sizes an `IceCreamItem` may have are: `small`, `medium`, and `large`.
	* Each size will have a base price for the order (without the addition of toppings). A `small` size is $3.00, a `medium` size is $5.00, and a `large` size is $6.50.
* `virtual ~CustomItem();`
	* A virtual deconstructor in case you have to deallocate any memory on the heap.
* `void addTopping(std::string topping);`
	* A method that allows you to add a topping to the custom ice cream order.
	* Toppings are not predefined and can be identified with strings. You may assume any topping added to a `CustomItem` has a weight of 1 oz. Each oz. increases the price of the `CustomItem` by $0.40 cents.
	* You may add the same topping (i.e. represented as the same string) as many times you want, with each topping addition being 1 oz. Your implementation will need to keep track of the number of ounces for each topping and display the correct number of ounces when constructing a string in `composeItem`.

## `PreMadeItem` inherits from `IceCreamItem`
* In addition to the functions inherited from `IceCreamItem.h`, you will need to implement the following specifically for a `PreMadeItem`:
* `PreMadeItem(std::string name, std::string size);`
	* Constructs a pre-made ice cream order with a size. The only sizes any `IceCreamItem` may have are `small`, `medium`, and `large`.
	* Each `PreMadeItem` also consists of a name (represented as a string) used when composing the details for this item.
	* Each size will have a base price for the order (without the addition of toppings). A `small` size is $4.00, a `medium` size is $6.00, and a `large` size is $7.50.
	* Since a `PreMadeItem` already has the necessary toppings built in, there is no need to add toppings such as in the `CustomItem`.
* `virtual ~PreMadeItem();`
	* A virtual deconstructor in case you have to deallocate any memory on the heap.

## Step 3: Implement the files to pass your tests.
* The provided starter code will test your implementation by constructing orders of various ice cream items. This will make sure your price calculations, toppings, names, etc. are correct. You must implement the following files according to the specifications above:
	* `IceCreamItem.cpp`, `CustomItem.h`, `CustomItem.cpp`, `PreMadeItem.h`, `PreMadeItem.cpp`

* Since you will need to provide a `composeItem()` implementation for each subclass, there is a certain format that a `CustomItem` and `PreMadeItem` must compose the details of the item into a string that `composeItem()` returns. Some notes:
	* Your price must be displayed in a traditional dollar amount with a precision of two decimal places.
	* For a `CustomItem`, your toppings must be displayed in lexicographical order. How you do this is up to you, but I recommend using a `<map>` since the keys are inherently sorted. The keys can be stored as strings representing the topping names, and the values are the number of ounces of that topping (i.e. number of times `addTopping()` was called for that specific topping).

An example of a `CustomItem` that is a large size, contains one addition of an "oreo" topping, 2 additions of "peanut" topping, and a price of $7.70.

```
Custom Size: large
Toppings:
oreos: 1 oz
peanuts: 2 oz
Price: $7.70
```

An example of a `PreMadeItem` that is a medium size, the item name is "Banana Slamma", and has a price of $6.00.

```
Pre-made Size: medium
Pre-made Item: Banana Slamma
Price: $6.00
```

## Step 4: Testing

The following executables will be generated by typing `make all`:

* `testIceCreamOrder1`
* `testIceCreamOrder2`
* `testIceCreamOrder3`
* `testIceCreamOrder4`

You can test each executable separately by executing each individual binary file or you can run all tests by typing `make tests`.

## Step 5: Submitting via Gradescope

You will turn in `IceCreamItem.cpp`, `CustomItem.h`, `CustomItem.cpp`, `PreMadeItem.h`, and `PreMadeItem.cpp` for this lab.

The lab assignment "Lab08" should appear in your Gradescope dashboard in CMPSC 32. If you haven't submitted anything for this assignment yet, Gradescope will prompt you to upload your files.

For this lab, you will need to upload your modified files (i.e. `IceCreamItem.cpp`, `CustomItem.h`, `CustomItem.cpp`, `PreMadeItem.h`, and `PreMadeItem.cpp`). You either can navigate to your file, "drag-and-drop" them into the "Submit Programming Assignment" window, or even use a GitHub repo to submit your work.

If you already submitted something on Gradescope, it will take you to their "Autograder Results" page. There is a "Resubmit" button on the bottom right that will allow you to update the files for your submission.

For this lab, if everything is correct, you'll see a successful submission passing all of the autograder tests.

**Remember to add your partner to Groups Members for this submission on Gradescope if applicable. At this point, if you worked in a pair, it is a good idea for both partners to log into Gradescope and check if you can see the uploaded files for Lab08.**

