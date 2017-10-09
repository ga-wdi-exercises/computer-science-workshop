# Computer Science Fundamentals

## Learning Objectives
* Define what an algorithm is
* Use asymptotic analysis to analyze the complexity of different algorithms.
* Understand basic data structures and why they are useful.

## Framing

> "Computer science is a discipline that involves the understanding and design of computers and computational processes. In its most general form it is concerned with the understanding of information transfer and transformation. Particular interest is placed on making processes efficient and endowing them with some form of intelligence. The discipline ranges from theoretical studies of algorithms to practical problems of implementation in terms of computational hardware and software."

> ([Source](https://www.cs.mtu.edu/~john/whatiscs.html))

Computer Science fields include but are not limited to...
- Algorithms
- Data structures
- Mathematical logic
- Networking
- Computer Architecture
- Theory (Coding, Game, Graph)
- Artificial intelligence

> [This Wikipedia article](https://en.wikipedia.org/wiki/Outline_of_computer_science#Subfields) has a nice summary of CS subfields.

Many think of computer science as a necessary prerequisite to do anything programming-related with a computer and *really know what you are doing*, or that knowing a certain amount of computer science is some kind of litmus test for a *true programmer*. This attitude perhaps unnecessarily mystifies an already difficult subject and field of study and, at worst, makes the learning curve seem so steep that it is like a learning barrier.

What do you already know about computer science?

Decades ago, it was absolutely necessary to have an understanding of computer science to do anything with a computer. In the beginning of consumer computing, home computers were essentially electronics projects for enthusiasts and hardcore hobbyists. The types of things you could do with a computer were very limited, and of interest to people with specific interests. Computers have come a long way since then, and are equipped with operating systems that attempt to make it as easy as possible for anyone to use a computer.

Something similar is true for programming, namely that not knowing any computer science is no longer a barrier to entry.

### How Can We Use Computer Science?

**Computer science provides methods and concepts for evaluating what we are doing as programmers.** At the very least, understanding some computer science can simply deepen our appreciation for our discipline and our craft. Not everyone who programs all of sudden thinks inherently, or has to think, like the stereotype of an engineer might think.

What does computer science have to do with modern web development? Not much, on the surface. As application developers, we can do our job well by following best practices, guided by our experience. It probably will not be often that you are interested in the time-complexity of a method you write.

Complexity and data structures are something **engineers** worry about, not developers, right?

Well, no. While it is true that we don't usually care much about optimization,
there are a few reasons why developers should care a bit about classic topics in
introductory computer science (CS).

1. Classic problems allow us to practice our problem solving skills; in fact, most of our lesson today can be completed without coding.
2.  Being familiar with the tradeoffs inherent in choosing an algorithm or a data structure have direct parallels in choices you make writing your application code.
3. Some of our colleagues will have CS degrees, and being able to understand the jargon and figures of speech they use helps us communicate with them. Perhaps most importantly, these colleagues will probably have some say in hiring you, since they're your prospective team. Nearly every technical interview touches on these topics.

### What is an algorithm?

Take 10 minutes and read [this](https://www.economist.com/blogs/economist-explains/2017/08/economist-explains-24) article. Write an issue on this repository with a definition in your own words of what an algorithm is.

> An algorithm is, essentially, a brainless way of doing clever things. It is a set of precise steps that need no great mental effort to follow but which, if obeyed exactly and mechanically, will lead to some desirable outcome.

from [here](https://www.economist.com/blogs/economist-explains/2017/08/economist-explains-24).


### What makes a good algorithm?

When we work with small inputs, like we have for the most part in this class, using an efficient algorithm to solve a problem is not crucial. Instead, it is more important to have clean code, good interfaces, and bug-less applications. However, once we are working with huge inputs our code will get a lot slower. At that point, building efficient algorithms becomes really important. 

When we write code, one of our main goals is to make that code execute fast. If our code is slow, our sites will load slowly and users may leave. We also want to use as little memory as possible when we execute our code so that it is less expensive to host our sites.

## Sorting Algorithms

One of the best examples of where we can use more efficient algorithms than the "brute force" or most obvious solution is when we sort arrays. 

The immediate thought is probably to find the smallest item in the array and move it down the array in order. That brute force solution is called an insertion sort. It's pretty inefficient -- we will have to traverse the array a bunch of times to always find the minimum. 

### Bubble Sort

The bubble sort algorithm goes like this: pass through the array a bunch of times, and each time if one element is higher than its neighbor, swap them. [Here](https://www.toptal.com/developers/sorting-algorithms/) is a visualisation of that.

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

This is probably one of the more obvious ways to sort an array -- we are just passing through it and swapping elements. This doesn't really scale well -- think about how many times you would have to pass through a really unsorted array!


## Quicksort

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
Quick sort is a more efficient algorithm for sorting an array. But why is that?

> Aside: writing sorting algorithms is important for understanding the "behind the scenes" of a programming language, but each one we have used in this class has a `.sort()` method built in. Ruby's uses a [merge sort](https://en.wikipedia.org/wiki/Merge_sort), Python uses a [tim sort](https://en.wikipedia.org/wiki/Timsort), and JavaScript uses [quick sort](https://stackoverflow.com/questions/234683/javascript-array-sort-implementation) -- but this depends on the browser. In practice, you should use these since they are highly optimised, though many companies like you to know some sorting algorithms (usually have two on hand). 


## Running Time and Big-O Analysis

We can look at a program and say -- "Oh that took two seconds to run". But that two seconds is dependant on a lot of things. That two seconds is for a very specific input. If we make the input 100 items instead of 10, what happens? Also, that two seconds is on a certain computer with a certain version of your programming language. Instead, we should generalize the algorithm's complexity.

We do so using a notation that mathematicians and computer scientists use, called Big-O notation.


* Learn how to optimize code both in terms of memory and runtime.
* 

## Computers
https://imgur.com/XuGhPgC

### Binary
https://i.redd.it/gk7dicv6hsvy.jpg
https://i.redd.it/x5ehl617qofz.jpg

### Pointers

#### Passing by Reference

## Big O Notation

## Data Structures

### Arrays
Arrays are the most basic data structure. For an array, the user must declare its size upfront (though most modern languages handle this behind the scenes) since arrays are stored in adjacent blocks of memory. If you were able to change its size then there would be no guarantee that there would be more memory to use in that block of memory. 
* Arrays hold values referenced by index, so accessing items is very quick. 
* Strings are arrays of characters, tuples are immutable arrays, and Python lists are dynamically resized arrays.
* Each cell in an array uses the same number of bytes, so usually the array will actually just store a pointer to the actual object rather than storing it within the contiguous block of memory.
* ```address = start + (cellsize * index)```


|Operation|Complexity|
|---------|----------|
|Access   |O(1)      |
|Search   |O(n)      |
|Insert   |O(n)      |
|Delete   |O(n)      | 


### Maps/Dictionaries/Hashes/Objects
Hash tables are often very efficient data structures. They store data using a computed index. The function that computes the index is called a hashing function. Each item in the hash table has a key and value, rather than storing data by index. The biggest difficulty with hashing is collisions, which happen when the hashing function computes the same index for multiple values. There are many ways around this, including creating a new key or using arrays to store the values at that index.

* Dictionaries in Python are an implementation of a hash table.

|Operation|Complexity|
|---------|----------|
|Access   |O(1)->O(n)|
|Search   |O(1)->O(n)|
|Insert   |O(1)->O(n)|
|Delete   |O(1)->O(n)| 

The complexities of each of the above operations depend on the hashing function used.


### Linked Lists
Linked lists are graph data structures that consist of nodes and pointers. There can be doubly or singly linked lists. Singly linked lists have nodes that store the value of the node and a pointer to the next node. Doubly linked lists additionally store a pointer to the previous node as well.

* The first item is called the head and the rest of the list is called the tail.
* Insertion and deletion is relatively simple since the nodes do not need to be stored adjacently in memory.
* Indexing and accessing elements is pretty slow since you must traverse the list to do so.

|Operation|Complexity|
|---------|----------|
|Access   |O(n)      |
|Search   |O(n)      |
|Insert   |O(1)      |
|Delete   |O(1)      | 

### Queues / Stacks
A stack is a data structure that operates in a last in first out nature. Newer items are at the top of the stack and will be accessed first whereas older items are near the bottom and will be accessed last. A back button is a good example of an implementation of a stack. Common methods include:
* Push - add an item to the top of the stack.
* Pop - remove the top item from the stack.
* Peek - check to see the top item of the stack.

```python 
class Stack:
	
	def __init__(self):
		self.data = []

	def push(self, item):
		self.data.append(item)

	def pop(self):
		return self.data.pop()

	def peek(self):
		return self.data[-1]
```

A queue is a data structure that operates on a first in first out basis, similar to a line for a movie. These are often used for breadth-first searching where nodes are stored in order for processing. These are usually implemented using either a singly linked list or an array. Common methods include:

* Enqueue: add an item to the queue
* Dequeue: remove item from the queue
* Peek: return the next item in the queue

```python 
class Queue:

	def __init__(self):
		self.data = []

	def enqueue(self, item):
		self.data.insert(0, item)

	def dequeue(self):
		return self.data.pop()

	def peek(self):
		return self.data[-1]
```


### Sets

### Graphs
Graphs are non-linear data structures that do not necessarily follow a numerical order. Graphs are similar to trees but with essentially no rules. A tree is a graph, but most graphs are not trees. 

```
     A –→ B ←–––– C → D ↔ E
     ↑    ↕     ↙ ↑     ↘
     F –→ G → H ← I ––––→ J
           ↓     ↘ ↑
           K       L
```
Image from [itsy-bitsy-data-structures](https://github.com/thejameskyle/itsy-bitsy-data-structures/blob/master/itsy-bitsy-data-structures.js).

Graphs have nodes (also called vertices) and edges. The node holds the data and then the edges point to related nodes. There are two types of edges: directed and undirected. Directed edges point in a direction whereas undirected edges point both ways. 

* Good examples of graphs are Facebook friends, Twitter following (which would be directed), or a map of Metro stops.

* There are many ways to store a graph data structure. You can use pointers and nodes, or you could use an adjacency list or matrix.

* A degree is how many edges a given vertex has. 

* An Euler path visits each edge just once. A graph must have either zero or two vertices with an odd degree to have an euler path. 

* A cycle is a circle mad of edges.

* Both edges and nodes can be weighted.
* The top node in a tree is called the root.

Visual representation of a tree
```
          A                     
        ↙   ↘              
      B       C                
    ↙  ↘
   D    E
```

### Heaps

Heaps are inverted tree-like data structures. They are a set of interconnected nodes that store data in a particular order. The function that determines ordering is called the heap property. Each child node must have a parent with a higher priority according to that heap property. 

|Operation|Complexity|
|---------|----------|
|Access   |N/A       |
|Search   |O(n)      |
|Insert   |O(1)      |
|Delete   |O(log(n)) | 

### Trees

Trees are graph data structures that are hierarchical and unidirectional. That means that certain nodes that are above others in the tree. Nodes at the same level cannot point to one another. 


#### Binary Search Trees

Binary search trees are a special form of where each left child of a node has a lower value than its parent and each right child has a greater value than its parent. There cannot be any duplicate values in the tree. These are very efficient for searching. 

|Operation|Complexity|
|---------|----------|
|Access   |O(log n)  |
|Search   |O(log n)  |
|Insert   |O(log n)  |
|Delete   |O(log n)  | 

## Algorithms

### Sorting

### Searching

### Recursion
https://i.redd.it/f4pua0fm4ysy.gif

#### Divide and Conquer
Divide and conquer is "an algorithm design paradigm that is based on multi-branch recursion. It takes a larger problem and breaks it into 2+ sub-problems" ([Wikipedia](https://en.wikipedia.org/wiki/Divide_and_conquer_algorithm)). [Merge soring](https://github.com/aspittel/coding_cheat_sheets/blob/master/sorting/mergesort.md) and some fibonacci algorithms are implementations of the divide and conquer algorithm. These are especially useful on multi-processor systems.

##### Code Example
```ruby
def multiply_range n, m
	if n == m
		return m
	elsif m < n
		return 1
	else
		return multiply_range(n, (m+n)/2) * multiply_range((n+m)/2 + 1, m)
    end
end
```

Additional resources: 

* https://www.youtube.com/watch?v=JPyuH4qXLZ0