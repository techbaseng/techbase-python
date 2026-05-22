---
render_with_liquid: false
title: "Lesson 39: Trees, Binary Trees, Binary Search Trees, AVL Trees, and Graphs in Python"
nav_order: 39
---

# Lesson 39: Trees, Binary Trees, Binary Search Trees, AVL Trees, and Graphs in Python

---

## Lesson Introduction

Welcome to one of the most exciting topics in Data Structures and Algorithms! In this lesson, you will learn about **Trees** and **Graphs** — two of the most powerful and widely-used data structures in computing.

You have already learned about **linear data structures**: Arrays, Linked Lists, Stacks, and Queues. In those structures, elements follow one after another in a straight line.

But what happens when your data is not a simple list? What if it has **branches**, **hierarchies**, or **relationships** that cannot be captured in a straight line?

That is exactly what **Trees** and **Graphs** solve. They let you represent data that branches out — like a family tree, a folder system on your computer, a city's road map, or even the internet itself.

By the end of this lesson, you will be able to:
- Understand what a Tree is and why it is useful
- Build and traverse Binary Trees
- Implement a Binary Search Tree (BST) with insert, search, and delete
- Understand how AVL Trees keep themselves balanced automatically
- Understand Graphs and how they are stored in memory

Let's start from the very beginning — no prior knowledge of trees or graphs is needed!

---

## Prerequisite Concepts

Before diving in, let us quickly review the concepts you already know that will help here.

**Classes and Objects:** Trees and Graphs are built using Python classes. Each "node" in a tree is an object.

**Recursion:** Many tree operations use recursion — a function that calls itself. Think of it like a set of Russian nesting dolls: you open one, and inside is a smaller version of the same thing.

**Linked Lists:** A Binary Tree works similarly to a Linked List, except instead of one "next" pointer, each node has a "left" and a "right" pointer.

If any of those sound unfamiliar, don't worry — we will explain everything as we go!

---

## Part 1: What Is a Tree?

### Understanding Trees — The Big Picture

Imagine your company's organisational chart. At the very top is the CEO. Below the CEO are vice-presidents. Below each vice-president are managers. Below each manager are employees. This is a **hierarchy** — a structure that branches downward.

That is exactly what a **Tree data structure** looks like!

A **Tree** is a data structure made of **nodes** (boxes that hold values) connected by **edges** (lines between boxes). It is called a "tree" because it looks like an upside-down tree: the root is at the top, and the branches spread downward.

```
        R          <-- This is the ROOT (the top node)
       / \
      A   B        <-- A and B are children of R
     / \ / \
    C  D E  F      <-- Leaf nodes (no children)
              \
               G   <-- G is a child of F
```

### Key Vocabulary — Explained Simply

| Word | Simple Meaning |
|---|---|
| **Node** | A box that holds a value |
| **Root** | The very top node (the starting point) |
| **Child** | A node connected below another node |
| **Parent** | The node directly above a child node |
| **Leaf** | A node with no children (at the bottom) |
| **Edge** | The line connecting two nodes |
| **Height** | The number of edges from root to the farthest leaf |
| **Subtree** | Any node plus all nodes below it |

### Why Not Just Use Arrays or Linked Lists?

Great question! Here is the honest comparison:

- **Arrays** are fast at accessing a specific element directly (e.g., element 700 in 1000 elements). But inserting or deleting requires shifting other elements in memory — slow!
- **Linked Lists** are fast at inserting and deleting. But finding an element means going through the entire list one by one — slow!
- **Trees** give you the BEST of both worlds. Accessing, inserting, and deleting can all be done **fast**, without shifting elements in memory.

### Real-World Uses of Trees

Trees appear everywhere in computing and real life:

- **File systems:** Your computer's folders and files form a tree (the root is `/` or `C:\`)
- **Databases:** Used for quick data lookup
- **Routing tables:** Networking uses trees to decide how to send data
- **Sorting and searching:** Trees make these operations super fast
- **AI game engines:** Chess and other game AIs build decision trees
- **Priority queues:** Often built using a special type of tree called a heap

---

## Part 2: Binary Trees

### What Makes a Tree "Binary"?

A **Binary Tree** is a tree where **every node has at most two children** — a **left child** and a **right child**.

The word "binary" means "two". So binary tree = each node can branch into at most two directions.

```
        R
       / \
      A   B
     / \ / \
    C  D E  F
              \
               G
```

Why is this useful? By limiting each node to at most two children, operations like searching, inserting, and deleting become much easier to program and much faster to run.

### Building a Binary Tree in Python

Let us now write code to create a Binary Tree! We will use a Python **class** for the node.

#### Step 1: Create the TreeNode class

```python
class TreeNode:
    def __init__(self, data):
        self.data = data      # The value stored in this node
        self.left = None      # Pointer to the left child (starts as nothing)
        self.right = None     # Pointer to the right child (starts as nothing)
```

**Line by line explanation:**
- `class TreeNode:` — We are defining a blueprint for a tree node
- `def __init__(self, data):` — This runs automatically when we create a new node
- `self.data = data` — Store the value passed in (like 'R' or 42)
- `self.left = None` — No left child yet (None means "nothing")
- `self.right = None` — No right child yet

#### Step 2: Create all the nodes and link them

```python
root = TreeNode('R')
nodeA = TreeNode('A')
nodeB = TreeNode('B')
nodeC = TreeNode('C')
nodeD = TreeNode('D')
nodeE = TreeNode('E')
nodeF = TreeNode('F')
nodeG = TreeNode('G')

# Connect the nodes
root.left = nodeA     # R's left child is A
root.right = nodeB    # R's right child is B

nodeA.left = nodeC    # A's left child is C
nodeA.right = nodeD   # A's right child is D

nodeB.left = nodeE    # B's left child is E
nodeB.right = nodeF   # B's right child is F

nodeF.left = nodeG    # F's left child is G

# Test: Print a specific node's value
print("root.right.left.data:", root.right.left.data)
```

**Expected Output:**
```
root.right.left.data: E
```

**Why E?**
- `root` is R
- `root.right` is B (R's right child)
- `root.right.left` is E (B's left child)
- `.data` gives us the value stored there: `E`

> **Thinking Prompt:** What would `root.right.right.left.data` print? Think about it before running the code!

---

### Types of Binary Trees

Before we move on, let us understand the different "shapes" a Binary Tree can have. These shapes matter because they affect performance.

#### Balanced Binary Tree

A **balanced** tree has at most 1 in height-difference between its left and right subtrees, for every node.

```
        11
       /  \
      7    15
     / \  /  \
    3   9 13  19
               /
              18
```
This tree is balanced — no side is much taller than the other.

#### Complete Binary Tree

A **complete** tree has all levels fully filled except possibly the last one, which is filled from left to right.

```
        11
       /  \
      7    15
     / \  /  \
    3   9 13  19
   / \  /
  2   4  8
```
All levels are full except the last, and the last fills left to right. A complete tree is also balanced.

#### Full Binary Tree

A **full** tree means every node has either 0 or 2 children — never just one.

```
      11
     /  \
    7    15
        /  \
       13  19
      /  \
     12   14
```

#### Perfect Binary Tree

A **perfect** tree has every level completely full of nodes, and all leaf nodes are at the same depth. A perfect tree is also full, complete, and balanced.

```
        11
       /  \
      7    15
     / \  /  \
    3   9 13  19
```

> **Real-world tip:** Balanced trees give you the best performance for searching and sorting. Unbalanced trees can become as slow as a Linked List. That is why AVL Trees (which we cover later) automatically stay balanced!

---

## Part 3: Binary Tree Traversal

### What Is Traversal?

**Traversal** means visiting every node in a tree exactly once, in some specific order. It is like taking a tour of every room in a building.

With a Linked List, traversal is simple — just go left to right. But with a tree, it branches! So we need rules about which direction to go first.

There are two main categories of traversal:

**Breadth First Search (BFS):** Visit all nodes on the same level (same depth) before going deeper. Like reading a book page by page.

**Depth First Search (DFS):** Go as deep as possible down one branch before exploring another branch. There are three types of DFS traversal:
- **Pre-order**
- **In-order**
- **Post-order**

Let us explore each one using this example tree:

```
        R
       / \
      A   B
     / \ / \
    C  D E  F
              \
               G
```

---

### Pre-order Traversal (Root → Left → Right)

**Pre-order** visits the current node FIRST ("pre" = before), then goes left, then goes right.

Think of it like exploring a file system: you note down the folder name first, then explore inside it.

**Order: Visit node → Go Left → Go Right**

```python
def preOrderTraversal(node):
    if node is None:       # If there is no node here, stop
        return
    print(node.data, end=", ")       # 1. Visit (print) the current node
    preOrderTraversal(node.left)     # 2. Explore the left subtree
    preOrderTraversal(node.right)    # 3. Explore the right subtree

preOrderTraversal(root)
```

**Expected Output:**
```
R, A, C, D, B, E, F, G,
```

**How does it work?**
1. Visit R → print "R"
2. Go left to A → print "A"
3. Go left to C → print "C"
4. C has no left child → return
5. C has no right child → return
6. Back at A → go right to D → print "D"
7. D has no children → return
8. Back at R → go right to B → print "B"
9. Go left to E → print "E"
10. E has no children → continue...
11. Go right to F → print "F"
12. F has left child G → print "G"

> **Real-world use:** Pre-order is used to copy or serialize a tree (saving it to a file in the right order to rebuild it later).

---

### In-order Traversal (Left → Root → Right)

**In-order** visits the left subtree first, then the current node ("in" = the node is visited "in between" the left and right subtrees), then the right subtree.

**Order: Go Left → Visit node → Go Right**

```python
def inOrderTraversal(node):
    if node is None:
        return
    inOrderTraversal(node.left)      # 1. Explore the left subtree first
    print(node.data, end=", ")       # 2. Visit (print) the current node
    inOrderTraversal(node.right)     # 3. Explore the right subtree
```

**Expected Output:**
```
C, A, D, R, E, B, G, F,
```

> **Very important fact:** When you do in-order traversal on a **Binary Search Tree**, the values always come out in **ascending (sorted) order**! This is incredibly useful.

---

### Post-order Traversal (Left → Right → Root)

**Post-order** visits the left subtree, then the right subtree, and LAST ("post" = after) visits the current node.

Think of it like cleaning up a directory: you delete files inside folders before you delete the folder itself.

**Order: Go Left → Go Right → Visit node**

```python
def postOrderTraversal(node):
    if node is None:
        return
    postOrderTraversal(node.left)    # 1. Explore the left subtree
    postOrderTraversal(node.right)   # 2. Explore the right subtree
    print(node.data, end=", ")       # 3. Visit (print) the current node LAST
```

**Expected Output:**
```
C, D, A, E, G, F, B, R,
```

> **Real-world use:** Post-order is used when deleting a tree (delete children before the parent) or evaluating mathematical expression trees.

---

### Quick Traversal Reference Table

| Traversal | Order | Output for our tree |
|---|---|---|
| Pre-order | Root → Left → Right | R, A, C, D, B, E, F, G |
| In-order | Left → Root → Right | C, A, D, R, E, B, G, F |
| Post-order | Left → Right → Root | C, D, A, E, G, F, B, R |

---

## Part 4: Binary Search Trees (BST)

### What Is a Binary Search Tree?

A **Binary Search Tree (BST)** is a special type of Binary Tree with one powerful rule:

> For every node X:
> - All values in the **left subtree** are **LESS than** X
> - All values in the **right subtree** are **GREATER than** X
> - Both left and right subtrees must also follow this same rule

Think of it like a number-guessing game. Is the number you're looking for smaller or bigger than the current number? If smaller, go left. If bigger, go right. You eliminate half the possibilities each time!

```
           13
          /  \
         7    15
        / \  /  \
       3   8 14  19
                /
               18
```

**Check the rule:**
- Node 13: All left values (3, 7, 8) < 13 ✓  All right values (14, 15, 18, 19) > 13 ✓
- Node 7: All left values (3) < 7 ✓  All right values (8) > 7 ✓
- Node 15: Left (14) < 15 ✓  Right (18, 19) > 15 ✓

### Key BST Terminology

- **Size (n):** Total number of nodes in the tree
- **Height (h):** Maximum number of edges from the root to a leaf
- **In-order successor:** The node that would come next if you did an in-order traversal. For node 13, the successor is 14 (the next higher value)

---

### BST Traversal — Proving It Is a BST

A quick way to verify that a Binary Tree is a BST: do an **in-order traversal** and check that the output is in ascending order.

```python
class TreeNode:
    def __init__(self, data):
        self.data = data
        self.left = None
        self.right = None

def inOrderTraversal(node):
    if node is None:
        return
    inOrderTraversal(node.left)
    print(node.data, end=", ")
    inOrderTraversal(node.right)

# Build the BST from the diagram above
root = TreeNode(13)
node7 = TreeNode(7)
node15 = TreeNode(15)
node3 = TreeNode(3)
node8 = TreeNode(8)
node14 = TreeNode(14)
node19 = TreeNode(19)
node18 = TreeNode(18)

root.left = node7
root.right = node15
node7.left = node3
node7.right = node8
node15.left = node14
node15.right = node19
node19.left = node18

# Traverse to verify
inOrderTraversal(root)
```

**Expected Output:**
```
3, 7, 8, 13, 14, 15, 18, 19,
```

The output is in ascending order — confirming it is a valid BST!

---

### Searching in a BST

Searching in a BST is fast because at every node, you can eliminate half the tree.

**Algorithm:**
1. Start at the root
2. If the current node equals the target → found it!
3. If the target is **less than** current node → search the **left** subtree
4. If the target is **greater than** current node → search the **right** subtree
5. If we reach `None` (an empty spot) → the value doesn't exist

```python
def search(node, target):
    if node is None:
        return None                        # Value not found
    elif node.data == target:
        return node                        # Found it!
    elif target < node.data:
        return search(node.left, target)   # Go left (smaller values)
    else:
        return search(node.right, target)  # Go right (larger values)

# Search for the value 13
result = search(root, 13)
if result:
    print(f"Found the node with value: {result.data}")
else:
    print("Value not found in the BST.")
```

**Expected Output:**
```
Found the node with value: 13
```

**Time complexity:** O(h), where h is the height of the tree. For a balanced tree, h ≈ log(n), which is very fast. For an unbalanced tree, h could be n (as slow as a list).

> **Thinking Prompt:** If you search for the value 10 in the BST above, which nodes does the algorithm visit? (Hint: it goes 13 → 7 → 8 → and then?)

---

### Inserting Into a BST

Inserting a new value works exactly like searching — but when you reach an empty spot, you place the new node there. Inserted nodes always become new leaf nodes.

```python
def insert(node, data):
    if node is None:
        return TreeNode(data)    # Create and return the new node here
    else:
        if data < node.data:
            node.left = insert(node.left, data)    # Insert in left subtree
        elif data > node.data:
            node.right = insert(node.right, data)  # Insert in right subtree
        # If data == node.data, we do nothing (no duplicates in BST)
    return node

# Insert the value 10
root = insert(root, 10)

# Verify by traversal — 10 should appear between 8 and 13
inOrderTraversal(root)
```

**Expected Output:**
```
3, 7, 8, 10, 13, 14, 15, 18, 19,
```

The value 10 was correctly placed between 8 and 13.

---

### Finding the Minimum Value in a Subtree

Before we cover deletion, we need a helper: finding the smallest value in a subtree.

**The rule is simple:** In a BST, the smallest value is always the **leftmost node**. Just keep going left until you can't anymore.

```python
def minValueNode(node):
    current = node
    while current.left is not None:    # Keep going left
        current = current.left
    return current                     # This is the minimum

print("Lowest value:", minValueNode(root).data)
```

**Expected Output:**
```
Lowest value: 3
```

We use this function during deletion to find a node's **in-order successor** (the smallest value in the right subtree).

---

### Deleting a Node in a BST

Deletion is the most complex BST operation. There are three cases:

**Case 1: The node to delete is a leaf** (no children)
→ Simply remove it. Set the parent's pointer to `None`.

**Case 2: The node has ONE child**
→ Replace the node with its one child. The parent now points to the grandchild.

**Case 3: The node has TWO children**
→ Find the node's **in-order successor** (smallest value in the right subtree). Copy that value into the current node. Then delete the successor (which will be Case 1 or Case 2).

```python
def delete(node, data):
    if node is None:
        return None

    if data < node.data:
        node.left = delete(node.left, data)       # Go left
    elif data > node.data:
        node.right = delete(node.right, data)     # Go right
    else:
        # Found the node to delete!

        # Case 1 & 2: Zero or one child
        if node.left is None:
            return node.right        # Replace with right child (or None)
        elif node.right is None:
            return node.left         # Replace with left child

        # Case 3: Two children
        # Find in-order successor (smallest in right subtree)
        successor = minValueNode(node.right)
        # Copy successor's value to this node
        node.data = successor.data
        # Delete the successor from the right subtree
        node.right = delete(node.right, successor.data)

    return node

# Delete node 15 (which has two children: 14 and 19)
root = delete(root, 15)
inOrderTraversal(root)
```

**Expected Output:**
```
3, 7, 8, 10, 13, 14, 18, 19,
```

Node 15 was replaced by 18 (its in-order successor — the smallest value in its right subtree), and then the old 18 was deleted.

---

### Balanced vs. Unbalanced BSTs

Here is a critical issue with BSTs: if you insert values in sorted order, the tree becomes "lopsided" (unbalanced), and performance degrades to O(n) — as slow as a linked list.

**Balanced BST (good):**
```
         13
        /   \
       7     15
      / \   /  \
     3   8 14   19
              /
             18
```
Height = 4. Searching takes at most 4 steps.

**Unbalanced BST (bad — if you insert 7, 13, 15, 19 in order):**
```
7
 \
  13
    \
     15
       \
        19
```
Height = 4. But with 1000 nodes, you might need 1000 steps to find anything!

This is exactly the problem that **AVL Trees** solve, coming up next.

---

## Part 5: AVL Trees — Self-Balancing Trees

### What Is an AVL Tree?

An **AVL Tree** is a Binary Search Tree that **automatically keeps itself balanced** after every insertion or deletion.

The name "AVL" comes from two Soviet inventors: Georgy **A**delson-**V**elsky and Evgenii **L**andis, who invented it in 1962.

Why does this matter? Because an AVL Tree **guarantees** that all operations (search, insert, delete) run in **O(log n)** time — even in the worst case. Regular BSTs can degrade to O(n) if the data is inserted in sorted order.

The only difference between a regular BST and an AVL Tree is that the AVL Tree performs **rotation operations** to restore balance whenever it becomes unbalanced.

**Unbalanced BST (height 6):**
```
B
 \
  G
   \
    E
     \
      K
       \
        F
         \
          P
           \
            I
             \
              M
```

**Same data as an AVL Tree (height 3):**
```
       G
      / \
     E   K
    / \ / \
   B  F I  P
           /
          M
```

Both trees contain the same data, but the AVL Tree's height is dramatically smaller!

---

### The Balance Factor

Every node in an AVL Tree keeps track of its **Balance Factor (BF)**: the difference between the heights of its right and left subtrees.

```
BF(X) = height(right subtree of X) - height(left subtree of X)
```

**Interpreting the balance factor:**
- **BF = 0:** The node is perfectly balanced
- **BF = +1:** The right side is one taller (acceptable)
- **BF = -1:** The left side is one taller (acceptable)
- **BF ≥ +2:** Too right-heavy → must rotate to fix!
- **BF ≤ -2:** Too left-heavy → must rotate to fix!

An AVL Tree checks and updates balance factors after every insert or delete. If any node has a balance factor outside [-1, 1], rotations are performed.

---

### Left and Right Rotations

**Rotations** are the mechanism AVL Trees use to fix imbalance. They rearrange nodes while keeping the BST property (left < parent < right) intact.

Think of a rotation like a "pivot": you take a node and rotate the tree around it.

#### Right Rotation (fixes left-heavy imbalance)

```
Before (left-heavy, BF = -2):
      Z
     /
    Y
   /
  X

After right rotation at Z:
    Y
   / \
  X   Z
```

#### Left Rotation (fixes right-heavy imbalance)

```
Before (right-heavy, BF = +2):
  X
   \
    Y
     \
      Z

After left rotation at X:
    Y
   / \
  X   Z
```

---

### The Four Out-of-Balance Cases

When a tree becomes unbalanced, there are exactly **four cases**, each requiring a specific fix:

| Case | Description | Fix |
|---|---|---|
| **Left-Left (LL)** | Unbalanced node AND its left child are both left-heavy (BF negative) | Single **right** rotation |
| **Right-Right (RR)** | Unbalanced node AND its right child are both right-heavy (BF positive) | Single **left** rotation |
| **Left-Right (LR)** | Unbalanced node is left-heavy, but its left child is right-heavy | First **left rotate** the left child, then **right rotate** the unbalanced node |
| **Right-Left (RL)** | Unbalanced node is right-heavy, but its right child is left-heavy | First **right rotate** the right child, then **left rotate** the unbalanced node |

**Simple way to remember:** If both the problem node and its heavy child lean the same direction → single rotation. If they lean in opposite directions → double rotation (fix the child first, then the node).

---

### AVL Tree Implementation in Python

Now let's put it all together. This is a complete AVL Tree implementation with insertion, deletion, and automatic rebalancing.

```python
class AVLNode:
    def __init__(self, data):
        self.data = data
        self.left = None
        self.right = None
        self.height = 1    # NEW: AVL nodes track their own height

class AVLTree:

    def getHeight(self, node):
        """Returns the height of a node (0 if None)."""
        if node is None:
            return 0
        return node.height

    def getBalanceFactor(self, node):
        """Calculates the balance factor of a node."""
        if node is None:
            return 0
        return self.getHeight(node.right) - self.getHeight(node.left)

    def updateHeight(self, node):
        """Recalculates height from children."""
        node.height = 1 + max(self.getHeight(node.left), self.getHeight(node.right))

    def rotateRight(self, z):
        """Performs a right rotation around node z."""
        y = z.left          # y is the left child of z
        T3 = y.right        # T3 is y's right subtree

        # Perform the rotation
        y.right = z         # z becomes y's right child
        z.left = T3         # T3 moves to be z's left child

        # Update heights (z first, then y, since y is now higher)
        self.updateHeight(z)
        self.updateHeight(y)

        return y            # y is the new root of this subtree

    def rotateLeft(self, z):
        """Performs a left rotation around node z."""
        y = z.right         # y is the right child of z
        T2 = y.left         # T2 is y's left subtree

        # Perform the rotation
        y.left = z          # z becomes y's left child
        z.right = T2        # T2 moves to be z's right child

        # Update heights
        self.updateHeight(z)
        self.updateHeight(y)

        return y            # y is the new root of this subtree

    def rebalance(self, node):
        """Checks balance and rotates if needed."""
        self.updateHeight(node)
        bf = self.getBalanceFactor(node)

        # Left-Left case (too left-heavy, left child is also left-heavy)
        if bf < -1 and self.getBalanceFactor(node.left) <= 0:
            return self.rotateRight(node)

        # Right-Right case (too right-heavy, right child is also right-heavy)
        if bf > 1 and self.getBalanceFactor(node.right) >= 0:
            return self.rotateLeft(node)

        # Left-Right case (left-heavy, but left child is right-heavy)
        if bf < -1 and self.getBalanceFactor(node.left) > 0:
            node.left = self.rotateLeft(node.left)   # Fix child first
            return self.rotateRight(node)

        # Right-Left case (right-heavy, but right child is left-heavy)
        if bf > 1 and self.getBalanceFactor(node.right) < 0:
            node.right = self.rotateRight(node.right) # Fix child first
            return self.rotateLeft(node)

        return node  # Already balanced

    def insert(self, node, data):
        """Inserts data like a regular BST, then rebalances."""
        if node is None:
            return AVLNode(data)
        if data < node.data:
            node.left = self.insert(node.left, data)
        elif data > node.data:
            node.right = self.insert(node.right, data)
        else:
            return node   # Duplicate values not allowed

        return self.rebalance(node)

    def inOrder(self, node):
        """In-order traversal to verify BST order."""
        if node is None:
            return
        self.inOrder(node.left)
        print(node.data, end=", ")
        self.inOrder(node.right)


# Demo: Build an AVL tree that would be unbalanced as a regular BST
avl = AVLTree()
root = None

# Insert values in sorted order — a regular BST would become a straight line
for val in [10, 20, 30, 40, 50, 25]:
    root = avl.insert(root, val)

print("In-order traversal (should be sorted):")
avl.inOrder(root)
print()
print("Root value (should be near middle due to balancing):", root.data)
```

**Expected Output:**
```
In-order traversal (should be sorted):
10, 20, 25, 30, 40, 50,
Root value (should be near middle due to balancing): 30
```

Even though we inserted values 10 → 20 → 30 → 40 → 50 → 25 in an order that would make a regular BST into a long chain, the AVL Tree kept itself balanced, with 30 at the root!

---

### Retracing After Insertion or Deletion

After every insert or delete, the AVL Tree "retraces" its steps back up to the root, updating heights and fixing any imbalances it finds along the way. This is handled automatically through recursion.

If node H is unbalanced, the algorithm fixes H first. After the rotation at H, nodes higher up (like E and C) often find they are now balanced too — so fixing one often fixes many.

---

## Part 6: Graphs

### What Is a Graph?

A **Graph** is a data structure made of **vertices** (also called nodes) and **edges** (connections between vertices).

Think of a graph like a city map: the cities are vertices, and the roads connecting them are edges. Or think of social media: each person is a vertex, and friendships are edges.

```
    F
   2|4
  B   C
  |     \
  A   E  D
  |    \ /
  G     D
```

Unlike a Tree, a Graph has **no root** and **no parent-child hierarchy**. Any vertex can connect to any other vertex. There can even be cycles (paths that loop back to where you started).

### Why Are Graphs So Important?

Graphs model almost every real-world network:

- **Social networks:** Facebook, Instagram, LinkedIn — people (vertices) connected by friendships (edges)
- **Maps and GPS:** Locations (vertices) connected by roads (edges). Shortest path algorithms find the fastest route
- **The internet:** Web pages (vertices) connected by hyperlinks (edges)
- **Biology:** Neural networks, protein interactions, disease spread
- **Logistics:** Delivery networks, supply chains

### Key Graph Vocabulary

| Term | Meaning |
|---|---|
| **Vertex (Node)** | A point/object in the graph |
| **Edge** | A connection between two vertices |
| **Adjacent (Neighbors)** | Two vertices that share an edge |
| **Directed Graph** | Edges have a direction (one-way roads) |
| **Undirected Graph** | Edges go both ways (two-way roads) |
| **Weighted Graph** | Edges have weights/costs (like road distances) |

---

### Graph Representations — How to Store a Graph in Python

A Graph is not as simple to store in memory as a list or tree. We need a special structure. There are two main ways:

---

#### Method 1: Adjacency Matrix

An **Adjacency Matrix** is a 2D table (grid) where the row number represents the "from" vertex and the column number represents the "to" vertex.

If there is an edge from vertex `i` to vertex `j`, we put a `1` (or the edge weight) in cell `[i][j]`.

**Example: Simple undirected graph with 4 vertices A, B, C, D**

```
Edges: A-B, A-C, A-D, B-C
```

```
   A  B  C  D
A [0, 1, 1, 1]
B [1, 0, 1, 0]
C [1, 1, 0, 0]
D [1, 0, 0, 0]
```

Notice the matrix is **symmetric** for undirected graphs (if A connects to B, then B connects to A).

**For a weighted, directed graph** (e.g., A→B with weight 3, A→D with weight 2, B→C with weight 1, D→A with weight 4):

```
   A  B  C  D
A [0, 3, 0, 2]
B [0, 0, 1, 0]
C [0, 0, 0, 0]
D [4, 0, 0, 0]
```

**Python implementation:**

```python
# Adjacency matrix for an undirected graph
# Vertices: A=0, B=1, C=2, D=3

size = 4
adj_matrix = [[0] * size for _ in range(size)]   # Create a 4x4 grid of zeros

def add_edge(matrix, u, v, weight=1, directed=False):
    """Add an edge from vertex u to vertex v."""
    matrix[u][v] = weight
    if not directed:
        matrix[v][u] = weight    # For undirected, add both directions

# Add edges (using index numbers: A=0, B=1, C=2, D=3)
add_edge(adj_matrix, 0, 1)   # A-B
add_edge(adj_matrix, 0, 2)   # A-C
add_edge(adj_matrix, 0, 3)   # A-D
add_edge(adj_matrix, 1, 2)   # B-C

# Print the adjacency matrix
print("Adjacency Matrix:")
print("   A  B  C  D")
labels = ['A', 'B', 'C', 'D']
for i, row in enumerate(adj_matrix):
    print(f"{labels[i]} {row}")
```

**Expected Output:**
```
Adjacency Matrix:
   A  B  C  D
A [0, 1, 1, 1]
B [1, 0, 1, 0]
C [1, 1, 0, 0]
D [1, 0, 0, 0]
```

**Pros of Adjacency Matrix:** Simple to implement. Checking if an edge exists between two specific vertices is O(1) — instant!
**Cons:** Uses a LOT of memory if the graph has many vertices but few edges (most cells will be 0).

---

#### Method 2: Adjacency List

An **Adjacency List** stores each vertex with a list of all its neighbors. This is much more memory-efficient for "sparse" graphs (graphs where most vertices are not connected to each other).

**Python implementation:**

```python
# Adjacency list for the same graph using a dictionary
adj_list = {
    'A': ['B', 'C', 'D'],
    'B': ['A', 'C'],
    'C': ['A', 'B'],
    'D': ['A']
}

def add_edge_list(graph, u, v, directed=False):
    """Add an edge to the adjacency list."""
    if u not in graph:
        graph[u] = []
    graph[u].append(v)
    if not directed:
        if v not in graph:
            graph[v] = []
        graph[v].append(u)

# Build a new graph
graph = {}
add_edge_list(graph, 'A', 'B')
add_edge_list(graph, 'A', 'C')
add_edge_list(graph, 'A', 'D')
add_edge_list(graph, 'B', 'C')

print("Adjacency List:")
for vertex, neighbors in graph.items():
    print(f"  {vertex}: {neighbors}")
```

**Expected Output:**
```
Adjacency List:
  A: ['B', 'C', 'D']
  B: ['A', 'C']
  C: ['A', 'B']
  D: ['A']
```

**For a directed, weighted graph** — store tuples `(neighbor, weight)`:

```python
weighted_directed = {
    'A': [('B', 3), ('D', 2)],   # A→B with weight 3, A→D with weight 2
    'B': [('C', 1)],              # B→C with weight 1
    'C': [],                       # C has no outgoing edges
    'D': [('A', 4)]               # D→A with weight 4
}

print("Weighted Directed Adjacency List:")
for vertex, edges in weighted_directed.items():
    print(f"  {vertex}: {edges}")
```

**Expected Output:**
```
Weighted Directed Adjacency List:
  A: [('B', 3), ('D', 2)]
  B: [('C', 1)]
  C: []
  D: [('A', 4)]
```

**Pros of Adjacency List:** Memory-efficient for sparse graphs. Easy to iterate over all neighbors of a vertex.
**Cons:** Checking if a specific edge exists requires scanning the neighbor list — O(degree) time.

---

### Which Representation Should You Use?

| Situation | Recommended Representation |
|---|---|
| Dense graph (many edges) | Adjacency Matrix |
| Sparse graph (few edges) | Adjacency List |
| Need to quickly check if edge (u,v) exists | Adjacency Matrix |
| Need to iterate over all neighbors of a vertex | Adjacency List |
| This tutorial going forward | **Adjacency Matrix** (simpler to understand) |

---

## Part 7: Guided Practice Exercises

### Exercise 1: Build and Traverse a BST

**Objective:** Create a Binary Search Tree and verify it using in-order traversal.

**Scenario:** You are building a student grade lookup system. Each student has an ID number. You want to store them in a BST for fast lookup.

**Steps:**
1. Create a `TreeNode` class with `data`, `left`, and `right`
2. Create an `insert()` function
3. Insert these student IDs in this order: `50, 30, 70, 20, 40, 60, 80`
4. Perform in-order traversal to verify the tree is a valid BST

```python
class TreeNode:
    def __init__(self, data):
        self.data = data
        self.left = None
        self.right = None

def insert(node, data):
    if node is None:
        return TreeNode(data)
    if data < node.data:
        node.left = insert(node.left, data)
    elif data > node.data:
        node.right = insert(node.right, data)
    return node

def inOrder(node):
    if node is None:
        return
    inOrder(node.left)
    print(node.data, end=", ")
    inOrder(node.right)

# Build the BST
root = None
for val in [50, 30, 70, 20, 40, 60, 80]:
    root = insert(root, val)

print("In-order traversal:")
inOrder(root)
```

**Expected Output:**
```
In-order traversal:
20, 30, 40, 50, 60, 70, 80,
```

**Self-check questions:**
- Is the output in ascending order? (It should be!)
- What is the root of this tree? (Hint: it is the first value inserted)
- What would happen if you inserted the values in sorted order (20, 30, 40, ...)?

---

### Exercise 2: BST Search

**Objective:** Search for values in your BST.

**Steps:** Using the BST from Exercise 1, search for student IDs 40 and 55.

```python
def search(node, target):
    if node is None:
        return None
    elif node.data == target:
        return node
    elif target < node.data:
        return search(node.left, target)
    else:
        return search(node.right, target)

# Search for ID 40 (should be found)
result = search(root, 40)
print("Search for 40:", "Found!" if result else "Not found")

# Search for ID 55 (should NOT be found)
result = search(root, 55)
print("Search for 55:", "Found!" if result else "Not found")
```

**Expected Output:**
```
Search for 40: Found!
Search for 55: Not found
```

---

### Exercise 3: Build a Graph with Adjacency Matrix

**Objective:** Model a simple city road network as a graph.

**Scenario:** A city has 5 locations: Airport (0), Mall (1), Hospital (2), School (3), Park (4). The roads are: Airport↔Mall, Mall↔Hospital, Hospital↔School, School↔Park, Mall↔Park.

```python
# Build adjacency matrix for 5 vertices
size = 5
graph = [[0] * size for _ in range(size)]

edges = [(0,1), (1,2), (2,3), (3,4), (1,4)]   # (from, to) pairs

for u, v in edges:
    graph[u][v] = 1
    graph[v][u] = 1   # Undirected

labels = ['Airport', 'Mall', 'Hospital', 'School', 'Park']

print("City Road Network (Adjacency Matrix):")
print("         ", " ".join(f"{l[:4]:>6}" for l in labels))
for i, row in enumerate(graph):
    print(f"{labels[i][:8]:>8}:", row)
```

**Expected Output:**
```
City Road Network (Adjacency Matrix):
          Airp   Mall   Hosp   Scho   Park
 Airport: [0, 1, 0, 0, 0]
    Mall: [1, 0, 1, 0, 1]
Hospital: [0, 1, 0, 1, 0]
  School: [0, 0, 1, 0, 1]
    Park: [0, 1, 0, 1, 0]
```

**Self-check questions:**
- Is the matrix symmetric? (It should be for an undirected graph)
- How many roads does the Mall have? (Count the 1s in the Mall row)
- What would you change to make this a **directed** graph (one-way roads)?

---

## Part 8: Mini-Project — Student Records BST with Search and Report

### Project Brief

You will build a small student record system using a BST. Each student has an ID and a name. The system supports inserting students, searching by ID, and printing all students in sorted order by ID.

### Stage 1: Setup — Define the Student Node

```python
class StudentNode:
    def __init__(self, student_id, name):
        self.student_id = student_id
        self.name = name
        self.left = None
        self.right = None
```

### Stage 2: Core Logic — Insert and Search

```python
def insert_student(node, student_id, name):
    if node is None:
        return StudentNode(student_id, name)
    if student_id < node.student_id:
        node.left = insert_student(node.left, student_id, name)
    elif student_id > node.student_id:
        node.right = insert_student(node.right, student_id, name)
    return node

def search_student(node, student_id):
    if node is None:
        return None
    if node.student_id == student_id:
        return node
    elif student_id < node.student_id:
        return search_student(node.left, student_id)
    else:
        return search_student(node.right, student_id)

def print_all_students(node):
    """In-order traversal to print all students sorted by ID."""
    if node is None:
        return
    print_all_students(node.left)
    print(f"  ID: {node.student_id} | Name: {node.name}")
    print_all_students(node.right)
```

### Stage 3: Build and Use the System

```python
# Build the student database
root = None
students_data = [
    (1045, "Amina"),
    (1023, "Babatunde"),
    (1067, "Chisom"),
    (1011, "David"),
    (1089, "Emeka"),
    (1034, "Fatima"),
]

for sid, name in students_data:
    root = insert_student(root, sid, name)

print("=== ALL STUDENTS (sorted by ID) ===")
print_all_students(root)

# Search for a student
print("\n=== SEARCH ===")
found = search_student(root, 1034)
if found:
    print(f"Found: ID {found.student_id} - {found.name}")
else:
    print("Student not found.")

# Search for a non-existent student
not_found = search_student(root, 9999)
print("Search for 9999:", "Found" if not_found else "Not in database")
```

**Expected Output:**
```
=== ALL STUDENTS (sorted by ID) ===
  ID: 1011 | Name: David
  ID: 1023 | Name: Babatunde
  ID: 1034 | Name: Fatima
  ID: 1045 | Name: Amina
  ID: 1067 | Name: Chisom
  ID: 1089 | Name: Emeka

=== SEARCH ===
Found: ID 1034 - Fatima
Search for 9999: Not in database
```

**Milestone Output:** All students are printed in ascending order by ID — confirming the BST is valid!

**Reflection Questions:**
- How many comparisons does it take to find Fatima (ID 1034) in this BST?
- What happens if you insert all students in ID order 1011, 1023, ... (sorted)? Draw what the tree looks like. Would it still be efficient?
- How would you add a `delete_student()` function?

**Optional Extension:** Add a grade field to each student and a function that finds and prints students with a grade above a threshold.

---

## Part 9: Common Beginner Mistakes

### Mistake 1: Forgetting to return the node in recursive BST functions

```python
# WRONG — the return value is lost!
def insert(node, data):
    if node is None:
        return TreeNode(data)
    if data < node.data:
        insert(node.left, data)   # ❌ Missing return!
    else:
        insert(node.right, data)  # ❌ Missing return!
    return node

# CORRECT
def insert(node, data):
    if node is None:
        return TreeNode(data)
    if data < node.data:
        node.left = insert(node.left, data)   # ✅ Assign the return!
    else:
        node.right = insert(node.right, data) # ✅ Assign the return!
    return node
```

Without `return`, the new node is created but never connected to the tree. The tree appears empty!

---

### Mistake 2: Forgetting to update the root variable

```python
root = TreeNode(10)

# WRONG — root is not updated!
insert(root, 20)   # ❌ The result is discarded

# CORRECT — always assign the return value back to root
root = insert(root, 20)   # ✅
```

---

### Mistake 3: Treating a tree as a list

A beginner sometimes tries to iterate over a tree like a list using a `for` loop directly. Trees are not iterable by default. You must always use a traversal function.

```python
# WRONG
for node in root:   # ❌ This will cause an error
    print(node.data)

# CORRECT
inOrderTraversal(root)   # ✅ Use a traversal function
```

---

### Mistake 4: Confusing tree height and tree size

- **Size:** The total number of nodes (e.g., a tree with 7 nodes has size 7)
- **Height:** The number of edges on the longest path from root to a leaf

A common mistake is using the wrong term when discussing performance. Time complexity usually depends on **height**, not size.

---

### Mistake 5: Making an Adjacency Matrix the wrong size

```python
# WRONG — matrix is too small
size = 3
graph = [[0] * size for _ in range(size)]   # Only 3x3
graph[3][0] = 1   # ❌ Index out of range error!

# CORRECT — make sure size matches your vertex count
size = 5   # If you have 5 vertices (indexed 0 to 4)
graph = [[0] * size for _ in range(size)]
```

---

### Mistake 6: Forgetting that BST values must be unique

Standard BSTs do not allow duplicate values. Inserting a duplicate is simply ignored by the standard `insert()` function. If your application needs duplicates, you need a modified BST.

---

## Part 10: Reflection Questions

Answer these to test your understanding:

1. You have 1,000 employees in a sorted BST. How many comparisons do you need in the worst case to find one employee? (Hint: think about the height of a balanced BST)

2. What is the difference between a Binary Tree and a Binary Search Tree?

3. What problem does an AVL Tree solve that a regular BST does not?

4. If you perform in-order traversal on a valid BST, what property will the output always have?

5. Your company wants to model employee connections (who works with whom). Which data structure would you use — a Tree or a Graph? Why?

6. You have a social network with 10 million users but each user has on average only 200 friends. Would you prefer an Adjacency Matrix or an Adjacency List? Why?

7. What are the four AVL rotation cases, and when does each one apply?

8. Why does inserting values in sorted order (1, 2, 3, 4, 5...) into a regular BST create such a serious performance problem?

---

## Completion Checklist

Go through this checklist before moving to the next lesson:

- [ ] I understand what a Tree data structure is and how it differs from a list
- [ ] I know the key tree vocabulary: root, node, leaf, edge, height, subtree
- [ ] I can explain what makes a Binary Tree "binary"
- [ ] I know the four types of Binary Trees: balanced, complete, full, perfect
- [ ] I can implement and explain Pre-order, In-order, and Post-order traversal
- [ ] I understand the BST property (left < parent < right)
- [ ] I can implement BST insert, search, and delete in Python
- [ ] I understand what balance factor means in an AVL Tree
- [ ] I can identify the four AVL rotation cases (LL, RR, LR, RL)
- [ ] I understand what a Graph is and how it differs from a Tree
- [ ] I can represent a Graph using an Adjacency Matrix
- [ ] I can represent a Graph using an Adjacency List
- [ ] I understand when to use each graph representation
- [ ] I completed the mini-project successfully

---

## Lesson Summary

You have covered a tremendous amount of ground in this lesson! Here is what you learned:

**Trees** are hierarchical, non-linear data structures. Unlike arrays and linked lists, trees branch in multiple directions, making them fast for both accessing and modifying data.

**Binary Trees** limit each node to at most two children (left and right). You learned three traversal methods: Pre-order (root first), In-order (root in middle), and Post-order (root last). In-order traversal of a BST always produces a sorted sequence.

**Binary Search Trees (BSTs)** add an ordering rule: all left descendants are smaller, all right descendants are larger. This makes search, insert, and delete all O(h) — fast when the tree is balanced, slow when it is not.

**AVL Trees** are self-balancing BSTs. They store a balance factor at every node and perform rotations (single or double) to keep the tree balanced after every change, guaranteeing O(log n) performance always.

**Graphs** are the most general data structure, representing any network of objects and their relationships. Vertices are the objects; edges are the connections. Graphs can be directed or undirected, weighted or unweighted. They are stored either as an Adjacency Matrix (a 2D grid — great for dense graphs and instant edge lookup) or an Adjacency List (a dictionary of neighbor lists — great for sparse graphs and memory efficiency).

These data structures are the backbone of databases, GPS navigation, social networks, compilers, machine learning, and nearly every sophisticated software system you will ever encounter.

---

*Sources: W3Schools Python DSA — Trees, Binary Trees, Binary Search Trees, AVL Trees, Graphs*
