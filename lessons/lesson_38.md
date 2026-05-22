---
render_with_liquid: false
title: "Lesson 38: Merge Sort, Stacks, Queues, Linked Lists & Hash Tables in Python"
nav_order: 38
---

# Lesson 38: Merge Sort, Stacks, Queues, Linked Lists & Hash Tables in Python

---

## Lesson Introduction

Welcome to one of the most exciting lessons in your Python journey! In this lesson, you will learn about five incredibly important topics in computer science:

1. **Merge Sort** — a clever way to sort a list of numbers
2. **Stacks** — a structure that works like a pile of pancakes
3. **Queues** — a structure that works like a line at a shop
4. **Linked Lists** — a chain of connected data boxes
5. **Hash Tables** — a super-fast way to store and find data

These are part of a topic called **Data Structures and Algorithms** (DSA). Don't be scared by that name. It simply means: "how do we organise and process data efficiently?"

By the end of this lesson you will understand how each one works, how to write them in Python, and where they are used in real life.

> **Tip:** You do not need to memorise everything. Focus on *understanding what each structure does* and *why it was invented*. The code will make sense once the idea is clear.

---

## Prerequisite Concepts

Before we begin, let's make sure you understand these building blocks. If you already know them, just skim through quickly.

### Python Lists (Quick Recap)

A list is an ordered collection of items stored in one variable.

```python
fruits = ["apple", "banana", "cherry"]
print(fruits[0])   # apple
print(fruits[1])   # banana
print(fruits[-1])  # cherry  (last item)
```

**Expected Output:**
```
apple
banana
cherry
```

You can add items with `.append()` and remove the last item with `.pop()`:

```python
fruits.append("mango")    # add to the end
print(fruits)

last = fruits.pop()       # remove and return the last item
print(last)
print(fruits)
```

**Expected Output:**
```
['apple', 'banana', 'cherry', 'mango']
mango
['apple', 'banana', 'cherry']
```

### Python Classes (Quick Recap)

A **class** is a blueprint for creating objects. Think of it like a cookie cutter — you define the shape once and then make as many cookies (objects) as you want.

```python
class Dog:
    def __init__(self, name):   # __init__ runs when you create a Dog object
        self.name = name        # self.name stores the name on THIS specific dog

    def bark(self):
        print(self.name + " says: Woof!")

my_dog = Dog("Rex")
my_dog.bark()
```

**Expected Output:**
```
Rex says: Woof!
```

- `class Dog:` — defines the blueprint
- `__init__(self, name)` — the setup method (runs automatically when you create a Dog)
- `self` — refers to the specific object being created/used
- `self.name = name` — stores the name on this specific dog object

### Recursion (Quick Intro)

**Recursion** means a function that calls itself. It's like looking up a word in a dictionary, and the definition uses the same word — you have to look it up again!

```python
def countdown(n):
    if n <= 0:        # BASE CASE — when to stop
        print("Done!")
        return
    print(n)
    countdown(n - 1)  # RECURSIVE CALL — function calls itself

countdown(3)
```

**Expected Output:**
```
3
2
1
Done!
```

Every recursive function needs:
- A **base case** (when to stop — prevents infinite looping)
- A **recursive call** (calling itself with a smaller/simpler version of the problem)

---

## Part 1: Merge Sort

### What is Merge Sort?

Imagine you have a messy pile of numbered cards on a table. You want to arrange them from smallest to largest. One smart strategy is:

1. **Split** the pile in half
2. **Sort** each half separately
3. **Merge** the two sorted halves back together, putting smaller numbers first

This is **exactly** how Merge Sort works! It is a **divide-and-conquer** algorithm — it solves a big problem by breaking it into smaller problems.

### Why Was Merge Sort Invented?

Simple sorting methods (like Bubble Sort) are slow for large lists because they compare almost every element with every other element. Merge Sort is much faster because it keeps dividing the problem in half. This gives it a time complexity of **O(n log n)** — which means it scales very well for large datasets.

> **Real-world use:** Merge Sort (or variations of it) is used in programming languages' built-in sort functions, in database sorting, and in external sorting (when data is too big to fit in memory).

### How Merge Sort Works — Step by Step

Let's walk through sorting this list manually: `[12, 8, 9, 3, 11, 5, 4]`

**Step 1 — Keep splitting in half until each piece has only 1 element:**

```
[12, 8, 9, 3, 11, 5, 4]
[12, 8, 9]          [3, 11, 5, 4]
[12]    [8, 9]      [3, 11]    [5, 4]
[12]  [8]  [9]      [3]  [11]  [5]  [4]
```

A list of 1 element is already sorted (there's nothing to compare).

**Step 2 — Start merging pairs, always putting the smaller value first:**

```
[8, 9]     (8 < 9, so 8 goes first)
[3, 11]    (3 < 11, already in order)
[4, 5]     (4 < 5, so 4 goes first)
```

**Step 3 — Merge larger pieces:**

```
[8, 9, 12]      (merge [12] with [8, 9]: compare 8 vs 12 → 8, then 9 vs 12 → 9, then 12)
[3, 4, 5, 11]   (merge [3, 11] with [4, 5])
```

**Step 4 — Final merge:**

```
[3, 4, 5, 8, 9, 11, 12]   ← SORTED!
```

> **Think about it:** Why does splitting in half make the problem faster? Because if you have 8 elements, splitting gives you 4+4. Splitting again gives 2+2+2+2. You only need to split about log₂(8) = 3 times to get to single elements. That's much fewer steps than comparing all pairs!

### The Merge Step Explained

The **merge** step is the heart of the algorithm. When you have two sorted sub-lists, you merge them by:
- Comparing the front items of both lists
- Always picking the smaller one
- Moving to the next item in whichever list you picked from
- When one list runs out, just add all remaining items from the other list

```
Left:  [3, 8, 9]
Right: [4, 5, 11]

Compare 3 vs 4  → pick 3   Result: [3]
Compare 8 vs 4  → pick 4   Result: [3, 4]
Compare 8 vs 5  → pick 5   Result: [3, 4, 5]
Compare 8 vs 11 → pick 8   Result: [3, 4, 5, 8]
Compare 9 vs 11 → pick 9   Result: [3, 4, 5, 8, 9]
11 has nothing to compare with → add 11 Result: [3, 4, 5, 8, 9, 11]
```

### Implementing Merge Sort in Python (Recursive Version)

```python
def mergeSort(arr):
    # BASE CASE: A list of 0 or 1 elements is already sorted
    if len(arr) <= 1:
        return arr

    # DIVIDE: Find the middle point and split the list
    mid = len(arr) // 2      # '//' means integer division (no decimals)
    leftHalf = arr[:mid]     # everything BEFORE the middle index
    rightHalf = arr[mid:]    # everything FROM the middle index onwards

    # RECURSE: Sort each half by calling mergeSort on each half
    sortedLeft = mergeSort(leftHalf)
    sortedRight = mergeSort(rightHalf)

    # CONQUER: Merge the two sorted halves together
    return merge(sortedLeft, sortedRight)


def merge(left, right):
    result = []    # this will hold the merged, sorted elements
    i = 0          # pointer for the left list
    j = 0          # pointer for the right list

    # Compare elements from both lists one by one
    while i < len(left) and j < len(right):
        if left[i] < right[j]:
            result.append(left[i])   # left item is smaller, add it
            i += 1                   # move the left pointer forward
        else:
            result.append(right[j])  # right item is smaller, add it
            j += 1                   # move the right pointer forward

    # If any items remain in left (right is empty), add them all
    result.extend(left[i:])
    # If any items remain in right (left is empty), add them all
    result.extend(right[j:])

    return result


# Test it
mylist = [3, 7, 6, -10, 15, 23.5, 55, -13]
mysortedlist = mergeSort(mylist)
print("Sorted array:", mysortedlist)
```

**Expected Output:**
```
Sorted array: [-13, -10, 3, 6, 7, 15, 23.5, 55]
```

**Line-by-line explanation:**

| Line | What it does |
|---|---|
| `if len(arr) <= 1: return arr` | Base case — a single element is already sorted, stop recursing |
| `mid = len(arr) // 2` | Find the middle index using integer division (e.g. 8//2 = 4) |
| `leftHalf = arr[:mid]` | Slice the list from index 0 up to (not including) mid |
| `rightHalf = arr[mid:]` | Slice the list from mid to the end |
| `sortedLeft = mergeSort(leftHalf)` | Recursively sort the left half |
| `sortedRight = mergeSort(rightHalf)` | Recursively sort the right half |
| `return merge(sortedLeft, sortedRight)` | Combine the two sorted halves |
| `i = 0; j = 0` | Pointers (index markers) for each half-list |
| `while i < len(left) and j < len(right)` | Keep going while both lists have items left |
| `result.extend(left[i:])` | Add all remaining left items (already sorted) |
| `result.extend(right[j:])` | Add all remaining right items (already sorted) |

> **What happens if you change `<` to `<=`?** Try it! The result is the same because equal elements are handled either way. The current code is stable — equal elements from the left list come first.

### Merge Sort Without Recursion (Iterative Version)

Some problems don't allow recursion. Here's Merge Sort using a `while` loop instead:

```python
def merge(left, right):
    result = []
    i = j = 0

    while i < len(left) and j < len(right):
        if left[i] < right[j]:
            result.append(left[i])
            i += 1
        else:
            result.append(right[j])
            j += 1

    result.extend(left[i:])
    result.extend(right[j:])
    return result


def mergeSort(arr):
    step = 1         # start by merging sub-arrays of length 1
    length = len(arr)

    while step < length:
        for i in range(0, length, 2 * step):
            # Extract the left and right chunks
            left = arr[i : i + step]
            right = arr[i + step : i + 2 * step]

            # Merge them
            merged = merge(left, right)

            # Place merged result back into the original array
            for j, val in enumerate(merged):
                arr[i + j] = val

        step *= 2    # double the chunk size each round

    return arr


mylist = [3, 7, 6, -10, 15, 23.5, 55, -13]
print(mergeSort(mylist))
```

**Expected Output:**
```
[-13, -10, 3, 6, 7, 15, 23.5, 55]
```

This version modifies the array **in place** (no extra arrays created for the split). It starts by merging pairs of single elements, then pairs of pairs, and so on — doubling the chunk size each time until the whole array is sorted.

### Quick Comparison

| Feature | Recursive Version | Iterative Version |
|---|---|---|
| Code clarity | Easier to read | Slightly harder to read |
| Memory usage | Uses call stack | Doesn't use call stack |
| Result | Same | Same |

---

## Part 2: Stacks

### What is a Stack?

A **Stack** is a data structure where the **last item added** is the **first item removed**.

Think of a **stack of pancakes**:
- You add new pancakes on top
- You remove pancakes from the top
- You cannot grab a pancake from the middle without moving the ones above it

This rule is called **LIFO** — **Last In, First Out**.

### Why Do Stacks Exist?

Stacks are used everywhere in computing:
- **Undo button** in text editors (last action is undone first)
- **Browser back button** (last page visited is where you go back to)
- **Function call stack** (the computer tracks which function called which)
- **Depth-first search** in graphs and trees

### Stack Operations

| Operation | What it does |
|---|---|
| **Push** | Add a new element on top of the stack |
| **Pop** | Remove and return the top element |
| **Peek** | Look at the top element without removing it |
| **isEmpty** | Check if the stack has no elements |
| **Size** | Count how many elements are in the stack |

### Visualising a Stack

```
Push A → Stack: [A]
Push B → Stack: [A, B]
Push C → Stack: [A, B, C]   ← C is on top
Peek   → returns 'C'         ← still [A, B, C]
Pop    → returns 'C'  Stack: [A, B]
Pop    → returns 'B'  Stack: [A]
```

### Method 1: Stack Using a Python List

The simplest way to build a stack is using a Python list:

```python
stack = []

# PUSH: add items to the top (end of the list)
stack.append('A')
stack.append('B')
stack.append('C')
print("Stack:", stack)

# PEEK: look at the top item without removing it
# [-1] means "the last item" in Python
topElement = stack[-1]
print("Peek:", topElement)

# POP: remove and return the top item
poppedElement = stack.pop()
print("Pop:", poppedElement)

# Stack after popping
print("Stack after Pop:", stack)

# isEmpty: check if stack is empty
isEmpty = not bool(stack)    # bool([]) is False, so not False = True
print("isEmpty:", isEmpty)

# Size
print("Size:", len(stack))
```

**Expected Output:**
```
Stack: ['A', 'B', 'C']
Peek: C
Pop: C
Stack after Pop: ['A', 'B']
isEmpty: False
Size: 2
```

> **Why `stack[-1]` for peek?** In Python, index `-1` always refers to the last element. Since the "top" of our stack is the end of the list, `stack[-1]` gives us the top without removing it.

### Method 2: Stack Using a Class

Using a dedicated class gives you better organisation and error-handling:

```python
class Stack:
    def __init__(self):
        self.stack = []    # internal list to hold elements

    def push(self, element):
        self.stack.append(element)

    def pop(self):
        if self.isEmpty():
            return "Stack is empty"    # avoid error if empty
        return self.stack.pop()

    def peek(self):
        if self.isEmpty():
            return "Stack is empty"
        return self.stack[-1]

    def isEmpty(self):
        return len(self.stack) == 0   # True if no elements

    def size(self):
        return len(self.stack)


# Create a stack and test it
myStack = Stack()

myStack.push('A')
myStack.push('B')
myStack.push('C')

print("Stack:", myStack.stack)
print("Pop:", myStack.pop())
print("Stack after Pop:", myStack.stack)
print("Peek:", myStack.peek())
print("isEmpty:", myStack.isEmpty())
print("Size:", myStack.size())
```

**Expected Output:**
```
Stack: ['A', 'B', 'C']
Pop: C
Stack after Pop: ['A', 'B']
Peek: B
isEmpty: False
Size: 2
```

### Method 3: Stack Using a Linked List

For more advanced use cases (especially when you need dynamic memory), you can build a stack using a Linked List:

```python
class Node:
    def __init__(self, value):
        self.value = value    # the data stored in this node
        self.next = None      # pointer to the next node (starts as None)


class Stack:
    def __init__(self):
        self.head = None    # the top of the stack is the head node
        self.size = 0

    def push(self, value):
        new_node = Node(value)      # create a new node
        if self.head:
            new_node.next = self.head   # new node points to old top
        self.head = new_node            # new node becomes the new top
        self.size += 1

    def pop(self):
        if self.isEmpty():
            return "Stack is empty"
        popped_node = self.head         # grab the top node
        self.head = self.head.next      # move head to next node
        self.size -= 1
        return popped_node.value

    def peek(self):
        if self.isEmpty():
            return "Stack is empty"
        return self.head.value          # value of the top node

    def isEmpty(self):
        return self.size == 0

    def stackSize(self):
        return self.size

    def traverseAndPrint(self):
        currentNode = self.head
        while currentNode:
            print(currentNode.value, end=" -> ")
            currentNode = currentNode.next
        print()


myStack = Stack()
myStack.push('A')
myStack.push('B')
myStack.push('C')

print("LinkedList: ", end="")
myStack.traverseAndPrint()
print("Peek:", myStack.peek())
print("Pop:", myStack.pop())
print("LinkedList after Pop: ", end="")
myStack.traverseAndPrint()
print("isEmpty:", myStack.isEmpty())
print("Size:", myStack.stackSize())
```

**Expected Output:**
```
LinkedList: C -> B -> A -> 
Peek: C
Pop: C
LinkedList after Pop: B -> A -> 
isEmpty: False
Size: 2
```

> **Notice** the order is reversed! When we push A, then B, then C, the Linked List stack shows `C -> B -> A` because C was pushed last and sits at the head (top).

### Choosing Between List and Linked List Implementation

| | List-based Stack | Linked List Stack |
|---|---|---|
| Memory efficiency | ✅ Better (no extra pointers) | ❌ Each node has extra pointer |
| Dynamic size | ❌ Can fill up | ✅ Grows freely |
| Code simplicity | ✅ Simpler | ❌ More complex |

---

## Part 3: Queues

### What is a Queue?

A **Queue** is a data structure where the **first item added** is the **first item removed**.

Think of **people standing in line at a bus stop**:
- People join the line at the back
- People leave from the front
- The first person who arrived is the first to board the bus

This is called **FIFO** — **First In, First Out**.

### Why Do Queues Exist?

Queues are used in many real-world systems:
- **Office printer queue** — documents print in the order they were sent
- **Online ticket booking** — customers are served in the order they joined
- **CPU task scheduling** — the operating system uses queues to manage running programs
- **Breadth-first search** in graphs (visiting all nearby nodes before far ones)
- **Message queues** in distributed systems (like WhatsApp message delivery)

### Queue Operations

| Operation | What it does |
|---|---|
| **Enqueue** | Add a new element to the back of the queue |
| **Dequeue** | Remove and return the element at the front |
| **Peek** | Look at the front element without removing it |
| **isEmpty** | Check if the queue has no elements |
| **Size** | Count how many elements are in the queue |

### Visualising a Queue

```
Enqueue A → Queue: [A]
Enqueue B → Queue: [A, B]
Enqueue C → Queue: [A, B, C]
Peek      → returns 'A'        (front of the queue)
Dequeue   → returns 'A' Queue: [B, C]
Dequeue   → returns 'B' Queue: [C]
```

### Stack vs Queue — The Key Difference

| | Stack (LIFO) | Queue (FIFO) |
|---|---|---|
| Think of... | A pile of pancakes | A line at a shop |
| Add to... | The top | The back |
| Remove from... | The top | The front |
| Real example | Undo button | Printer queue |

### Method 1: Queue Using a Python List

```python
queue = []

# ENQUEUE: add items to the back (end of the list)
queue.append('A')
queue.append('B')
queue.append('C')
print("Queue:", queue)

# PEEK: look at the front item (index 0)
frontElement = queue[0]
print("Peek:", frontElement)

# DEQUEUE: remove and return the FRONT item
# pop(0) removes the first item — index 0
poppedElement = queue.pop(0)
print("Dequeue:", poppedElement)

print("Queue after Dequeue:", queue)

# isEmpty
isEmpty = not bool(queue)
print("isEmpty:", isEmpty)

# Size
print("Size:", len(queue))
```

**Expected Output:**
```
Queue: ['A', 'B', 'C']
Peek: A
Dequeue: A
Queue after Dequeue: ['B', 'C']
isEmpty: False
Size: 2
```

> **Important note:** `queue.pop(0)` removes the first element, but it forces Python to shift all remaining elements one position back in memory. For very large queues this is slow. The Linked List implementation below avoids this.

### Method 2: Queue Using a Class

```python
class Queue:
    def __init__(self):
        self.queue = []

    def enqueue(self, element):
        self.queue.append(element)     # add to the back

    def dequeue(self):
        if self.isEmpty():
            return "Queue is empty"
        return self.queue.pop(0)       # remove from the front

    def peek(self):
        if self.isEmpty():
            return "Queue is empty"
        return self.queue[0]           # look at the front

    def isEmpty(self):
        return len(self.queue) == 0

    def size(self):
        return len(self.queue)


myQueue = Queue()

myQueue.enqueue('A')
myQueue.enqueue('B')
myQueue.enqueue('C')

print("Queue:", myQueue.queue)
print("Peek:", myQueue.peek())
print("Dequeue:", myQueue.dequeue())
print("Queue after Dequeue:", myQueue.queue)
print("isEmpty:", myQueue.isEmpty())
print("Size:", myQueue.size())
```

**Expected Output:**
```
Queue: ['A', 'B', 'C']
Peek: A
Dequeue: A
Queue after Dequeue: ['B', 'C']
isEmpty: False
Size: 2
```

### Method 3: Queue Using a Linked List

```python
class Node:
    def __init__(self, data):
        self.data = data     # the value stored
        self.next = None     # pointer to next node


class Queue:
    def __init__(self):
        self.front = None    # the node at the front (where we dequeue from)
        self.rear = None     # the node at the back (where we enqueue to)
        self.length = 0

    def enqueue(self, element):
        new_node = Node(element)
        if self.rear is None:               # queue was empty
            self.front = self.rear = new_node
        else:
            self.rear.next = new_node       # link the old rear to new node
            self.rear = new_node            # update rear to the new node
        self.length += 1

    def dequeue(self):
        if self.isEmpty():
            return "Queue is empty"
        temp = self.front                   # grab the front node
        self.front = temp.next             # move front to the next node
        self.length -= 1
        if self.front is None:             # queue is now empty
            self.rear = None
        return temp.data

    def peek(self):
        if self.isEmpty():
            return "Queue is empty"
        return self.front.data

    def isEmpty(self):
        return self.length == 0

    def size(self):
        return self.length

    def printQueue(self):
        temp = self.front
        while temp:
            print(temp.data, end=" -> ")
            temp = temp.next
        print()


myQueue = Queue()
myQueue.enqueue('A')
myQueue.enqueue('B')
myQueue.enqueue('C')

print("Queue: ", end="")
myQueue.printQueue()
print("Peek:", myQueue.peek())
print("Dequeue:", myQueue.dequeue())
print("Queue after Dequeue: ", end="")
myQueue.printQueue()
print("isEmpty:", myQueue.isEmpty())
print("Size:", myQueue.size())
```

**Expected Output:**
```
Queue: A -> B -> C -> 
Peek: A
Dequeue: A
Queue after Dequeue: B -> C -> 
isEmpty: False
Size: 2
```

> **Why is the Linked List version better for large queues?** Because removing the front item (`dequeue`) only requires updating the `front` pointer — no elements need to shift in memory. It is O(1) rather than O(n).

---

## Part 4: Linked Lists

### What is a Linked List?

A **Linked List** is a sequence of data where each piece of data (called a **node**) knows where the next piece is stored in memory.

Think of a **treasure hunt**: each clue tells you where to find the next clue. You can't jump directly to clue 5 — you have to follow the chain from the start.

A single node contains:
- **Data** — the actual value (e.g. a number, name, etc.)
- **Next pointer** — the memory address of the next node

```
[Data: 7 | Next: →]  →  [Data: 11 | Next: →]  →  [Data: 3 | Next: None]
```

The first node is called the **head**. The last node's `next` pointer is `None`, which signals the end.

### Linked Lists vs Arrays

| Feature | Array | Linked List |
|---|---|---|
| Fixed size? | Yes | No — grows dynamically |
| Elements stored together in memory? | Yes (contiguous) | No — scattered in memory |
| Access element by position | ✅ Fast — myArray[5] | ❌ Slow — must traverse |
| Insert/delete without shifting? | ❌ Must shift elements | ✅ Just update pointers |
| Memory per element | ✅ Low | ❌ Higher (stores pointer too) |

### Types of Linked Lists

**1. Singly Linked List** — each node points to the next node only

```
Head → [7|→] → [11|→] → [3|→] → [2|→] → [9|None]
```

**2. Doubly Linked List** — each node points to both the next AND previous node

```
None ← [←|7|→] ↔ [←|11|→] ↔ [←|3|→] ↔ [←|9|None]
```

**3. Circular Linked List** — the last node points back to the head (forming a circle)

```
Head → [7|→] → [11|→] → [3|→] → (back to Head)
```

### Building a Singly Linked List: Step 1 — The Node Class

```python
class Node:
    def __init__(self, data):
        self.data = data    # the value this node holds
        self.next = None    # pointer to the next node (None = end of list)
```

To create nodes and link them manually:

```python
node1 = Node(7)
node2 = Node(11)
node3 = Node(3)
node4 = Node(2)
node5 = Node(9)

# Link the nodes together to form a chain
node1.next = node2    # 7 → 11
node2.next = node3    # 11 → 3
node3.next = node4    # 3 → 2
node4.next = node5    # 2 → 9
# node5.next is already None (end of list)
```

### Traversal — Walking Through a Linked List

**Traversal** means visiting each node one by one, starting from the head:

```python
def traverseAndPrint(head):
    currentNode = head            # start at the head
    while currentNode:            # keep going until currentNode is None
        print(currentNode.data, end=" -> ")
        currentNode = currentNode.next    # move to the next node
    print("null")                 # signal the end


node1 = Node(7)
node2 = Node(11)
node3 = Node(3)
node4 = Node(2)
node5 = Node(9)

node1.next = node2
node2.next = node3
node3.next = node4
node4.next = node5

traverseAndPrint(node1)
```

**Expected Output:**
```
7 -> 11 -> 3 -> 2 -> 9 -> null
```

**Line-by-line explanation:**
- `currentNode = head` — we start at the first node
- `while currentNode:` — a Node object is "truthy"; `None` is "falsy", so this loop stops when we reach the end
- `currentNode = currentNode.next` — this is how we "move" to the next node

### Finding the Minimum Value in a Linked List

```python
def findLowestValue(head):
    minValue = head.data             # start by assuming the head has the minimum
    currentNode = head.next          # start checking from the second node

    while currentNode:
        if currentNode.data < minValue:
            minValue = currentNode.data    # update minimum if smaller found
        currentNode = currentNode.next

    return minValue


node1 = Node(7)
node2 = Node(11)
node3 = Node(3)
node4 = Node(2)
node5 = Node(9)

node1.next = node2
node2.next = node3
node3.next = node4
node4.next = node5

print("The lowest value:", findLowestValue(node1))
```

**Expected Output:**
```
The lowest value: 2
```

### Deleting a Node from a Linked List

To delete a node, you must:
1. Find the node **before** the one you want to delete
2. Make that node's `next` skip over the target node
3. Python's garbage collector will clean up the deleted node automatically

```
Before: [7|→] → [11|→] → [3|→] → [2|→] → [9|None]
                           ↑ delete this

After:  [7|→] → [11|→] → [2|→] → [9|None]
                  ↑ node3's previous node now skips node3 and points to node4
```

```python
def deleteSpecificNode(head, nodeToDelete):
    # Special case: deleting the HEAD node
    if head == nodeToDelete:
        return head.next    # the new head is the second node

    currentNode = head
    # Traverse until we find the node BEFORE the one to delete
    while currentNode.next and currentNode.next != nodeToDelete:
        currentNode = currentNode.next

    if currentNode.next is None:
        return head    # nodeToDelete not found, nothing to delete

    # Skip over nodeToDelete
    currentNode.next = currentNode.next.next

    return head    # head hasn't changed


node1 = Node(7)
node2 = Node(11)
node3 = Node(3)
node4 = Node(2)
node5 = Node(9)

node1.next = node2
node2.next = node3
node3.next = node4
node4.next = node5

print("Before deletion:")
traverseAndPrint(node1)

node1 = deleteSpecificNode(node1, node4)   # delete node with value 2

print("After deletion:")
traverseAndPrint(node1)
```

**Expected Output:**
```
Before deletion:
7 -> 11 -> 3 -> 2 -> 9 -> null
After deletion:
7 -> 11 -> 3 -> 9 -> null
```

### Inserting a Node into a Linked List

To insert a node at a specific position:
1. Traverse to the node just **before** the desired position
2. Make the new node point to what was next
3. Make the previous node point to the new node

```python
def insertNodeAtPosition(head, newNode, position):
    # Insert at the very beginning (position 1)
    if position == 1:
        newNode.next = head
        return newNode       # new node is now the head

    currentNode = head
    # Walk to position-2 steps (the node BEFORE insertion point)
    for _ in range(position - 2):
        if currentNode.next is None:
            break
        currentNode = currentNode.next

    newNode.next = currentNode.next    # new node points forward
    currentNode.next = newNode         # previous node points to new node
    return head


node1 = Node(7)
node2 = Node(3)
node3 = Node(2)
node4 = Node(9)

node1.next = node2
node2.next = node3
node3.next = node4

print("Original list:")
traverseAndPrint(node1)

newNode = Node(97)
node1 = insertNodeAtPosition(node1, newNode, 2)   # insert 97 at position 2

print("After insertion:")
traverseAndPrint(node1)
```

**Expected Output:**
```
Original list:
7 -> 3 -> 2 -> 9 -> null
After insertion:
7 -> 97 -> 3 -> 2 -> 9 -> null
```

### Time Complexity: Linked Lists vs Arrays

| Operation | Array | Linked List |
|---|---|---|
| Access by index | O(1) — instant | O(n) — must traverse |
| Search (linear) | O(n) | O(n) |
| Insert at beginning | O(n) — must shift | O(1) — update pointer |
| Insert at end | O(1) (amortised) | O(n) (must traverse to end) |
| Delete at beginning | O(n) — must shift | O(1) — update pointer |

> **Binary search is NOT possible** on a Linked List because you can't jump directly to the middle — you must traverse from the head.

---

## Part 5: Hash Tables

### What is a Hash Table?

A **Hash Table** is a data structure that stores data using a special technique called **hashing**, which lets you find, add, and delete data extremely quickly — even in huge datasets.

Imagine a **library with a magic filing system**: instead of searching every shelf for a book, you give the book title to a librarian who instantly tells you exactly which shelf it's on. That "magic librarian" is the **hash function**.

### Why Are Hash Tables So Fast?

In an array or linked list, to find "Bob" you might have to check every element until you find him — that's **O(n)** time.

With a hash table, "Bob" maps to a specific index in one calculation — that's **O(1)** time (constant time, regardless of how many people are stored).

### Key Vocabulary

| Term | Meaning |
|---|---|
| **Bucket** | A slot in the hash table (like a drawer in a filing cabinet) |
| **Hash function** | The function that converts a key into a bucket index |
| **Hash code** | The number produced by the hash function |
| **Collision** | When two different keys produce the same hash code |
| **Chaining** | Solving collisions by allowing multiple items per bucket (using a list) |

### Building a Hash Table from Scratch

#### Step 1: Create an Empty Table

We start with a list of 10 empty buckets:

```python
my_list = [None, None, None, None, None, None, None, None, None, None]
print(my_list)
```

**Expected Output:**
```
[None, None, None, None, None, None, None, None, None, None]
```

Each position (index 0–9) is a bucket.

#### Step 2: Create a Hash Function

A **hash function** takes a key (like a name) and converts it to a number that fits our table size (0–9).

Our strategy: add up the **Unicode numbers** of all characters in the name, then use **modulo 10** to get a number between 0 and 9.

> **Unicode** is a system where every character has a unique number. For example, 'A' = 65, 'B' = 66, 'a' = 97, 'b' = 98. In Python, `ord('A')` gives you the Unicode number.
>
> **Modulo** (`%`) gives you the remainder after division. So `275 % 10 = 5` (because 275 = 27×10 with remainder 5).

```python
def hash_function(value):
    sum_of_chars = 0
    for char in value:
        sum_of_chars += ord(char)    # ord() gives Unicode number of a character
    return sum_of_chars % 10         # modulo 10 gives a number 0-9

print("'Bob' has hash code:", hash_function('Bob'))
```

**Expected Output:**
```
'Bob' has hash code: 5
```

How did we get 5?
- 'B' = 66, 'o' = 111, 'b' = 98
- 66 + 111 + 98 = 275
- 275 % 10 = 5 → Bob is stored at index 5 ✅

> **What if you change 'Bob' to 'Bob2'?** Try adding more characters and see how the hash code changes!

#### Step 3: Insert an Element

```python
def add(name):
    index = hash_function(name)    # calculate where to store
    my_list[index] = name          # store the name at that index

add('Bob')
print(my_list)
```

**Expected Output:**
```
[None, None, None, None, None, 'Bob', None, None, None, None]
```

"Bob" is stored at index 5, exactly where our hash function said!

Let's add more names:

```python
add('Pete')
add('Jones')
add('Lisa')
add('Siri')
print(my_list)
```

**Expected Output:**
```
[None, 'Jones', None, 'Lisa', None, 'Bob', None, 'Siri', 'Pete', None]
```

#### Step 4: Look Up a Name

```python
def contains(name):
    index = hash_function(name)    # calculate the index
    return my_list[index] == name  # check if the name is there

print("'Pete' is in the Hash Table:", contains('Pete'))
print("'Anna' is in the Hash Table:", contains('Anna'))
```

**Expected Output:**
```
'Pete' is in the Hash Table: True
'Anna' is in the Hash Table: False
```

Notice: we go directly to index 8 to check for "Pete" — no looping needed!

#### Step 5: Handling Collisions with Chaining

What happens when two names have the same hash code? This is a **collision**.

Let's try adding "Stuart":
- 'S' = 83, 't' = 116, 'u' = 117, 'a' = 97, 'r' = 114, 't' = 116
- 83+116+117+97+114+116 = 643
- 643 % 10 = 3

But "Lisa" is already at index 3! This is a collision.

The solution is **chaining**: make each bucket hold a list so multiple items can share the same index.

```python
# Redesign: each bucket is now an empty list instead of None
my_list = [[], [], [], [], [], [], [], [], [], []]

def hash_function(value):
    sum_of_chars = 0
    for char in value:
        sum_of_chars += ord(char)
    return sum_of_chars % 10

def add(name):
    index = hash_function(name)
    my_list[index].append(name)    # append to the list at this bucket

add('Bob')
add('Pete')
add('Jones')
add('Lisa')
add('Siri')
add('Stuart')   # this collides with Lisa but now they share bucket 3

print(my_list)
```

**Expected Output:**
```
[[], ['Jones'], [], ['Lisa', 'Stuart'], [], ['Bob'], [], ['Siri'], ['Pete'], []]
```

"Lisa" and "Stuart" now share bucket 3. When searching for "Stuart", we go to bucket 3 and then scan the small list — much faster than searching the entire table.

### The Complete Hash Table Picture

```python
# Complete Hash Table with chaining

my_list = [[], [], [], [], [], [], [], [], [], []]

def hash_function(value):
    sum_of_chars = 0
    for char in value:
        sum_of_chars += ord(char)
    return sum_of_chars % 10

def add(name):
    index = hash_function(name)
    my_list[index].append(name)

def contains(name):
    index = hash_function(name)
    return name in my_list[index]   # check the list at this bucket

# Add some names
add('Bob')
add('Pete')
add('Jones')
add('Lisa')
add('Siri')
add('Stuart')

# Look up names
print("Contains 'Bob':", contains('Bob'))
print("Contains 'Anna':", contains('Anna'))
print("Contains 'Stuart':", contains('Stuart'))
print("Full table:", my_list)
```

**Expected Output:**
```
Contains 'Bob': True
Contains 'Anna': False
Contains 'Stuart': True
Full table: [[], ['Jones'], [], ['Lisa', 'Stuart'], [], ['Bob'], [], ['Siri'], ['Pete'], []]
```

### Time Complexity Comparison

| Operation | Array/List | Hash Table (average) |
|---|---|---|
| Search | O(n) | O(1) |
| Insert | O(1) (at end) | O(1) |
| Delete | O(n) | O(1) |

> **Best use cases for Hash Tables:** checking membership (is "Bob" in the list?), storing key-value pairs (name → phone number), and counting occurrences (how many times does each word appear?).

> **Fun fact:** Python's built-in `dict` (dictionary) and `set` are implemented using hash tables! Every time you write `my_dict["Bob"] = 42`, Python is using a hash function behind the scenes.

---

## Guided Practice Exercises

### Exercise 1: Sort Student Scores with Merge Sort

**Objective:** Use Merge Sort to rank students from lowest to highest score.

**Scenario:** A teacher has recorded exam scores for 8 students. She wants them sorted so she can assign grades fairly.

**Steps:**

1. Define the `mergeSort` and `merge` functions from earlier.
2. Create a list of student scores.
3. Sort them using Merge Sort.
4. Print the sorted scores.

**Starter Code:**

```python
def mergeSort(arr):
    if len(arr) <= 1:
        return arr
    mid = len(arr) // 2
    leftHalf = arr[:mid]
    rightHalf = arr[mid:]
    sortedLeft = mergeSort(leftHalf)
    sortedRight = mergeSort(rightHalf)
    return merge(sortedLeft, sortedRight)

def merge(left, right):
    result = []
    i = j = 0
    while i < len(left) and j < len(right):
        if left[i] < right[j]:
            result.append(left[i])
            i += 1
        else:
            result.append(right[j])
            j += 1
    result.extend(left[i:])
    result.extend(right[j:])
    return result

# Student scores (unsorted)
scores = [72, 45, 88, 63, 91, 55, 38, 79]
sorted_scores = mergeSort(scores)
print("Sorted scores:", sorted_scores)
```

**Expected Output:**
```
Sorted scores: [38, 45, 55, 63, 72, 79, 88, 91]
```

**Self-check Questions:**
- How many times did the list split before reaching single elements?
- What would happen if you added a score of 100? Where would it appear?
- Could you modify the code to sort from highest to lowest?

---

### Exercise 2: Browser History with a Stack

**Objective:** Simulate a simple web browser's back button using a Stack.

**Scenario:** A user visits websites one after another. They can press "Back" to return to the previous page.

```python
class Stack:
    def __init__(self):
        self.stack = []

    def push(self, element):
        self.stack.append(element)

    def pop(self):
        if self.isEmpty():
            return "No more history"
        return self.stack.pop()

    def peek(self):
        if self.isEmpty():
            return "No pages visited"
        return self.stack[-1]

    def isEmpty(self):
        return len(self.stack) == 0

    def size(self):
        return len(self.stack)


# Simulate browser history
history = Stack()

# User visits pages
history.push("google.com")
history.push("wikipedia.org")
history.push("python.org")
history.push("w3schools.com")

print("Currently on:", history.peek())
print("Pages in history:", history.size())

# User presses back button 2 times
print("\nPressing back...")
print("Left:", history.pop())
print("Pressing back...")
print("Left:", history.pop())
print("Currently on:", history.peek())
```

**Expected Output:**
```
Currently on: w3schools.com
Pages in history: 4

Pressing back...
Left: w3schools.com
Pressing back...
Left: python.org
Currently on: wikipedia.org
```

**Self-check Questions:**
- Why is a Stack the perfect data structure for browser history?
- What would happen if you pressed back when `isEmpty()` returns True?
- How would you add a "forward" button?

---

### Exercise 3: Print Queue Simulation

**Objective:** Simulate an office printer queue using a Queue.

**Scenario:** Three employees send documents to print. The printer processes them in order of arrival.

```python
class Queue:
    def __init__(self):
        self.queue = []

    def enqueue(self, element):
        self.queue.append(element)

    def dequeue(self):
        if self.isEmpty():
            return "Queue is empty"
        return self.queue.pop(0)

    def peek(self):
        if self.isEmpty():
            return "Nothing queued"
        return self.queue[0]

    def isEmpty(self):
        return len(self.queue) == 0

    def size(self):
        return len(self.queue)


printer_queue = Queue()

# Employees send documents to print
printer_queue.enqueue("Alice's Report (5 pages)")
printer_queue.enqueue("Bob's Invoice (2 pages)")
printer_queue.enqueue("Carol's Presentation (10 pages)")

print("Printer queue:", printer_queue.queue)
print("Documents waiting:", printer_queue.size())

# Printer processes documents one by one
print("\nPrinting:", printer_queue.dequeue())
print("Printing:", printer_queue.dequeue())
print("Documents remaining:", printer_queue.size())
print("Next up:", printer_queue.peek())
```

**Expected Output:**
```
Printer queue: ["Alice's Report (5 pages)", "Bob's Invoice (2 pages)", "Carol's Presentation (10 pages)"]
Documents waiting: 3

Printing: Alice's Report (5 pages)
Printing: Bob's Invoice (2 pages)
Documents remaining: 1
Next up: Carol's Presentation (10 pages)
```

---

### Exercise 4: Phone Book with a Hash Table

**Objective:** Create a mini phone book using a hash table.

**Scenario:** Store contact names and look them up quickly.

```python
# Hash table with chaining
phone_book = [[] for _ in range(10)]   # 10 empty buckets

def hash_name(name):
    return sum(ord(c) for c in name) % 10

def add_contact(name, number):
    index = hash_name(name)
    # Check if already exists (update if so)
    for i, entry in enumerate(phone_book[index]):
        if entry[0] == name:
            phone_book[index][i] = (name, number)
            return
    phone_book[index].append((name, number))

def find_contact(name):
    index = hash_name(name)
    for entry in phone_book[index]:
        if entry[0] == name:
            return entry[1]
    return "Contact not found"

# Add contacts
add_contact("Alice", "080-111-2222")
add_contact("Bob", "080-333-4444")
add_contact("Charlie", "080-555-6666")
add_contact("Diana", "080-777-8888")

# Look up contacts
print("Alice's number:", find_contact("Alice"))
print("Bob's number:", find_contact("Bob"))
print("Eve's number:", find_contact("Eve"))
```

**Expected Output:**
```
Alice's number: 080-111-2222
Bob's number: 080-333-4444
Eve's number: Contact not found
```

---

## Mini Project: Student Grade Manager

In this project, you will build a system that:
1. Sorts student exam scores using Merge Sort
2. Uses a Stack to track the history of score entries
3. Uses a Hash Table to look up a student's score by name

### Stage 1: Setup — Define the Data Structures

```python
# ============================================================
# MERGE SORT
# ============================================================
def mergeSort(arr):
    if len(arr) <= 1:
        return arr
    mid = len(arr) // 2
    return merge(mergeSort(arr[:mid]), mergeSort(arr[mid:]))

def merge(left, right):
    result = []
    i = j = 0
    while i < len(left) and j < len(right):
        if left[i][1] <= right[j][1]:   # compare scores (index 1)
            result.append(left[i])
            i += 1
        else:
            result.append(right[j])
            j += 1
    result.extend(left[i:])
    result.extend(right[j:])
    return result

# ============================================================
# STACK (for undo history)
# ============================================================
class Stack:
    def __init__(self):
        self.stack = []
    def push(self, item):
        self.stack.append(item)
    def pop(self):
        if not self.stack:
            return None
        return self.stack.pop()
    def peek(self):
        if not self.stack:
            return None
        return self.stack[-1]
    def isEmpty(self):
        return len(self.stack) == 0

# ============================================================
# HASH TABLE (for fast name lookup)
# ============================================================
hash_table = [[] for _ in range(20)]   # 20 buckets

def hash_name(name):
    return sum(ord(c) for c in name.lower()) % 20

def ht_add(name, score):
    index = hash_name(name)
    for i, entry in enumerate(hash_table[index]):
        if entry[0] == name:
            hash_table[index][i] = (name, score)
            return
    hash_table[index].append((name, score))

def ht_lookup(name):
    index = hash_name(name)
    for entry in hash_table[index]:
        if entry[0] == name:
            return entry[1]
    return None
```

### Stage 2: Core Logic — Add Students and Scores

```python
# Data: list of (name, score) tuples
students = []
history = Stack()   # track all additions for undo

def add_student(name, score):
    student = (name, score)
    students.append(student)
    ht_add(name, score)          # also add to hash table for fast lookup
    history.push(student)        # push to history stack for undo
    print(f"Added: {name} → {score}")

def undo_last():
    if history.isEmpty():
        print("Nothing to undo.")
        return
    removed = history.pop()
    students.remove(removed)
    print(f"Undone: {removed[0]} → {removed[1]}")

# Add students
add_student("Alice", 88)
add_student("Bob", 72)
add_student("Charlie", 95)
add_student("Diana", 61)
add_student("Eve", 83)
```

**Expected Output:**
```
Added: Alice → 88
Added: Bob → 72
Added: Charlie → 95
Added: Diana → 61
Added: Eve → 83
```

### Stage 3: Enhancements — Sort, Lookup, Undo

```python
# Sort all students by score (ascending)
def show_ranked():
    ranked = mergeSort(students[:])   # sort a copy
    print("\n--- Student Rankings (Lowest to Highest) ---")
    for rank, (name, score) in enumerate(ranked, start=1):
        print(f"  {rank}. {name}: {score}")

# Look up a student's score instantly
def lookup_student(name):
    score = ht_lookup(name)
    if score is not None:
        print(f"\n{name}'s score: {score}")
    else:
        print(f"\n{name} not found.")

# Test everything
show_ranked()
lookup_student("Charlie")
lookup_student("Frank")

print("\nUndoing last entry...")
undo_last()
show_ranked()
```

**Expected Output:**
```
--- Student Rankings (Lowest to Highest) ---
  1. Diana: 61
  2. Bob: 72
  3. Eve: 83
  4. Alice: 88
  5. Charlie: 95

Charlie's score: 95

Frank not found.

Undoing last entry...
Undone: Eve → 83

--- Student Rankings (Lowest to Highest) ---
  1. Diana: 61
  2. Bob: 72
  3. Alice: 88
  4. Charlie: 95
```

### Stage 4: Reflection Questions

- Why did we use Merge Sort instead of Python's built-in `sorted()`? (Answer: to learn the algorithm!)
- Why is the hash table better than looping through `students` to find a name?
- What would happen to the undo functionality if we used a Queue instead of a Stack?
- How would you add a "top 3 students" feature?

**Optional Extension Ideas:**
- Add a `dequeue`-based print queue that prints student names in order of score
- Add letter grade assignment (A/B/C/D/F) based on score ranges
- Build a leaderboard using a sorted Linked List

---

## Common Beginner Mistakes

### Merge Sort Mistakes

**Mistake 1: Forgetting the base case**
```python
# WRONG - will run forever (infinite recursion!)
def mergeSort(arr):
    mid = len(arr) // 2
    left = mergeSort(arr[:mid])
    right = mergeSort(arr[mid:])
    return merge(left, right)
```

```python
# CORRECT - base case stops the recursion
def mergeSort(arr):
    if len(arr) <= 1:    # ← BASE CASE is essential!
        return arr
    mid = len(arr) // 2
    left = mergeSort(arr[:mid])
    right = mergeSort(arr[mid:])
    return merge(left, right)
```

**Mistake 2: Using `/` instead of `//` for the midpoint**
```python
mid = len(arr) / 2    # WRONG: gives a float like 3.5 — can't use as index
mid = len(arr) // 2   # CORRECT: gives an integer like 3
```

---

### Stack Mistakes

**Mistake 1: Accessing an empty stack**
```python
stack = []
# If you do stack[-1] or stack.pop() on an empty list, Python gives an IndexError
stack.pop()   # IndexError: pop from empty list
```

```python
# CORRECT: always check first
if stack:
    top = stack.pop()
```

**Mistake 2: Using `pop(0)` instead of `pop()` for a stack**
```python
# pop(0) removes the FIRST item — that's Queue behaviour, not Stack!
stack.pop(0)   # WRONG for a stack

# Stack removes from the END (last item = top of stack)
stack.pop()    # CORRECT
```

---

### Queue Mistakes

**Mistake 1: Confusing Queue with Stack order**
- Stack: last in, first out → `pop()` (end)
- Queue: first in, first out → `pop(0)` (beginning)

**Mistake 2: Forgetting that `pop(0)` is slow for big lists**

For production code with large queues, use Python's `collections.deque` which has O(1) removal from both ends:

```python
from collections import deque
queue = deque()
queue.append("A")       # enqueue to the right
queue.popleft()         # dequeue from the left — O(1)!
```

---

### Linked List Mistakes

**Mistake 1: Losing the head reference**
```python
# WRONG: this loses the head and you can't find the list anymore
currentNode = node1
while currentNode:
    currentNode = currentNode.next   # after the loop, currentNode is None
# node1 still points to the first node — you didn't lose it
# But if you wrote: node1 = node1.next inside the loop, you would lose it!
```

**Mistake 2: Forgetting to set `next = None` for the last node**

Every new `Node` has `next = None` by default (we set it in `__init__`). But if you reuse or rearrange nodes, always double-check that the tail's `next` is `None`.

**Mistake 3: Deleting a node without adjusting pointers first**

Always link the previous node to the next node BEFORE you remove the target node. If you remove the target first, you lose the reference to the rest of the list.

---

### Hash Table Mistakes

**Mistake 1: Wrong modulo size**
```python
# If your table has 10 buckets, you MUST use % 10
# Using % 100 would give indexes 0–99 — out of range!
return sum_of_chars % 100   # WRONG if table has 10 buckets
return sum_of_chars % 10    # CORRECT
```

**Mistake 2: Not handling collisions**

If you don't handle collisions (e.g. just overwriting), you will lose data:
```python
my_list[index] = name   # If "Lisa" and "Stuart" both map to index 3,
                         # Stuart overwrites Lisa — Lisa is LOST!
```

Always use chaining (lists in each bucket) or another collision resolution strategy.

---

## Reflection Questions

Test your understanding by thinking through these:

1. If you have a list of 64 elements, how many times will Merge Sort split it before reaching single elements? *(Hint: 64 = 2⁶)*

2. You are building a "recently played songs" feature for a music app. Should you use a Stack or a Queue? Why?

3. You are managing a customer support ticket system where the oldest ticket should be resolved first. Should you use a Stack or a Queue? Why?

4. In a Linked List, why is inserting at the beginning O(1) but finding the 5th element is O(n)?

5. You look up "Alice" in a hash table and it returns `None`, but you know you added Alice. What might have gone wrong?

6. What is the difference between the `head` of a Linked List and the `head` of a Stack implemented with a Linked List?

7. Why can't you use Binary Search on a Linked List?

8. If two keys have the same hash code, are they the same key? Why or why not?

---

## Completion Checklist

Before moving to the next lesson, check off each item:

- [ ] I can explain what Merge Sort is and describe its divide-and-conquer strategy
- [ ] I can trace through a Merge Sort manually with a small list
- [ ] I can write the recursive Merge Sort implementation in Python
- [ ] I can explain what LIFO means and give a real-world example
- [ ] I can implement a Stack using a Python list and a class
- [ ] I can explain what FIFO means and give a real-world example
- [ ] I can implement a Queue using a Python list and a class
- [ ] I understand the difference between Stack (pop from end) and Queue (pop from front)
- [ ] I can describe what a Node is and how nodes link together in a Linked List
- [ ] I can traverse, delete, and insert nodes in a Linked List
- [ ] I understand the key differences between Linked Lists and Arrays
- [ ] I can explain what a hash function does and why it's useful
- [ ] I can implement a basic hash table with chaining for collision handling
- [ ] I understand why Hash Tables have O(1) average lookup time

---

## Lesson Summary

Congratulations on completing Lesson 38! Here's a compact recap of everything you learned:

**Merge Sort** is a divide-and-conquer sorting algorithm. It works by splitting a list in half repeatedly until each piece has one element, then merging the pieces back together in sorted order. It has O(n log n) time complexity — much better than simpler O(n²) algorithms for large datasets.

**Stacks** follow LIFO (Last In, First Out). The last item added is the first removed. Think of a pile of pancakes. Operations are push (add), pop (remove top), and peek (view top). Used for undo history, browser back buttons, and function call tracking.

**Queues** follow FIFO (First In, First Out). The first item added is the first removed. Think of a line at a shop. Operations are enqueue (add to back), dequeue (remove from front), and peek (view front). Used for printer queues, task scheduling, and breadth-first search.

**Linked Lists** are chains of nodes where each node stores data and a pointer to the next node. They allow efficient insertion and deletion without shifting elements, but accessing a specific element requires traversal from the head. There are three types: singly, doubly, and circular.

**Hash Tables** store data using a hash function to map keys directly to bucket positions, enabling O(1) average-time lookups, insertions, and deletions. Collisions (when two keys map to the same bucket) are handled using chaining — storing multiple values in the same bucket using a list.

| Structure | Key Principle | Python Equivalent |
|---|---|---|
| Merge Sort | Divide-and-conquer sorting | `sorted()` (uses Timsort, a variant) |
| Stack | LIFO — last in, first out | `list` with `.append()` and `.pop()` |
| Queue | FIFO — first in, first out | `collections.deque` |
| Linked List | Nodes with pointers | No direct built-in; custom class |
| Hash Table | Key → hash code → bucket | `dict` and `set` |
