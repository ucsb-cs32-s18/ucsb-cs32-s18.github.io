---
num: "Lecture 5"
desc: "Binary Search, Quadratic-time Sorting"
ready: true
date: 2018-04-17 12:30:00.00-7:00
---

# Binary Search

* A common search algorithm that applies to a sorted sequence of values that can be compared.
* We check the “middle” of the sequence and…
	* If the target is < the middle element, we know it must be in the lower-half of the sequence IF it exists.
	* If the target is > the middle element, we know if must be in the upper-half of the sequence IF it exists.
	* If the target is the middle element, then it exists and we’re done.

## Analysis
* Binary search is O(log n) execution time.
	* Scales well the larger n (# of elements gets).
	* Each iteration cuts the search space in half
		* Only look at either bottom or top half.
	* This works well BECAUSE of the sorted property
		* If items were unsorted, we would have to compare each element in the collection in the worst case scenario: (O(n)).

## Recursive Binary Search (from Book)
```
void search(const int a[], size_t first, size_t size,
		int target, bool &found, size_t &location) {
	
	size_t middle;
	// base case
	if (size == 0) {
		found = false;
	} else {
		middle = first + size/2;

		// found the target
		if (target == a[middle]) {
			location = middle;
			found = true;
		} else if (target < a[middle]) {
			// recurse lower-half
			search(a, first, middle, target, found, location);
		} else {
			// recurse upper-half
			search(a, middle + 1, (size - 1)/2, target, found, location);
		}
	}
}

------------
int main() {

	int a[] = {1,2,3,4,5,6,7,8,9,10};
	bool exists = false;
	size_t location;

	search(a, 0, 10, 3, exists, location);
	cout << "3 exists: " << exists << endl;
	cout << "index of 3: " << location << endl;

	cout << "----" << endl;

	search(a, 0, 10, 11, exists, location);
	cout << "11 exists: " << exists << endl;
	cout << "index of 11: " << location << endl;

	cout << "----" << endl;
	search(a, 0, 10, 9, exists, location);
	cout << "9 exists: " << exists << endl;
	cout << "index of 9: " << location << endl;

	return 0;
}
```
# Sorting
* Sorting algorithms are useful in order to optimize certain functionality (such as using binary search, checking for duplicates, ...)

* There are MANY sorting algorithms in existence (even inefficient ones such as [Bogosort](https://en.wikipedia.org/wiki/Bogosort)).

## Quadratic-time sorting algorithms
* Sorting algorithms in O(n<sup>2</sup>) are known as quadratic time algorithms.
* We'll cover three quadratic sorting algorithms:
	* Bubbles sort, Insertion sort, and Selection sort

## Bubble Sort
* Bubble sort compares adjacent items in the array and swaps them if a[i] > a[i+1].
	* This guarantees that the largest (or smallest depending on the direction the bubble is moving the item) will be in the proper place.
		* This needs to be done for each element in the collection.
		* O(n<sup>2</sup>) complexity.
		* A good illustration of how Bubble sort works is shown [here](https://en.wikipedia.org/wiki/Bubble_sort).
* Can be slightly optimized
	* If a swap doesn't occur in an iteration, we know the array is already sorted and no more comparisons need to be made.

## Example
```
void bubbleSort(int a[], size_t size) {
	int temp;
	bool swapped;

	for (int i = size - 1; i > 0; i--) {
		swapped = false;
		for (int j = 0; j < i; j++) {
			if (a[j] > a[j + 1]) {
				// swap
				temp = a[j];
				a[j] = a[j+1];
				a[j+1] = temp;
				swapped = true;
			}
		}
		if (!swapped) {
			// in order
			cout << "i = " << i << endl;
			cout << "already in order... returning" << endl;
			return;
		}
	}
}
-------
void printArray(const int a[], size_t size) {
	for (int i = 0; i < size; i++) {
		cout << "[" << i << "] = " << a[i] << endl;
	}
}
-------
int main() {
	int a[] = {1,2,3,4,5,6,7,8,9,10};
	int b[] = {1,10,2,9,3,8,4,7,5,6};
	int c[] = {2,9,4,7,6,5,8,3,10,1};
	int d[] = {10,9,8,7,6,5,4,3,2,1};
	int e[] = {1};

	bubbleSort(a, 10);
	printArray(a,10);
	cout << "---" << endl;
	bubbleSort(b, 10);
	printArray(b,10);
	cout << "---" << endl;
	bubbleSort(c,10);
	printArray(c,10);
	cout << "---" << endl;
	bubbleSort(d,10);
	printArray(d,10);
	cout << "---" << endl;
	bubbleSort(e,1);
	printArray(e,1);
------
```
## Selection Sort
* From top-down (or bottom-up), look through the array and find the largest (or smallest) element.
* Swap a[i] with a[index_of_largest_value]
* O(n<sup>2</sup>) complexity.
* A good illustration of how Selection Sort works is shown [here](https://en.wikipedia.org/wiki/Selection_sort).

```
void selectionSort(int a[], size_t size) {
	int temp;
	int largestIndex;
	int largest;
	for (int i = size - 1; i > 0; i--) {
		largestIndex = 0;
		largest = a[0];
		for (int j = 1; j <= i; j++) {
			if (a[j] > largest) {
				largest = a[j];
				largestIndex = j;
			}
		}
		temp = a[i];
		a[i] = a[largestIndex];
		a[largestIndex] = temp;
	}
}
-------
int main() {
	int a[] = {1,2,3,4,5,6,7,8,9,10};
	int b[] = {1,10,2,9,3,8,4,7,5,6};
	int c[] = {2,9,4,7,6,5,8,3,10,1};
	int d[] = {10,9,8,7,6,5,4,3,2,1};
	int e[] = {1};

	selectionSort(a, 10);
	printArray(a,10);
	cout << "---" << endl;
	selectionSort(b, 10);
	printArray(b,10);
	cout << "---" << endl;
	selectionSort(c,10);
	printArray(c,10);
	cout << "---" << endl;
	selectionSort(d,10);
	printArray(d,10);
	cout << "---" << endl;
	selectionSort(e,1);
	printArray(e,1);
------
```
## Insertion Sort
* Similar to sorting cards in a poker hand
* For each item in the array, find where it should "belong" and insert the item in its proper place.
	* Before insertion happens, shift all elements in order to to make an empty slot where the item should belong.
	* Do this for each element, and by the end of the algorithm, all elements will be in their proper place.
	* O(n<sup>2</sup>) complexity.
	* O(n) complexity for elements that are mostly-sorted.

## Example
```
void insertionSort(int a[], size_t size) {

	int item;
	int shiftIndex;
	for (int i = 1; i < size; i++) {
		item = a[i];
		shiftIndex = i - 1;

		while (shiftIndex >= 0 && a[shiftIndex] > item) {
			a[shiftIndex + 1] = a[shiftIndex];
			shiftIndex -= 1;
		}
		a[shiftIndex + 1] = item;
	}	
}
-------
int main() {
	int a[] = {1,2,3,4,5,6,7,8,9,10};
	int b[] = {1,10,2,9,3,8,4,7,5,6};
	int c[] = {2,9,4,7,6,5,8,3,10,1};
	int d[] = {10,9,8,7,6,5,4,3,2,1};
	int e[] = {1};

	insertionSort(a, 10);
	printArray(a,10);
	cout << "---" << endl;
	insertionSort(b, 10);
	printArray(b,10);
	cout << "---" << endl;
	insertionSort(c,10);
	printArray(c,10);
	cout << "---" << endl;
	insertionSort(d,10);
	printArray(d,10);
	cout << "---" << endl;
	insertionSort(e,1);
	printArray(e,1);
------
```





