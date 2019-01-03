---
num: "Lecture 15"
desc: "Heaps"
ready: true
date: 2018-05-31 12:30:00.00-7:00
---

## Heaps

* Recall
	* Binary tree: A tree structure where a node has two children
	* Binary Search tree: A tree structure where a node has two children AND
		* The left child < parent
		* The right child > parent
		* Insertion order affects the tree structure

## A Heap is a <b>complete</b> binary tree
* Every level of the tree, except the deepest, must contain as many nodes as possible.
* The deepest level must have all nodes to the left as possible.

## MaxHeap
* The value of a node is never less than the value of its children.
* Every level of the tree, except the deepest, must contain as many nodes as possible. The deepest level must have all nodes to the left as possible.

## MinHeap
* Same as MaxHeap, EXCEPT
	* The value of a node is never greater than the value of its children.

## Examples
* MaxHeap

![MaxHeap](MaxHeap.png)

* MinHeap

![MinHeap](MinHeap.png)

## Heaps are an efficient way to implement a Priority Queue
* The only element we care about is the root (the min or max depending on MinHeap or MaxHeap).
* Insertion order should not affect the structure of the tree since operations need to preserve the complete balanced property.

## Heaps represented as an array
* Since binary heaps have the complete property, representing this with an array is simple. 
	* Easier to represent the heap where the 0th element in the array is meaningless.
	* The root of the binary heap is at index 1.
* A node’s index with respect to its parent and children can be generalized as:
	* A node’s parent index: index / 2 (integer division truncates decimal)
	* A node’s left child index: 2 * index
	* A node’s right child index: 2 * index + 1

* Example of an array representation of MaxHeap above

![Heap Array](HeapArray.png)

## Insertion into a binary MaxHeap
* insert the element in the first available location.
	* Keeps the binary tree complete.
* While the element’s parent is less than the element
	* Swap the element with its parent
* Insertion is O(log n) (height of tree is log n)

![Max Heap Insertion](MaxHeapInsertion.png)

* Note that MinHeap would be the same algorithm except we swap while the element’s parent is greater than the element.

## Removing root element of a MaxHeap
* Since heaps are used to implement priority queues, removing the root element is a commonly used operation.
* Copy the root element into a variable
* Assign the last_element to the root position
* While last_element is less than one of its children
	* Swap the largest child with the last_element
* Return the original root element

![Extract Root](ExtractRoot.png)

