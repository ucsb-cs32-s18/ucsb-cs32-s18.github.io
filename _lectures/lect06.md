---
num: "Lecture 6"
desc: "Hashing"
ready: true
date: 2018-04-19 12:30:00.00-7:00
---

# Hashing
* The ability to address unique key values in an array whose size is smaller than the set of possible key values.
* Generally, keys are unique values that identify some record of information
	* In order to put data in the appropriate place in the collection, a hash function is required.
		* The hash function usually outputs a position in the collection based on the key value
		* Hash function outputs should be uniformly distributed
			* Or else all data would try to be stored in the same index.
		* For example, if you have array of 100 elements, a simple hash function could be:
			* key % 100 = [0-99]
* Hashing is very efficient for searching for data in an array.
	* Recall binary search: O(log n) search time (if elements are sorted).
	* Linear search: O(n) search time.
	* Hash Table search: O(1) average search time in unsorted order.
		* Hash Table searching provides instant access to an element in an array since the hash function computes the index where the data is stored.

## Collisions
* It's possible that two elements may be indexed to the same location.
	* This is known as collisions

## Open-address Hashing
* Collisions are resolved by placing the item in the next open spot in the array.
* For example, if a record is hashed to position i and data already exists in that index, then check the next available spot i+1, i+2, etc.
	* Known as linear probing
	* What is a problem with this mechanism?
		* Delayed Insertion – inserting an item in a crowded hash table takes time since it must look for an empty spot.
			* Elements are inserted farther away from their actual hashed index.
		* Clustering – When different keys are hashed to the same index, there may be groups of data records grouped in the same place.

## Double Hashing
* Technique that uses a 2nd hash function when resolving a collision.
	* If a hash function index results in a collision, then use the 2nd hash function to determine how far to step in the array to look for an empty slot.
	* Helps reduce the clustering effect.
* Problems
	* If hash2 function is large, there is a possibility that we will go out of bounds.
	* Depending on the table size and hash2, it is possible that the index won’t be uniformly distributed.

## Chained Hashing
* The biggest problem to open-address hashing is 
	* If the table is full, no more elements can be added.
	* Similar to a vector, it could expand the capacity “under-the-hood” when needed, but…
		* All elements will probably have to be rehashed
		* New capacity shouldn’t be wasteful (too big) or too small
* Chained hashing (chaining)
	* If a collision occurs, then we store a series of data records in a list that the index in the hash table references.
	* Linked Lists are a common collection to store collided data records

## std::map and std::unordered_map
* A map is another term for an associated container.
* std::map is implemented with a form of binary trees (red-black trees)
	* Useful if you care about the ordering of keys.
* std::unordered_map is implemented with hash tables
	* Better average case performance O(1), but data order is not guaranteed.
* Seem very similar, but “under-the-hood” is quite different.

## Example
```
#include <unordered_map>

using namespace std;

int main() {

	unordered_map<int, string> students; // hash table

	// Use bracket notation for creation
	students[0] = “Richert”;
	students[1] = “John Doe”;
	students[2] = “Jane Doe”;
	students[251] = "someone!";

	cout << “students[1] = “ << students[1] << endl;
	cout << "students[251] = " << students[251] << endl;
	cout << "students[101] = " << students[101] << endl;

	// Check if a student id exists using .find method
	if (students.find(1) != students.end()) {
		cout << "Found student id = 1, Name = " << students[1] << endl;
	} else {
		cout << "Can't find id = 1" << endl;
	}

	cout << "----" << endl;

	for (unordered_map<int, string>::iterator i = students.begin();
			i != students.end(); i++) {
		cout << i->first << " : " << i->second << endl;
	}
----
	// Use insertion method for adding an element in the dictionary
	//#include <utility> for std::pair

	students.insert(pair<int, string>(3, “Sleepy”));

	// Erasing by iterator
	unordered_map<int, string>::iterator p = students.find(2);
	students.erase(p); // erases “Jane Doe”

	// Erasing by key
	students.erase(0); // erases “Richert”

	// does not replace existing item
	students.insert(pair<int, string>(1, "Some other John Doe"));
	students[1] = "Some other John Doe"; // replaces existing item

	return 0;
}
```
