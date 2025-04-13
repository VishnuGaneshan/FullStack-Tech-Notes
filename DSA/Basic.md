[Back to DSA Home Page](./README.md#)

## 🟢 Basic Topics 🧠🔍📘

Start here if you're new or want to strengthen your foundation:

- [What is DSA?](#what-is-dsa)
- [Time & Space Complexity (Big O Notation)](#time--space-complexity-big-o-notation)
- [Recursion](#recursion)
- [Arrays](#arrays)
- [Strings](#strings)
- [Linked Lists (Singly & Doubly)](#linked-lists-singly--doubly)
- [Stack](#stack)
- [Queue (Normal, Circular, Deque)](#queue-normal-circular-deque)
- [Hashing (Hash Tables, Hash Maps)](#hashing-hash-tables-hash-maps)
- [Searching Algorithms](#searching-algorithms)
  - [Linear Search](#linear-search)
  - [Binary Search](#binary-search)

---

### **What is DSA?**

**Data Structures and Algorithms (DSA)** are the building blocks of computer science. They help in organizing data efficiently and solving problems optimally.

#### 🔹 **Data Structures**:
- 📂 **Definition**: Ways to organize and store data.
- 🛠️ **Examples**: Arrays, Linked Lists, Stacks, Queues, Trees, Graphs.

#### 🔹 **Algorithms**:
- 📜 **Definition**: Step-by-step procedures to solve problems.
- 🛠️ **Examples**: Searching, Sorting, Pathfinding.

#### 🔹 Why Learn DSA?
- 🧠 **Problem Solving**: Improves logical thinking.
- 🚀 **Efficiency**: Helps write optimized code.
- 💼 **Career Growth**: Essential for coding interviews.

[Back to Top](#)

---

### **Time & Space Complexity (Big O Notation)**

**Big O Notation** describes the performance of an algorithm in terms of time and space as the input size grows.

#### 🔹 **Time Complexity**:
- ⏱️ Measures how the runtime of an algorithm changes with input size.
- Common complexities:
  - **O(1)**: Constant time (e.g., accessing an array element).
  - **O(log n)**: Logarithmic time (e.g., Binary Search).
  - **O(n)**: Linear time (e.g., Linear Search).
  - **O(n²)**: Quadratic time (e.g., Nested loops).

#### 🔹 **Space Complexity**:
- 💾 Measures the memory used by an algorithm.
- Includes:
  - **Input space**: Memory for input data.
  - **Auxiliary space**: Extra memory used during execution.

#### 🔹 Example:
```cpp
// O(n) Time Complexity
void printElements(vector<int>& arr) {
    for (int element : arr) {
        cout << element << " ";
    }
    cout << endl;
}

// O(1) Space Complexity
```

[Back to Top](#)

---

### **Recursion**

**Recursion** is a technique where a function calls itself to solve smaller subproblems.

#### 🔹 Key Components:
1. 🛑 **Base Case**: Stops the recursion.
2. 🔄 **Recursive Case**: Reduces the problem size.

#### 🔹 Example: Factorial
```cpp
int factorial(int n) {
    if (n == 0) return 1; // Base case
    return n * factorial(n - 1); // Recursive case
}

cout << factorial(5); // Output: 120
```

#### 🔹 Advantages:
- ✨ Simplifies complex problems (e.g., Tree Traversals).
- 📉 Reduces code size.

#### 🔹 Disadvantages:
- ⚠️ Can lead to **stack overflow** if not handled properly.
- 💾 Higher memory usage due to recursive calls.

[Back to Top](#)

---

### **Arrays**

An **array** is a collection of elements stored at contiguous memory locations.

#### 🔹 Key Features:
- 📏 Fixed size.
- ⚡ Random access using indices.
- 🛠️ Stores elements of the same data type.

#### 🔹 Operations:
1. **Access**: O(1)
   ```cpp
   int arr[] = {10, 20, 30};
   cout << arr[1]; // Output: 20
   ```
2. **Insertion**: O(n) (shifting elements).
3. **Deletion**: O(n) (shifting elements).

#### 🔹 Use Cases:
- 📂 Storing data in a linear structure.
- 🛠️ Implementing other data structures (e.g., Stacks, Queues).

[Back to Top](#)

---

### **Strings**

A **string** is a sequence of characters.

#### 🔹 Key Features:
- 🔒 Mutable or immutable depending on the language.
- 🔢 Supports indexing and slicing.

#### 🔹 Common Operations:
1. **Concatenation**: O(n)
   ```cpp
   string s1 = "Hello";
   string s2 = "World";
   cout << s1 + " " + s2; // Output: Hello World
   ```
2. **Substring Search**: O(n)
   ```cpp
   string s = "Hello World";
   cout << (s.find("World") != string::npos); // Output: 1 (true)
   ```
3. **Reversal**: O(n)
   ```cpp
   string s = "Hello";
   reverse(s.begin(), s.end());
   cout << s; // Output: olleH
   ```

#### 🔹 Use Cases:
- 📝 Text processing.
- 🔍 Pattern matching (e.g., Regular Expressions).

[Back to Top](#)

---

### **Linked Lists (Singly & Doubly)**

A **Linked List** is a linear data structure where elements (nodes) are connected using pointers.

#### 🔹 Types:
1. 🔗 **Singly Linked List**: Each node points to the next node.
2. 🔄 **Doubly Linked List**: Each node points to both the next and previous nodes.

---

#### **Singly Linked List**

Each node contains data and a pointer to the next node.

#### 🔹 Operations:
1. **Traversal**: O(n)
   ```cpp
   struct Node {
       int data;
       Node* next;
       Node(int val) : data(val), next(nullptr) {}
   };

   void traverse(Node* head) {
       Node* temp = head;
       while (temp != nullptr) {
           cout << temp->data << " ";
           temp = temp->next;
       }
   }

   Node* head = new Node(10);
   head->next = new Node(20);
   head->next->next = new Node(30);
   traverse(head); // Output: 10 20 30
   ```

2. **Insertion at Head**: O(1)
   ```cpp
   void insertAtHead(Node*& head, int val) {
       Node* newNode = new Node(val);
       newNode->next = head;
       head = newNode;
   }

   insertAtHead(head, 5);
   traverse(head); // Output: 5 10 20 30
   ```

3. **Deletion at Head**: O(1)
   ```cpp
   void deleteAtHead(Node*& head) {
       if (head == nullptr) return;
       Node* temp = head;
       head = head->next;
       delete temp;
   }

   deleteAtHead(head);
   traverse(head); // Output: 10 20 30
   ```

---

#### **Doubly Linked List**

Each node contains data, a pointer to the next node, and a pointer to the previous node.

#### 🔹 Structure:
```cpp
struct DoublyNode {
    int data;
    DoublyNode* prev;
    DoublyNode* next;
    DoublyNode(int val) : data(val), prev(nullptr), next(nullptr) {}
};
```

#### 🔹 Operations:
1. **Traversal**: O(n)
   ```cpp
   void traverse(DoublyNode* head) {
       DoublyNode* temp = head;
       while (temp != nullptr) {
           cout << temp->data << " ";
           temp = temp->next;
       }
   }

   DoublyNode* head = new DoublyNode(10);
   head->next = new DoublyNode(20);
   head->next->prev = head;
   head->next->next = new DoublyNode(30);
   head->next->next->prev = head->next;
   traverse(head); // Output: 10 20 30
   ```

2. **Insertion at Head**: O(1)
   ```cpp
   void insertAtHead(DoublyNode*& head, int val) {
       DoublyNode* newNode = new DoublyNode(val);
       if (head != nullptr) {
           head->prev = newNode;
       }
       newNode->next = head;
       head = newNode;
   }

   insertAtHead(head, 5);
   traverse(head); // Output: 5 10 20 30
   ```

3. **Deletion at Head**: O(1)
   ```cpp
   void deleteAtHead(DoublyNode*& head) {
       if (head == nullptr) return;
       DoublyNode* temp = head;
       head = head->next;
       if (head != nullptr) {
           head->prev = nullptr;
       }
       delete temp;
   }

   deleteAtHead(head);
   traverse(head); // Output: 10 20 30
   ```

#### 🔹 Advantages of Doubly Linked List:
- 🔄 Allows traversal in both directions.
- 🛠️ Easier to delete a node when a pointer to it is given.

#### 🔹 Disadvantages:
- 💾 Requires more memory due to the extra pointer (`prev`).
- ⚙️ Slightly more complex to implement compared to a singly linked list.

[Back to Top](#)

---

### **Stack**

A **stack** is a linear data structure that follows the **LIFO** (Last In, First Out) principle.

#### 🔹 Operations:
1. **Push**: Add an element to the top.
2. **Pop**: Remove the top element.
3. **Peek**: View the top element.

#### 🔹 Example:
```cpp
stack<int> s;
s.push(10); // Push
s.push(20);
cout << s.top(); // Peek: Output: 20
s.pop(); // Pop
```

#### 🔹 Use Cases:
- 🔄 Undo functionality.
- 🧮 Expression evaluation (e.g., postfix, prefix).

[Back to Top](#)

---

### **Queue (Normal, Circular, Deque)**

A **queue** is a linear data structure that follows the **FIFO** (First In, First Out) principle.

#### 🔹 Types:
1. 🔗 **Normal Queue**: Simple FIFO queue.
2. 🔄 **Circular Queue**: Connects the rear to the front.
3. 🔁 **Deque**: Double-ended queue (insertion/deletion at both ends).

#### 🔹 Operations:
1. **Enqueue**: Add an element to the rear.
2. **Dequeue**: Remove an element from the front.

#### 🔹 Example:
```cpp
queue<int> q;
q.push(10); // Enqueue
q.push(20);
cout << q.front(); // Peek: Output: 10
q.pop(); // Dequeue
```

#### 🔹 Use Cases:
- 🕒 Task scheduling.
- 🌐 BFS (Breadth-First Search).

[Back to Top](#)

---

### **Hashing (Hash Tables, Hash Maps)**

**Hashing** is a technique to map data to a fixed-size table using a hash function.

#### 🔹 Key Features:
- ⚡ Fast lookups: O(1) on average.
- 🛠️ Handles collisions using techniques like chaining or open addressing.

#### 🔹 Example:
```cpp
unordered_map<string, int> hashMap;
hashMap["key"] = 42;
cout << hashMap["key"]; // Output: 42
```

#### 🔹 Use Cases:
- 🗂️ Caching.
- 📖 Implementing dictionaries.

[Back to Top](#)

---

### **Searching Algorithms**

Searching algorithms are used to find the position of a target element in a given dataset. Two commonly used searching algorithms are **Linear Search** and **Binary Search**.

---

### **Linear Search**

**Linear Search** is the simplest searching algorithm that checks each element of the array sequentially until the target element is found or the end of the array is reached.

#### 🔹 How It Works:
1. 🔍 Start from the first element of the array.
2. 🔄 Compare each element with the target.
3. ✅ If a match is found, return the index.
4. ❌ If no match is found, return `-1`.

#### 🔹 Time Complexity:
- **Best Case**: O(1) (Target is the first element).
- **Worst Case**: O(n) (Target is the last element or not present).
- **Average Case**: O(n).

#### 🔹 Space Complexity:
- 💾 O(1) (No extra space is used).

#### 🔹 Implementation:
```cpp
#include <iostream>
#include <vector>
using namespace std;

int linearSearch(vector<int>& arr, int target) {
    for (int i = 0; i < arr.size(); i++) {
        if (arr[i] == target) {
            return i; // Target found, return index
        }
    }
    return -1; // Target not found
}

int main() {
    vector<int> arr = {10, 20, 30, 40, 50};
    int target = 30;
    int result = linearSearch(arr, target);

    if (result != -1) {
        cout << "Element found at index " << result << endl;
    } else {
        cout << "Element not found" << endl;
    }
    return 0;
}
```

#### 🔹 Advantages:
- ✨ Simple to implement.
- 🛠️ Works on both sorted and unsorted arrays.

#### 🔹 Disadvantages:
- ⚠️ Inefficient for large datasets due to O(n) time complexity.

---

### **Binary Search**

**Binary Search** is an efficient algorithm that works on sorted arrays by repeatedly dividing the search space in half.

#### 🔹 How It Works:
1. 🔍 Start with two pointers: `low` (beginning of the array) and `high` (end of the array).
2. 📏 Calculate the middle index: `mid = (low + high) / 2`.
3. 🔄 Compare the middle element with the target:
   - ✅ If the middle element equals the target, return the index.
   - 🔽 If the target is smaller, narrow the search to the left half (`high = mid - 1`).
   - 🔼 If the target is larger, narrow the search to the right half (`low = mid + 1`).
4. 🔁 Repeat until the target is found or the search space becomes empty.

#### 🔹 Time Complexity:
- **Best Case**: O(1) (Target is the middle element).
- **Worst Case**: O(log n) (Dividing the array in half at each step).
- **Average Case**: O(log n).

#### 🔹 Space Complexity:
- 💾 O(1) (Iterative approach).
- 💾 O(log n) (Recursive approach due to stack space).

#### 🔹 Implementation (Iterative):
```cpp
#include <iostream>
#include <vector>
using namespace std;

int binarySearch(vector<int>& arr, int target) {
    int low = 0, high = arr.size() - 1;

    while (low <= high) {
        int mid = low + (high - low) / 2; // Avoid overflow

        if (arr[mid] == target) {
            return mid; // Target found
        } else if (arr[mid] < target) {
            low = mid + 1; // Search in the right half
        } else {
            high = mid - 1; // Search in the left half
        }
    }
    return -1; // Target not found
}

int main() {
    vector<int> arr = {10, 20, 30, 40, 50};
    int target = 30;
    int result = binarySearch(arr, target);

    if (result != -1) {
        cout << "Element found at index " << result << endl;
    } else {
        cout << "Element not found" << endl;
    }
    return 0;
}
```

#### 🔹 Implementation (Recursive):
```cpp
int binarySearchRecursive(vector<int>& arr, int low, int high, int target) {
    if (low > high) {
        return -1; // Base case: Target not found
    }

    int mid = low + (high - low) / 2;

    if (arr[mid] == target) {
        return mid; // Target found
    } else if (arr[mid] < target) {
        return binarySearchRecursive(arr, mid + 1, high, target); // Search in the right half
    } else {
        return binarySearchRecursive(arr, low, mid - 1, target); // Search in the left half
    }
}

int main() {
    vector<int> arr = {10, 20, 30, 40, 50};
    int target = 30;
    int result = binarySearchRecursive(arr, 0, arr.size() - 1, target);

    if (result != -1) {
        cout << "Element found at index " << result << endl;
    } else {
        cout << "Element not found" << endl;
    }
    return 0;
}
```

#### 🔹 Advantages:
- ⚡ Much faster than Linear Search for large datasets.
- 🛠️ Efficient for sorted arrays.

#### 🔹 Disadvantages:
- ⚠️ Requires the array to be sorted.
- 🔄 Not suitable for dynamic datasets where frequent insertions/deletions occur.

---

### **Comparison: Linear Search vs Binary Search**

| Feature                | Linear Search         | Binary Search         |
|------------------------|-----------------------|-----------------------|
| **Time Complexity**    | O(n)                 | O(log n)              |
| **Space Complexity**   | O(1)                 | O(1) (Iterative)      |
| **Array Requirement**  | Unsorted or Sorted   | Sorted Only           |
| **Best Case**          | O(1)                 | O(1)                  |
| **Worst Case**         | O(n)                 | O(log n)              |
| **Use Case**           | Small datasets       | Large, sorted datasets|

[Back to Top](#)