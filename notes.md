## Framing

Computer science is a discipline that involves the understanding and design of computers and computational processes. In its most general form it is concerned with the understanding of information transfer and transformation.

Computer Science fields include but are not limited to...
- Algorithms
- Data structures
- Mathematical logic
- Networking
- Computer Architecture
- Theory (Coding, Game, Graph)
- Artificial intelligence

What do you already know about computer science?

* You all already know the contents of a CS 101 class 

* My school's stuff

* **Computer science provides methods and concepts for evaluating what we are doing as programmers.** At the very least, understanding some computer science can simply deepen our appreciation for our discipline and our craft. Not everyone who programs all of sudden thinks inherently, or has to think, like the stereotype of an engineer might think.

1. Classic problems allow us to practice our problem solving skills; in fact, most of our lesson today can be completed without coding.
2.  Being familiar with the tradeoffs inherent in choosing an algorithm or a data structure have direct parallels in choices you make writing your application code.
3. Some of our colleagues will have CS degrees, and being able to understand the jargon and figures of speech they use helps us communicate with them. Perhaps most importantly, these colleagues will probably have some say in hiring you, since they're your prospective team. Nearly every technical interview touches on these topics.

Nearly every technical interview touches on these topics.

### CFU
* Three reasons why we learn CS

## Algorithms
Take 10 minutes and read [this](https://www.economist.com/blogs/economist-explains/2017/08/economist-explains-24) article. Write an issue on this repository with a definition in your own words of what an algorithm is.

### What makes a good algorithm?

When we work with relatively small inputs, like we have for the most part in this class, using an efficient algorithm to solve a problem is not crucial. Instead, it is more important to have clean code, good interfaces, and bug-less applications. However, once we are working with huge inputs our code will get a lot slower. At that point, building efficient algorithms becomes really important.

## Run Time and Big-O Analysis

We can look at a program and say -- "Oh that took two seconds to run". But that two seconds is dependent on a lot of factor. That two seconds is for a very specific input. If we make the input 100 items instead of 10, what happens? Also, that two seconds is on a certain computer with a certain version of your programming language. Instead, we should generalize the algorithm's complexity.

so how do we do that? 

Big-O notation is not an exact metric for benchmarking algorithms. Rather, it gives us an abstract idea about how costly or efficient an algorithm is, with respect to how much computing power it takes. With Big-O notation, we are comparing orders of magnitude.

Compare similar algorithms. 

For time complexity, we want to count how many times the code is run in context of how large the input to the code is. For example, O(1) is a very efficient piece of code, O(N!) is very inefficient. Let's break this down into categories of Big-O.

### O (log n) and O(n log n) Complexity

O (log n) complexity refers to algorithms with significantly lower than n complexity. We don't actually have to calculate logarithms or anything like that! Technically, a logarithm is a "quantity representing the power to which a fixed number (the base) must be raised to produce a given number." So, the base 10 logarithm of 1000 is 3 since 10^3 is 1000 source](https://en.wikipedia.org/wiki/Logarithm). O (log n) complex algorithms 

One example of an O (log n) algorithm is a binary search. In a standard array, if we want to find the index of an item with a given value, we have to iterate through it and check if each item is equal to the item we are searching for. If we know that we have a **sorted** array, we can do this a lot easier! 

For the array `[1, 3, 5, 7, 9, 11, 13]`, if we want to find the index of the 5, we can do so like this:
* Find the item at the midpoint of the array. This ends up being `7`.
* Our item is below 7, so then, since our array is sorted, we only have to search the the half of the array before the 7.
* The midpoint of the sub array from 1-7 or `[1, 3, 5]` is `3`.
* This time, 5 is larger than 3, so we search the sub-array `[5]`. Since the midpoint of that array `5` is equal to the number we are searching for, we just return that number.

An implementation of that algorithm is below:
```javascript
function binarySearch(arr, item, first = 0, last = null) {
	if (!last) last = arr.length

	let midpoint = (last - first) / 2 + first

	if (arr[midpoint] === item) return midpoint
	if (arr[midpoint] > item) return binarySearch(arr, item, first, midpoint)
	if (arr[midpoint] < item) return binarySearch(arr, item, midpoint, last)
}
```

The above function ran 3 times instead of the 7 that we would need if we iterated through the entire array! This algorithm is super efficient -- even if we have a million items in our array, on average we will only need to execute the binary search 20 times.

O(n log n) algorithms are ones that are significantly faster than O(n^2) but slower than O(n). Let's come back to O(n log n) in a minute -- a lot of sorting algorithms fall under this category.

## Sorting Algorithms

One of the most important subsets of algorithms is sorting algorithms. A lot of the time, we will have a collection of items that we want to order in some way for our analyses or for display purposes. 
![](https://cdn-images-1.medium.com/max/600/1*i0fopl3fml48X4aAxpqM4A.jpeg)

There are **tons** of sorting algorithms with various pros and cons to them -- some are more efficient with some types of inputs and less with others. Again, having an efficient sorting algorithm isn't super important with a collection of ten items, but when there are a million or a billion efficiency becomes very important!

With different sorting algorithms, there are a couple things we need to keep in mind. The first is the time complexity - which we just went over. The second is whether or not they are **in place**. Some sorting algorithms can just re-order the collection, others need an additional data structure in order to work. 

### Bubble Sort

The bubble sort algorithm goes like this: pass through the array a bunch of times, and each time if one element is higher than its neighbor, swap them. [Here](https://www.toptal.com/developers/sorting-algorithms/) is a visualization of it.

```javascript
Array.prototype.swap = function (idxA, idxB) {
	let temp = this[idxA]
	this[idxA] = this[idxB]
	this[idxB] = temp
}

function bubbleSort (a) {
	let keepGoing = true

	while (keepGoing) {
		keepGoing = false
		for (let i=0; i < a.length - 1; i++) {
			if (a[i] > a[i+1]) {
				keepGoing = true
				a.swap(i, i+1)
			}
		}
	}
}
```

```js
let randomArray = (length, max) => [...new Array(length)].map(() => Math.round(Math.random() * max))

let a = randomArray(1000000, 1000000)
console.time("Quick Sort")
quickSort(a)
console.timeEnd("Quick Sort")
```

The bubble sort algorithm has an O(n^2) complexity. It works really well if an array is close to sorted -- in that case the algorithm could be closer to O (n log n), but in the case that an array is not close to sorted, it will be a lot less efficient.

### Quicksort

With the person next to you, describe what the below function is doing. [Hint](https://www.toptal.com/developers/sorting-algorithms/quick-sort).

```js
function quickSort (a) {
	if (a.length <= 1) return a

	let below = [], above = []

	let pivot = a.length - 1

	let pivotValue = a[pivot]

	a = a.slice(0, pivot).concat(a.slice(pivot + 1))

	for (let i = 0; i < a.length; i ++) {
		a[i] < pivotValue ? above.push(a[i]) : below.push(a[i])
	}
	
	return quickSort(above).concat([pivotValue], quickSort(below))
} 
```
Each partitioning operation takes O(n) operations (one pass on the array). In average, each partitioning divides the array to two parts (which sums up to log n operations). In total we have O(n * log n) operations.

I.e. in average log n partitioning operations and each partitioning takes O(n) operations.


```js
let randomArray = (length, max) => [...new Array(length)].map(() => Math.round(Math.random() * max))

let a = randomArray(1000000, 1000000)
console.time("Quick Sort")
quickSort(a)
console.timeEnd("Quick Sort")
```

## You Do: Researching Common Sorting Algorithms

In groups of two, research the following sorting algorithms:
* Selection sort
* Merge sort
* Radix sort
* Counting sort

You will be presenting your findings to the rest of the class! Make sure you include the benefits, drawbacks, complexity, and a code sample of your algorithm. If you want to send any materials for your presentation to me feel free to do so!

## Data Structures

Throughout this class, we've used some of the built-in data structures that our programming languages give us. Let's review what a data structure is: data structures define how a collection of data should be organized. We have used arrays, objects, hashes, and ranges in our code.  There are reasons why we choose one over the other -- if we want ordered data we use an array, if we want key value pairs we use an object. There are also other data structures out there. Some are built in to the programming language, some are not. 

These data structures are programming language agnostic -- they can be implemented in any language. Therefore, they fall into the category of "abstract data types" -- or theoretical data types described by their values and actions. For example, an integer is a whole number which can be added, subtracted, multiplied etc. These can be implemented across programming languages -- or even outside of programming. Data structures fall into this same category!

Similar to the sorting algorithms from before, we use different data structures for different reasons. Usually, they have some operation optimized -- like sorting, searching, adding or removing items, or iterating through them. Let's first start looking more in depth at the data structures we've seen in class and then look at some new ones!

## CFU 
* What are types of collections?
* Abstract data types?
* Example of abstract data type - in your own words and its implementation

### Arrays

Arrays are ordered data structures that allow us to access pieces of data at a given index.

Traditionally, arrays have a set size, so you can't add or remove data from them. This makes them really efficient because array items can be stored together in a block of memory on your computer. The indexes of the items are then calculated based on the address in memory that the item is located at.

The high level programming languages that we have seen in this class abstract away the memory allocation dynamic in arrays, so we can easily add and remove items from them. Most programming languages implement this process by allocating more memory than needed for an array at initialization and then resizing dynamically at certain indexes. In a lot of cases, arrays wil store a pointer to the item rather than the item itself in memory. This makes them less efficient from a computational perspective, but makes them much more programmer friendly!

|Operation|Complexity|
|---------|----------|
|Access   |O(1)      |
|Search   |O(n)      |
|Insert   |O(n)      |
|Delete   |O(n)      | 

* Accessing can be done using the formula start + (cellsize * index)
* Searching is done by iterating through the array and seeing if the value equals the item you are searching for.
* Insertion is done by recreating the array, which means that each item must be recreated.
* Deletion is done by recreating the array, which means that each item must be recreated.

## CFU
* how are arrays stored in memory?
* how do they differ between higher and lower level languages?
* What's a pointer?

### Hash Tables

Hash tables are another name for objects, hashes, maps, associative arrays, and dictionaries depending on the language. They store data in key value pairs. 

Hash tables allow us to easily insert, delete, search, and access data. 

|Operation|Complexity|
|---------|----------|
|Access   |O(1) -> O(n)|
|Search   |O(1) -> O(n)|
|Insert   |O(1) -> O(n)|
|Delete   |O(1) -> O(n)| 

The implementation details of hash tables are outside the scope of this class, but the efficiency of each of their operations is usually very close to O(1). [Here](https://github.com/aspittel/coding-cheat-sheets/blob/master/data_structures/hash_tables.md) and [here](https://github.com/SF-WDI-LABS/hash-map-lab) have more details on how hash tables are implemented if you are interested.

## CFU
* Other terms for hash tables
* Why hash tables?

### Linked Lists

Linked lists are linear collections of data that consist of nodes with data and pointers. Singly linked lists have nodes that store the value of the node and a pointer to the next node. Doubly linked lists additionally store a pointer to the previous node.

Linked lists do not need to be stored contiguously in memory like an array, so insertion and deletion is relatively simple. They do not natively support accessing one data node or indexing through operations. These operations are normally performed just by looping through the nodes. They use more memory than arrays since they store pointers to the next link(s).

```javascript
class Node {
	constructor (data, next = null) {
		this.data = data
		this.next = next
	}
}


class SinglyLinkedList {
	constructor () {
		this.head = null
		this.length = 0
	}

	insert (item) {
		this.head = new Node(item)
		this.length ++
	}

	search (item) {
		let idx = 0
		let node = self.head

		while (node) {
			if (node.data == data) return idx
			node = node.next
			idx += 1
		}

		return -1
	}
}
```

#### You Do: Implement Delete and Access
* Add methods to the `SinglyLinkedList` that allow you to delete a node and that allow you to access an item at a certain index.

```javascript
class Node {
	constructor (data, next = null, prev = null) {
		this.data = data
		this.next = next
		this.prev = prev
	}
}


class DoublyLinkedList {
	constructor () {
		this.head = null
		this.tail = null
		this.length = 0
	}

	insert (item) {
		new_node = new Node(item, null, self.head)
		
		if (!self.head) {
			self.head = new_node
		} else {
			self.tail.next = new_node
			new_node.prev = self.tail
		}

		self.tail = new_node
		this.length ++
	}

	search (item) {
		let idx = 0
		let node = self.head

		while (node) {
			if (node.data == data) return idx
			node = node.next
			idx += 1
		}

		return -1
	}
}
```

#### You Do: Implement Delete and Access
* Add methods to the `DoublyLinkedList` that allow you to traverse the doubly linked list backwards.

## CFU
* What are linked lists good for?
* What two attributes define a linked list?
* What is the difference between a singly and doubly linked list?

### Stacks

Stacks as a data structure are a lot like stacks as a physical structure. Think of stacks of dishes or books. Stacks operate in a last in first out nature. Newer items are at the top of the stack and will be accessed first whereas older items are near the bottom and will be accessed last. Back buttons, undo buttons, and the function call stack are common uses of stacks. Common methods include:
* Push - add an item to the top of the stack.
* Pop - remove the top item from the stack.
* Peek - check to see the top item of the stack.

![](https://camo.githubusercontent.com/6847160e586699a3fbd38eba5fef228440975c77/687474703a2f2f6c65676163792e6561726c68616d2e6564752f2537456c746e677579656e31342f63732532307765622f706963732f737461636b2e706e67)

Stacks are usually implemented either using a linked list or an array.

#### Linked List Implementation
```javascript
class Node {
	constructor (data, next = null) {
		this.data = data
		this.next = next
	}
}

class Stack {
	constructor () {
		this.head = null
	}

	push (data) {
		this.head = new Node(data, this.head)
	}

	pop () {
		let data = this.head.data
		this.head = this.head.next
		return data
	}

	peek () {
		return this.head.data
	}
}
```

|Operation|Complexity|
|---------|----------|
|Access   |O(1)      |
|Insert   |O(1)      |
|Delete   |O(1)      | 

Stacks are very efficient, but they are also limited in what we can do with them.

#### You Do: Implement a Stack Using an Array
Create a stack using an array. Make sure you have the methods push, pop, and peek!

### CFU
* What actions define a stack?
* how do we access items in a stack?
* What are stacks used for?


### Queues

A queue is a data structure that operates on a first in first out basis, similar to a line for a movie. These are often used for breadth-first searching where nodes are stored in order for processing. These are usually implemented using either a singly linked list or an array. Common methods include:

* Enqueue: add an item to the queue
* Dequeue: remove item from the queue
* Peek: return the next item in the queue

Software queues are used in a lot of cases like real life queues -- they give service to the task that asked for it first. A printer, for example, usually prints the first job given to it and then queues up the others until it is their turn. 

![](https://camo.githubusercontent.com/36f5620ed351f717bdce36d783f9261472f0634a/68747470733a2f2f75706c6f61642e77696b696d656469612e6f72672f77696b6970656469612f636f6d6d6f6e732f7468756d622f352f35322f446174615f51756575652e7376672f3230303070782d446174615f51756575652e7376672e706e67)

```javascript 
class Node {
	constructor (data, next = null, prev = null) {
		this.data = data
		this.next = next
		this.prev = prev
	}
}

class Queue {
	constructor () {
		this.head = null
		this.tail = null
	}

	enqueue (data) {
		let newNode = new Node (data, null, this.head)

		if (!this.head) {
			this.head = newNode
		} else {
			this.tail.next = newNode
			newNode.prev = self.tail
		}

		this.tail = newNode
	}

	dequeue (data) {
		let data = this.head.data
		this.head = this.head.next
		return data
	}

	peek () {
		return this.head.data
	}
}
```

|Operation|Complexity|
|---------|----------|
|Access   |O(1)      |
|Insert   |O(1)      |
|Delete   |O(1)      | 

#### You Do: Implement a Queue Using an Array
Create a queue using an array. Make sure you have the methods enqueue, dequeue, and peek!

## CFU 
* Why use a queue?
* What are they used for?
* Which operations define a queue?


### Graphs
In computer science, graphs are collections of **vertices** or **nodes**, which usually store or represent some data, and **edges**, which connect the nodes. Each edge connects two nodes together.  If you think of nodes as airports, edges would be the flight paths between them.  Here are some use cases for graphs:

* graph databases
* relationships among users in a social network
* links between pages on a website
* finding a route between two locations
* planning the order of classes to take based on prerequisites

The node holds the data and then the edges point to related nodes. There are two types of edges: directed and undirected. Directed edges point in a direction whereas undirected edges point both ways. 

There are many ways to store a graph data structure. You can use pointers and nodes, or you could use an adjacency list or matrix.

Creating a graph is very simple and we can do so in many ways. For example:
```javascript
class Node {
	constructor (data) {
		this.data = data
		this.edges = []
	}
}
```

Usually the most important action we can take with graphs is traversing their relationships. Breadth first and depth first searching

## CFU
* What are graphs used for?
* Example of a graph in the wild?


### Trees

Trees are graph data structures that are hierarchical and unidirectional. They have a root value, and then sub-trees of children that each have parents. They are represented as a series of linked nodes. Each node has a value and then pointers to its children.

The most common tree is a binary tree -- each node has at most two children.

|Operation|Complexity|
|---------|----------|
|Access   |O(log n)  |
|Search   |O(log n)  |
|Insert   |O(log n)  |
|Delete   |O(log n)  | 

Here are a few examples of trees in computing:

* **the DOM tree**
* The file system, where directories contain other directories and/or files. The `/` directory is called the "root" directory because it's the root of the computer's directory tree. Use the command `tree` to view the tree structure of any given directory. (You may need to install this capability with `brew install tree`)
* comment trees (where users can comment on comments)
* data compression algorithm trees (Huffman coding)
* single-elimination tournaments
* parser trees or syntax trees that help a computer interpret human-readable code
* the way calculators compute order of operations * indexes in databases usually utilize trees.

Usually, trees are extended so that they have more features than just two branches. Some common trees include AVL trees, red-black trees, splay trees, tries, Radix trees, ternary search trees, B trees, and B+ trees. Potentially the most used ones, though, are binary search trees.

## CFU
* Why use trees?
* what does a tree look like?
* Why do trees have their complexity?

Binary search trees or BSTs are special types of trees that add extra restrictions to them.
In each node's left child subtree (if it has one), all nodes will will have keys less than the original node's key. In each node's right child subtree (if it has one), all nodes must have a greater key than the original node itself (or equal). Left is less!

![](https://upload.wikimedia.org/wikipedia/commons/thumb/d/da/Binary_search_tree.svg/1200px-Binary_search_tree.svg.png)

```javascript
class Node {
	constructor (value, right = null, left = null) {
		this.value = value
		this.right = right
		this.left = left
	}
}


class BST {
	constructor () {
		this.root = null
	}

	insert (value) {
		let node = new Node(value)

		if (!this.root) {
			this.root = node
		} else {
			let currentNode = this.root

			while (currentNode) {
				if (currentNode.value > value) {
					if (currentNode.left) {
						currentNode = currentNode.left
					} else {
						currentNode.left = node
						return
					}
				} else {
					if (currentNode.right) {
						currentNode = currentNode.right
					} else {
						currentNode.right = node
						return
					}
				}
			}
		}
	}
}
```
#### You Do: Add getMinimum method to BST
Add a method that retrieves the minimum value in a Binary Search Tree.

#### CFU
* What defines a BST?
* Why do we use them?
* What are they used for?