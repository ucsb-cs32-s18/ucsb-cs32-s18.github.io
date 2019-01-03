---
num: "Lecture 16"
desc: "Heaps cont."
ready: true
date: 2018-06-05 12:30:00.00-7:00
---

```
// main.cpp
#include <unistd.h>
#include <iostream>

using namespace std;

class HeapEmptyException {};

class MaxHeap {
private:
	int* heapArray;
	int size;
	const static int CAPACITY = 100;
	void heapify(int index);
public:
	MaxHeap();
	int removeMax() throw (HeapEmptyException);
	void insert(int e);
	int getSize() { return size; }
	void printHeap();
};

void MaxHeap::heapify(int index) {
	int leftChild = 2 * index;
	int rightChild = 2 * index + 1;
	int largestIndex = index;
	
	if (leftChild <= size && 
    heapArray[leftChild] > heapArray[largestIndex]) {
		largestIndex = leftChild;
	}
	if (rightChild <= size &&
    heapArray[rightChild] > heapArray[largestIndex]) {
		largestIndex = rightChild;
	}
	if (largestIndex != index) {
		int temp = heapArray[index];
		heapArray[index] = heapArray[largestIndex];
		heapArray[largestIndex] = temp;
		heapify(largestIndex);
	}
}

MaxHeap::MaxHeap() {
	size = 0;
	heapArray = new int[CAPACITY];
}

void MaxHeap::insert(int e) {
	size++;
	heapArray[size] = e;
	int temp;
	int index = size;
	while (index > 1 && heapArray[index / 2] < heapArray[index]) {
		// swap parent and current node
		temp = heapArray[index];
		heapArray[index] = heapArray[index / 2];
		heapArray[index / 2] = temp;
		index = index / 2;
	}
}
int MaxHeap::removeMax() throw (HeapEmptyException) {
	if (size <= 0)
		throw HeapEmptyException();
	
	if (size == 1) {
		size--;
		return heapArray[1];
	}

	int index = 1;
	int max = heapArray[index];
	heapArray[index] = heapArray[size];
	size--;

	heapify(index);
	return max;
}

void MaxHeap::printHeap() {
	for (int i = 1; i <= size; i++) {
		cout << "i = " << i << ": " << heapArray[i] << endl;
	}
}

int main() {
	MaxHeap heap;
	heap.insert(3);
	heap.insert(2);
	heap.insert(1);
	heap.insert(15);
	heap.insert(5);
	heap.insert(4);
	heap.insert(45);
	cout << "---" << endl;
	heap.printHeap();
	cout << "---" << endl;

	cout << heap.getSize() << endl;
	cout << "---" << endl;

	int times = heap.getSize();
	for (int i = 0; i < times; i++) {
		cout << heap.removeMax() << endl;
	}
}
```
