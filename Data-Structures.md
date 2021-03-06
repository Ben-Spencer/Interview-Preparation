<h1>Data Structures</h1>
<h1>Preface</h1>
<h1>Table of Contents</h1>
<h2>Definition</h2>
<ul><li>Data structures optimze data access and modification by efficiently organizing, managing, and storing data.</li></ul>
<h2>Why Learn Data Structures?</h2>
<ul>
	<li>To improve the computational complexity of algorithms. Computational complexity is the amount of time and space required to execute an algorithm. By improving the computational complexity, data structures can yield faster runtime and less memory usage for users.</li>
	<li>They are part of the main topic of technical interviews, for large software companies.</li>
</ul>
<h2>Types of Data Structures</h2>
<ul>
	<li>Primitive</li>
	<li>Non-Primitive</li>
		<ul>
			<li>Linear</li>
			<li>Non-Linear</li>
		</ul>
</ul>
<h1>Primitive Data Structures</h1>
<h1>Non-Primitive Data Structures</h1>

<h1>Linear Data Structures</h1>
Linear data structures share the following properties:<br>
<ul>
	<li>Data elements are sequentially connected and each element is traversable in a single run</li>
	<li>All elements are on one single level, rather than multi-level (such as trees)</li>
	<li>Generally, do not use memory efficiently</li>
	<li>Time complexity is normally at least O(n). There are exceptions, such as binary search</li>
	
<h2>Comparison of Linear Data Structures</h2>

| | Arrays | Lists |
|-| ------ | ----- |
|Memory Access | Random Access Memory (through indexing) | Sequential Memory Access |
| Append | Amortized O(1) | O(n) due to Traversal |
| Prepend | O(n) | O(1) |
| Insertion / Deletion | O(n) | O(1) |
| Traversal | O(n) | O(n) |
| Search | Binary Search [O(log n)] | Linear Search [O(n)]
| Memory Size | Fixed | Dynamic |
| Storage Type | Consecutive | Random |
| Data Cost | Less [Only data is stored] | More [Pointer(s) are stored, as well as data] |
| Memory Utilization | Inefficient (due to fixed memory) | Efficient (due to dynamic memory) |

<br>
<h2>Array Implementation</h2>
<pre>
class Array:
  def __init__(self):
    self.arr = []
  def append(self, item):
    self.arr.append(item)
  def prepend(self, item):
    self.arr.insert(0, item)
  def __str__(self):
    return str(self.arr)
</pre>
<br>

<h2>Types of Linked Lists</h2>
  
|  | Singly Linked List | Doubly Linked List | Circular Linked List | Doubly Circular Linked List |
|--| ------------------ | ------------------ | -------------------- | --------------------------- |
| Implementation | Node contains data and a pointer to next node. | Node contains data and a pointer to next and previous nodes. | Node contains data and a pointer to next node. Last node has a pointer to head node. | Node contains data and a pointer to next and pervious nodes. Last node has a pointer to head node. |
| Order of Elements | Allows traversal in one direction. Set head node. | Allows traversal in two directions. Set head node. | Allows traversal in one direction. Any node can be head. | Allows traversal in two directions. Any node can be head.|
| Usage | Implementing stack data structure. | Implementing deque data structure. | Implementing fibonacci heaps. |  Implementing two-direction fibonacci heaps. | 





<h2>Singly Linked List Implementation</h2>
<pre>
class Node:<br>
    def __init__(self, initdata):<br>
        self.data = initdata<br>
        self.next = None<br>
    def getData(self):<br>
        return self.data<br>
    def getNext(self):<br>
        return self.next<br>
    def setData(self, newData):<br>
        self.data = newData<br>
    def setNext(self, newNext):<br>
        self.next = newNext<br>
<br>
class SinglyLinkedList:<br>
    def __init__(self):<br>
        self.head = None<br>
    def isEmpty(self):<br>
        return self.head == None<br>
    def prepend(self,item):<br>
        temp = Node(item)<br>
        temp.setNext(self.head)<br>
        self.head = temp<br>
    def append(self, item):<br>
        temp = Node(item)<br>
        current = self.head<br>
        if current:<br>
            while current.getNext() != None:<br>
                current = current.getNext()<br>
            current.setNext(temp)<br>
        else:<br>
            self.head = temp<br>
    def size(self):<br>
        current = self.head<br>
        count = 0<br>
        while current != None:<br>
            count = count + 1<br>
            current = current.getNext()<br>
        return count<br>
    def removeBackHalf(self):<br>
        ls = self.listSize()<br>
        mid = ls//2<br>
        current = self.head<br>
        count = 1<br>
        while count < mid:<br>
            count += 1<br>
            current = current.getNext()<br>
        current.setNext(None)<br>
    def search(self,item):<br>
        current = self.head<br>
        found = False<br>
        while current != None and found != True:<br>
            if current.getData() == item:<br>
                found = True<br>
            else:<br>
                current = current.getNext()<br>
        return found<br>
    def reverse(self):<br>
        prev = None<br>
        current = self.head<br>
        while current:<br>
            next = current.getNext()<br>
            current.setNext(prev)<br>
            prev = current<br>
            current = next<br>
        self.head = prev<br>
    def remove(self,item):<br>
        current = self.head<br>
        previous = None<br>
        found = False<br>
        while found != True:<br>
            if current.getData() == item:<br>
                found = True<br>
            else:<br>
                previous = current<br>
                current = current.getNext()<br>
        if previous == None:<br>
            self.head = current.getNext()<br>
        else:<br>
            previous.setNext(current.getNext())<br>
    def sortedMerge(self, a, b): <br>
        result = None<br>
        if a == None: <br>
            return b <br>
        if b == None: <br>
            return a <br>
        if a.getData() <= b.getData():<br>
            result = a <br>
            result.setNext(self.sortedMerge(a.getNext(), b))<br> 
        else: <br>
            result = b <br>
            result.setNext(self.sortedMerge(a, b.getNext()))<br>
        return result <br>
    def mergeSort(self, h): <br>
        if h or h.getNext(): <br>
            return h<br>
        middle = self.getMiddle(h) <br>
        nexttomiddle = middle.getNext()<br>
        middle.setNext(None)<br>
        left = self.mergeSort(h) <br>
        right = self.mergeSort(nexttomiddle) <br>
        sortedlist = self.sortedMerge(left, right) <br>
        return sortedlist<br>
    def getMiddle(self, head): <br>
        if (head == None): <br>
            return head <br>
        slow = head <br>
        fast = head <br>
        while fast.getNext() and fast.getNext().getNext(): <br>
            slow = slow.getNext()<br>
            fast = fast.getNext().getNext()<br>
        return slow<br>
    def printList(self):<br>
        current = self.head<br>
        s = ""<br>
        while current:<br>
            s = s + str(current.getData()) + " -> "<br>
            current = current.getNext()<br>
        s = s + "None"<br>
        return s
</pre>
<h2>Doubly Linked List Implementation</h2>
<pre>
class Node:<br>
	def __init__(self, initdata):<br>
		self.data = initdata<br>
		self.next = None<br>
		self.prev = None<br>
	def getData(self):<br>
		return self.data<br>
	def getNext(self):<br>
		return self.next<br>
	def getPrev(self):<br>
		return self.prev<br>
	def setData(self, newData):<br>
		self.data = newData<br>
	def setNext(self, newNext):<br>
		self.next = newNext<br>
	def setPrev(self,newPrev):<br>
		self.prev = newPrev<br>
<br>
class DoublyLinkedList:<br>
	def __init__(self):<br>
		self.head = None<br>
	def isEmpty(self):<br>
		return self.head == None<br>
	def prepend(self, data):<br>
		new_node = Node(data)<br>
		new_node.setNext(self.head)<br>
		new_node.setPrev(None)<br>
		self.head = new_node<br>
	def append(self, data):<br>
		new_node = Node(data)<br>
		if current:<br>
			while current.getNext():<br>
				current = current.getNext()<br>
			current.setNext(new_node)<br>
			new_node.setPrev(current)<br>
			new_node.setNext(None)<br>
		else:<br>
			self.head = new_node<br>
			new_node.setPrev(None)<br>
	def addAfterTarget(self, target, data):<br>
		new_node = Node(data)<br>
		current = self.head<br>
		while current.getData() != target:<br>
			current = current.getNext()<br>
		new_node.setPrev(current)<br>
		new_node.setNext(current.getNext())<br>
		current.setNext(new_node)<br>
		current.getNext().setPrev(new_node)<br>
	def removeTarget(self, target):<br>
		current = self.head<br>
		prev = None<br>
		while current.getData() != target:<br>
			prev = current<br>
			current = current.getNext()<br>
		removed_item = current<br>
		prev.setNext(current.getNext())<br>
		removed_item.setNext(None)<br>
		return removed_item.getData()<br>
	def __str__(self):<br>
		s = ""<br>
		current = self.head<br>
		while current:<br>
			s = s + str(current.getData()) + " <-> "<br>
			current = current.getNext()<br>
		return "None <-> " + s + "None" 
</pre>
<h2>Circular Linked List Implementation</h2>
class Node:
	def __init__(self, initdata):
		self.data = initdata
		self.next = None
	def getData(self):
		return self.data
	def getNext(self):
		return self.next
	def setData(self, newData):
		self.data = newData
	def setNet(self, newNext):
		self.next = newNext
	
class CircularLinkedList:
	def __init__(self):
		self.last = None

<h2>Stacks, Queues, and Deques</h2>

Stacks, Queues, and Deques are linear data structures that force operations to be done at the front and/or back of the list. All three data structures can be implemented as both arrays (lists in Python) and linked lists; however, each implementation has different effects on the computational complexity. <br><br>
For example, implementing a queue as a linked list would not necessarily be the best idea, as either the enQueue and deQueue function would have to traverse the entire list before inserting / removing the element. Also, linked lists use additional storage, as they store pointers along with data. 
<br><br>
In summation: queues and deques are best implemented as arrays. Stacks work best as linked lists.
<br>
| | Stacks | Queues | Deques |
|-| -----| ---| ---|
|Behavior | Last in First Out (LIFO) | First in First Out (FIFO) | Either Side in Either Side Out |
|Main Operations | isEmpty, Push, Pop, Peek, getSize | isEmpty, EnQueue, DeQueue, Peek, getSize | isEmpty, InsertFront, InsertBack, RemoveFront, RemoveBack, PeekFront, PeekBack, getSize | 
| Data Structure | Array, Linked List | Array, Linked List | Array, Linked List |

<h3>Array Stack Implementation</h3>
<pre>
class ArrayStack:<br>
  def __init__(self):<br>
    self.items = []<br>
  def isEmpty(self):<br>
    return self.items == []<br>
  def push(self, item):<br>
    self.items.append(item)<br>
  def pop(self):<br>
    return self.items.pop()<br>
  def peek(self):<br>
    return self.items[-1]<br>
  def getSize(self):<br>
    return len(self.items)<br>
  def __str__(self):<br>
    return str(self.items)
 </pre>
 
 <h3>Linked List Stack Implementation</h3>
 <br>
 <pre>
 class Node:<br>
  def __init__(self, initdata):<br>
    self.data = initdata<br>
    self.next = None<br>
  def getData(self):<br>
    return self.data<br>
  def getNext(self):<br>
    return self.next<br>
  def setData(self, newData):<br>
    self.data = newData<br>
  def setNext(self, newNext):<br>
    self.next = newNext<br>
<br>
class LinkedListStack:<br>
  def __init__(self):<br>
    self.head = None<br>
  def isEmpty(self):<br>
    return self.head == None<br>
  def push(self, item):<br>
    new_node = Node(item)<br>
    new_node.setNext(self.head)<br>
    self.head = new_node<br>
  def pop(self):<br>
    popped_node = self.head<br>
    self.head = self.head.getNext()<br>
    popped_node.setNext(None)<br>
    return popped_node.getData()<br>
  def peek(self):<br>
    return self.head.getData()<br>
  def getSize(self):<br>
    current = self.head<br>
    count = 0<br>
    while current:<br>
      count += 1<br>
      current = current.getNext()<br>
    return count<br>
  def __str__(self):<br>
    s = ""<br>
    current = self.head<br>
    while current.getNext():<br>
      s = s + str(current.getData()) + " -> "<br>
      current = current.getNext()<br>
    return s + "None"
</pre>

<h3>Array Queue Implementation</h3>
<pre>
class ArrayQueue:<br>
  def __init__(self):<br>
    self.items = []<br>
  def isEmpty(self):<br>
    return self.items == []<br>
  def enQueue(self, item):<br>
    self.items.append(item)<br>
  def deQueue(self):<br>
    return self.items.pop(0)<br>
  def peek(self):<br>
    return self.items[0]<br>
  def getSize(self):<br>
    return len(self.items)<br>
  def __str__(self):<br>
    return str(self.items)
</pre>

<h3>Linked List Queue Implementation</h3>
 <br>
 <pre>
 class Node:<br>
  def __init__(self, initdata):<br>
    self.data = initdata<br>
    self.next = None<br>
  def getData(self):<br>
    return self.data<br>
  def getNext(self):<br>
    return self.next<br>
  def setData(self, newData):<br>
    self.data = newData<br>
  def setNext(self, newNext):<br>
    self.next = newNext<br>
<br>
class LinkedListQueue:<br>
  def __init__(self):<br>
    self.head = None<br>
  def isEmpty(self):<br>
    return self.head == None<br>
  def enQueue(self, item):<br>
    new_node = Node(item)<br>
    new_node.setNext(self.head)<br>
    self.head = new_node<br>
  def deQueue(self):<br>
    current = self.head<br>
    prev = None
    while current.getNext():<br>
      prev = current<br>
      current = current.getNext()<br>
    popped_node = current<br>
    prev.setNext(None)
    popped_node.setNext(None)
    return popped_node.getData()<br>
  def peek(self):<br>
    return self.head.getData()<br>
  def getSize(self):<br>
    current = self.head<br>
    count = 0<br>
    while current:<br>
      count += 1<br>
      current = current.getNext()<br>
    return count<br>
  def __str__(self):<br>
    s = ""<br>
    current = self.head<br>
    while current.getNext():<br>
      s = s + str(current.getData()) + " -> "<br>
      current = current.getNext()<br>
    return s + "None"
</pre>

<h3>Array Deque Implementation</h3>
<pre>
class ArrayDeque:<br>
  def __init__(self):<br>
    self.items = []<br>
  def isEmpty(self):<br>
    return self.items == []<br>
  def insertFront(self, item):<br>
    self.items.insert(0, item)<br>
  def insertBack(self, item):<br>
    self.items.append(item)<br>
  def removeFront(self):<br>
    return self.items.pop(0)<br>
  def removeBack(self):<br>
    return self.items.pop()<br>
  def peekFront(self):<br>
    return self.items[0]<br>
  def peekBack(self):<br>
    return self.items[0]<br>
  def getSize(self):<br>
    return len(self.items)<br>
  def __str__(self):<br>
    return str(self.items)
</pre>

<h3>Linked List Deque Implementation</h3>
 <br>
 <pre>
 class Node:<br>
  def __init__(self, initdata):<br>
    self.data = initdata<br>
    self.next = None<br>
  def getData(self):<br>
    return self.data<br>
  def getNext(self):<br>
    return self.next<br>
  def setData(self, newData):<br>
    self.data = newData<br>
  def setNext(self, newNext):<br>
    self.next = newNext<br>
<br>
class LinkedListDeque:<br>
  def __init__(self):<br>
    self.head = None<br>
  def isEmpty(self):<br>
    return self.head == None<br>
  def insertFront(self, item):<br>
    new_node = Node(item)<br>
    new_node.setNext(self.head)<br>
    self.head = new_node<br>
  def insertBack(self, item):<br>
    new_node = Node(item)<br>
    current = self.head<br>
    if current:<br>
      while current.getNext():<br>
        current = current.getNext()<br>
      current.setNext(new_node)<br>
    else:<br>
      self.head = new_node<br>
  def removeFront(self):<br>
    popped_item = self.head<br>
    popped_item.getNext() = self.head<br>
    popped_item.setNext(None)<br>
    return popped_item<br>
  def removeBack(self):<br>
    current = self.head<br>
    prev = None<br>
    while current.getNext():<br>
      prev = current<br>
      current = current.getNext()<br>
    popped_node = current<br>
    prev.setNext(None)<br>
    popped_node.setNext(None)<br>
    return popped_node.getData()<br>
  def peekFront(self):<br>
    return self.head.getData()<br>
  def peekBack(self):<br>
    current = self.head<br>
    while current.getNext():<br>
      current = current.getNext()<br>
    return current.getData()<br>
  def getSize(self):<br>
    current = self.head<br>
    count = 0<br>
    while current:<br>
      count += 1<br>
      current = current.getNext()<br>
    return count<br>
  def __str__(self):<br>
    s = ""<br>
    current = self.head<br>
    while current.getNext():<br>
      s = s + str(current.getData()) + " -> "<br>
      current = current.getNext()<br>
    return s + "None"
</pre>
<h2>Priority Queues</h2>
A priority queue is similar to the regular queue, except for the following:<br>
* Every item has a priority associated with it<br>
* Elements with higher priorities are deQueued before the other elements<br>
* Elements with the same priority are deQueued in the order they were enQueued<br><br>
Priority queues typically support the following operations:<br>
* Insert(item, priority) - inserts an element with a priority<br>
* getHighestPriority() - returns the element with the highest priority<br>
* deleteHighestPriority() - deletes the element with the highest priority<br><br>
Priority queues can be implemented as arrays, linked lists, or heaps; however, heaps are the preferred data strucure.<br>
The reason for this is priority queue operations can be completed with lower computational complexity on heaps.<br>
The exact computational complexity priority queues can achieve is dependent on the type of heap that is implemented.
<h2>Heaps</h2>
Heaps are special tree based data strucures that are implemented as arrays. The benefit of storing a heap as an array, rather than a pointer-based binary tree, is the following:</br>
* Lower memory usage (only store data, rather than 3 additional pointers)</br>
* Easier memory management (just one object elemented, rather than N)</br>
* Better locality of memory (heap memory is contiguous due to array implementation; if binary tree is used, memory is scattered)</br>
<br>
Heap are stored as either max-heaps or min-heaps. <br><br>
<b>Max heaps</b> have the greatest key at the root. In other words, the biggest number is on top. Parent node is always larger than children nodes.<br>
<b>Min heaps</b> are the exact opposite. They have the lowest key at the root. Parent node is always smaller than children nodes.
<br>
<h3>Operation Time Complexity by Type of Heap</h3>

| Operation | Binary | Binomial | Fibonacci | Pairing | Brodal | Rank Pairing | Strict Fibonacci |
| --------- | ------ | -------- | --------- | ------- | ------ | ------------ | ---------------- |
| Find-Min | O(1) | O(log n) | O(1) | O(1) | O(1) | O(1) | O(1) |
| Delete-Min | O(log n) | O(log n) | O(log n) | O(log n) | O(log n) | O(log n) | O(log n) |
| Insert | O(log n) | O(1) | O(1) | O(1) | O(1) | O(1) | O(1) |
| Decrease Key | O(log n) | O(log n) | O(1) | O(log n) | O(1) | O(1) | O(1) |
| Merge | O(n) | O(log n) | O(1) | O(1) | O(1) | O(1) | O(1) |

<h2>Binary Heap</h2>
Binary heaps 

<h1>Tree Data Structure</h1>
Trees are non-linear, hierarchical data structures. They are a widely used abstract data type (ADT), composed of the following:</br>
<ul>
  <li>Node: Basic unit of trees that contain data and pointers to other nodes</li>
  <li>Edges: The connection, or pointer, between a parent and child node</li>
  <li>Root Node: A node from which the rest of the tree stems. Normally depicted at the top of the tree</li>
  <li>Parent Node: A node that extends a pointer to a child node</li>
  <li>Child Node: A node that is pointed to by a parent node</li>
  <li>Sibling Node: Two or more nodes that connect to one parent node</li>
  <li>Leaf Node: A node that has no children nodes</li>
  <li>Degree: The number of children had by a node</li>
  <li>Depth: The number of edges on the longest path from a chosen node to the root. The root node has a depth of 0</li>
  <li>Height: The number of edges on the longest path from a chosen node to a leaf. Leaf nodes have heights of 0</li>
  <li>Forest: A set of trees</li>
</ul>
<h2>General Tree</h2>
General trees are the most basic type of tree. They have the following rules that differentiate them from graphs:</br>
<ul>
  <li>There is exactly one root node and it has no parent node</li>
  <li>Each child node has exactly one parent node, meaning there are no cycles in trees</li>
</ul>
<h2>Binary Tree</h2>
Binary trees are different from general trees in that each parent node is restricted to having 0, 1, or 2 children nodes</br>
<pre>
class Node:
	def __init__(self, initdata):
		self.data = initdata
		self.left = None
		self.right = None
		self.level = None

class BinarySearchTree:
	def __init__(self):
		self.root = None
	def insert(self, data):
		new_node = Node(data)
		if self.root == None:
			self.root = new_node
		else:
			current = self.root
			while 1:
				if data < current.data:
					if current.left:
						current = current.left
					else:
						current.left = new_node
						break
				elif data > current.data:
					if current.right:
						current = current.right
					else:
						current.right = new_node
						break
				else:
					break
	def breadthFirstTraversal(self):
		self.root.level = 0
		queue = [self.root]
		out = []
		current_level = self.root.level
		while len(queue) > 0:
			current_node = queue.pop(0)
			if current_node.level > current_level:
				current_level += 1
				out.append("\n")
			out.append(str(current_node.data)+" ")
			if current_node.left:
				current_node.left.level = current_level + 1
				queue.append(current_node.left)
			if current_node.right:
				current_node.right.level = current_level + 1
				queue.append(current_node.right)
		print("".join(out))
	def inorder(self, node):
		if node:
			self.inorder(node.left)
			print(node.data)
			self.inorder(node.right)
	def preorder(self, node):
		if node:
			print(node.data)
			self.preorder(node.left)
			self.preorder(node.right)
	def postorder(self, node):
		if node:
			self.postorder(node.left)
			self.postorder(node.right)
			print(node.data)

b = BinarySearchTree()
arr = [8, 3, 10, 1, 6, 14, 4, 7, 13]
for i in arr:
	b.insert(i)
print("Breadth First Traversal:")
b.breadthFirstTraversal()
print("\nInOrder:")
b.inorder(b.root)
print("\nPreOrder:")
b.preorder(b.root)
print("\nPostOrder:")
b.postorder(b.root)</pre>
<h2>Binary Search Tree</h2>
Binary search trees are different from binary trees in that parent node values must be greater than left node values and less than right node values
<h2>AVL Tree</h2>
AVL Trees
