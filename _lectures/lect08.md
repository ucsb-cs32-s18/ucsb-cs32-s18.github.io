---
num: "Lecture 8"
desc: "Quicksort and Mergesort"
ready: true
date: 2018-05-01 12:30:00.00-7:00
---

# Divide and conquer
* Subdivide a larger problem into smaller parts
* Solve each smaller part
* Combine solutions of smaller sub problems back into the larger problem
* We see this pattern in recursive problems where they can be subdivided

# Divide and conquer sorting algorithms
* We’ve talked about quadratic sorting algorithms
	* Bubble sort, selection sort, insertion sort
		* Runs in O(n<sup>2</sup>)
	*Better sorting algorithms exist
		* Can improve our run time to O(nlogn) in the worst case.

# Mergesort
* Idea:
	* Break an array into sub arrays where size = 1.
	* Merge each small sub array together to form sorted larger array.
	* Apply technique to the entire array.
	* Sorting is done “bottom-up”

# Merge sort algorithm
```
// algorithm from DS textbook
void merge(int a[], size_t leftArraySize, size_t rightArraySize) {

	// Note: we are assuming the left and right sub arrays are sorted

	int* tempArray;		// tempArray to hold sorted elements
	size_t copied = 0; 	// num elements copied to tempArray
	size_t leftCopied = 0;	// num elements copied from leftArray
	size_t rightCopied = 0;	// num elements copied from rightArray

	// create temp array
	tempArray = new int[leftArraySize + rightArraySize];

	// merge left and right arrays into temp in sorted order
	while ((leftCopied < leftArraySize) && (rightCopied < rightArraySize)) {
		if (a[leftCopied] < (a + leftArraySize)[rightCopied]) {
			tempArray[copied++] = a[leftCopied++];
		} else {
			tempArray[copied++] = (a + leftArraySize)[rightCopied++];
		}
	}

	// copy remaining elements from left/right sub arrays into tempArray

	// if elements in leftArray still exist, then ...
	while (leftCopied < leftArraySize) {
		tempArray[copied++] = a[leftCopied++];
	}


	// if elements in rightArray still exist, then ...
	while (rightCopied < rightArraySize) {
		tempArray[copied++] = (a + leftArraySize)[rightCopied++];
	}

	// Replace the sorted values into the original array
	for (int i = 0; i < leftArraySize + rightArraySize; i++) {
		a[i] = tempArray[i];
	}

	// free up memory
	delete [] tempArray;
}


void mergesort(int a[], size_t size) {
	size_t leftArraySize;
	size_t rightArraySize;

	if (size > 1) {
		leftArraySize = size / 2;
		rightArraySize = size - leftArraySize;

		// call mergesort on left array
		mergesort(a, leftArraySize); 
		
		// call mergesort on right array
		mergesort((a + leftArraySize), rightArraySize);

		// left and right sorted arrays together
		merge(a, leftArraySize, rightArraySize);
	}
}

void printArray(const int a[], size_t size) {
	cout << "Printing Array" << endl;
	for (int i = 0; i < size; i++) {
		cout << "a[" << i << "] = " << a[i] << endl;
	}
}

int main() {
	int a[] = {0,1,2,3,4,5,6,7,8,9};
	int b[] = {9,8,7,6,5,4,3,2,1,0};
	int c[] = {0,9,1,8,2,7,3,6,4,5};
	int d[] = {5,4,6,3,7,2,8,1,9,0};

	mergesort(a, 10);
	printArray(a, 10);
	cout << "----" << endl;
	mergesort(b, 10);
	printArray(b, 10);
	cout << "----" << endl;
	mergesort(c, 10);
	printArray(c, 10);
	cout << "----" << endl;
	mergesort(d, 10);
	printArray(d, 10);
	cout << "----" << endl;
}
```

# Mergesort Analysis

* Best-case: O(nlogn)
* Average-case: O(nlogn)
* Worst-case: O(nlogn)
* Requires O(n) additional space to merge the unsorted arrays into a sorted array
	* Time / space tradeoff

# Quicksort
* Idea:
	* Can subdivide array based on a “pivot” value.
		* Place elements < pivot to the right-side of the array
	* Place elements >= pivot to the left-side of the array
		* Repeat for each left / right portion of the array
	* When sub array sizes = 1, then entire array is sorted
	* Sorting is done “top-down”

# Quicksort Algorithm
```
void partition(int a[], size_t size, size_t& pivotIndex) {
	int pivot = a[0];		 // choose 1st value for pivot
	size_t left = 1;		 // index just right of pivot
	size_t right = size - 1; // last item in array
	int temp;

	while (left <= right) {
		// increment left if <= pivot
		while (left < size && a[left] <= pivot) {
			left++;
		}

		// decrement right if > pivot
		while (a[right] > pivot) {
			right--;
		}

		// swap left and right if left < right
		if (left < right) {
			temp = a[left];
			a[left] = a[right];
			a[right] = temp;
		}
	}

	// swap pivot with a[right]
	pivotIndex = right;
	temp = a[0];
	a[0] = a[pivotIndex];
	a[pivotIndex] = temp;
}

void quicksort(int a[], size_t size) {
	size_t pivotIndex;		// index of pivot
	size_t leftSize;		// num elements left of pivot
	size_t rightSize;		// num elements right of pivot

	if (size > 1) {
		// partition a[] based on pivotIndex
		partition(a, size, pivotIndex);

		// Compute the sizes of left and right sub arrays
		leftSize = pivotIndex;
		rightSize = size - leftSize - 1;

		// recursive call sorting the left array
		quicksort(a, leftSize);

		// recursive call sorting the right array
		quicksort((a + pivotIndex + 1), rightSize);
	}
}

int main() {
	int a[] = {0,1,2,3,4,5,6,7,8,9};
	int b[] = {9,8,7,6,5,4,3,2,1,0};
	int c[] = {0,9,1,8,2,7,3,6,4,5};
	int d[] = {5,4,6,3,7,2,8,1,9,0};
	quicksort(a, 10);
	printArray(a, 10);
	cout << "----" << endl;
	quicksort(b, 10);
	printArray(b, 10);
	cout << "----" << endl;
	quicksort(c, 10);
	printArray(c, 10);
	cout << "----" << endl;
	quicksort(d, 10);
	printArray(d, 10);
	cout << "----" << endl;
	return 0;
}
```

# Quicksort Analysis

* Best-case: O(nlogn)
* Average-case: O(nlogn)
* Worst-case: O(n<sup>2</sup>)
	* Quicksort performs poorly depending on the pivot value chosen.
		* Run this algorithm with an array already in sorted order.
	* If the pivot is the least or greatest value in the array, then the sub arrays aren't evenly divided.
	* An optimization to try and prevent this scenario is to select a few pivot values in the array randomly and selecting the medium of these.
* Unlike (our version of) Mergesort, Quicksort does not require additional buffer space and can sort the array in-place.

