[Back to DSA Home Page](./README.md#)

## 🔵 Intermediate Topics 🧩📚🛠️

Great for those solving real-world problems or preparing for coding interviews:

- [Sorting Algorithms](#sorting-algorithms)
  - [Bubble, Selection, Insertion](#1-bubble-sort)
  - [Merge Sort, Quick Sort](#4-merge-sort)
  - [Heap Sort](#6-heap-sort)
- [Two Pointers Technique](#two-pointers-technique)
- [Sliding Window Technique](#sliding-window-technique)
- [Prefix Sum](#prefix-sum)
- [Fast & Slow Pointer (Tortoise & Hare)](#fast--slow-pointer-tortoise--hare)
- [Binary Search on Answer](#binary-search-on-answer)
- [Linked List Reversal](#linked-list-reversal)
- [Trees](#trees)
  - [Binary Trees](#binary-trees)
  - [Binary Search Trees (BST)](#binary-search-trees-bst)
  - [Tree Traversals (Preorder, Inorder, Postorder, Level Order)](#tree-traversals)
  - [Recursive and Iterative Traversals](#tree-traversals)

### Sorting Algorithms

Sorting algorithms are fundamental in computer science and are used to arrange data in a specific order. Below are some of the most common sorting algorithms, their explanations, and examples in C++.

#### 1. Bubble Sort
Bubble Sort is a simple comparison-based algorithm. It repeatedly steps through the list, compares adjacent elements, and swaps them if they are in the wrong order. This process is repeated until the list is sorted.

**Time Complexity:**
- Best Case: O(n) (when the array is already sorted)
- Average Case: O(n²)
- Worst Case: O(n²)

**Space Complexity:** O(1) (in-place sorting)

**C++ Code Example:**
```cpp
#include <iostream>
#include <vector>
using namespace std;

void bubbleSort(vector<int>& arr) {
    int n = arr.size();
    for (int i = 0; i < n - 1; i++) {
        for (int j = 0; j < n - i - 1; j++) {
            if (arr[j] > arr[j + 1]) {
                swap(arr[j], arr[j + 1]);
            }
        }
    }
}

int main() {
    vector<int> arr = {64, 34, 25, 12, 22, 11, 90};
    bubbleSort(arr);
    for (int num : arr) {
        cout << num << " ";
    }
    return 0;
}
```

#### 2. Selection Sort
Selection Sort divides the array into a sorted and an unsorted region. It repeatedly selects the smallest element from the unsorted region and moves it to the sorted region.

**Time Complexity:**
- Best Case: O(n²)
- Average Case: O(n²)
- Worst Case: O(n²)

**Space Complexity:** O(1) (in-place sorting)

**C++ Code Example:**
```cpp
#include <iostream>
#include <vector>
using namespace std;

void selectionSort(vector<int>& arr) {
    int n = arr.size();
    for (int i = 0; i < n - 1; i++) {
        int minIndex = i;
        for (int j = i + 1; j < n; j++) {
            if (arr[j] < arr[minIndex]) {
                minIndex = j;
            }
        }
        swap(arr[i], arr[minIndex]);
    }
}

int main() {
    vector<int> arr = {64, 25, 12, 22, 11};
    selectionSort(arr);
    for (int num : arr) {
        cout << num << " ";
    }
    return 0;
}
```

#### 3. Insertion Sort
Insertion Sort builds the sorted array one element at a time by repeatedly picking the next element and inserting it into its correct position.

**Time Complexity:**
- Best Case: O(n) (when the array is already sorted)
- Average Case: O(n²)
- Worst Case: O(n²)

**Space Complexity:** O(1) (in-place sorting)

**C++ Code Example:**
```cpp
#include <iostream>
#include <vector>
using namespace std;

void insertionSort(vector<int>& arr) {
    int n = arr.size();
    for (int i = 1; i < n; i++) {
        int key = arr[i];
        int j = i - 1;
        while (j >= 0 && arr[j] > key) {
            arr[j + 1] = arr[j];
            j--;
        }
        arr[j + 1] = key;
    }
}

int main() {
    vector<int> arr = {12, 11, 13, 5, 6};
    insertionSort(arr);
    for (int num : arr) {
        cout << num << " ";
    }
    return 0;
}
```

#### 4. Merge Sort
Merge Sort is a divide-and-conquer algorithm. It divides the array into halves, recursively sorts them, and then merges the sorted halves.

**Time Complexity:**
- Best Case: O(n log n)
- Average Case: O(n log n)
- Worst Case: O(n log n)

**Space Complexity:** O(n) (requires additional space for merging)

**C++ Code Example:**
```cpp
#include <iostream>
#include <vector>
using namespace std;

void merge(vector<int>& arr, int left, int mid, int right) {
    int n1 = mid - left + 1;
    int n2 = right - mid;
    vector<int> L(n1), R(n2);
    for (int i = 0; i < n1; i++) L[i] = arr[left + i];
    for (int i = 0; i < n2; i++) R[i] = arr[mid + 1 + i];

    int i = 0, j = 0, k = left;
    while (i < n1 && j < n2) {
        if (L[i] <= R[j]) {
            arr[k++] = L[i++];
        } else {
            arr[k++] = R[j++];
        }
    }
    while (i < n1) arr[k++] = L[i++];
    while (j < n2) arr[k++] = R[j++];
}

void mergeSort(vector<int>& arr, int left, int right) {
    if (left < right) {
        int mid = left + (right - left) / 2;
        mergeSort(arr, left, mid);
        mergeSort(arr, mid + 1, right);
        merge(arr, left, mid, right);
    }
}

int main() {
    vector<int> arr = {38, 27, 43, 3, 9, 82, 10};
    mergeSort(arr, 0, arr.size() - 1);
    for (int num : arr) {
        cout << num << " ";
    }
    return 0;
}
```

#### 5. Quick Sort
Quick Sort is another divide-and-conquer algorithm. It selects a pivot element, partitions the array around the pivot, and recursively sorts the partitions.

**Time Complexity:**
- Best Case: O(n log n)
- Average Case: O(n log n)
- Worst Case: O(n²) (when the pivot is the smallest or largest element)

**Space Complexity:** O(log n) (due to recursion stack)

**C++ Code Example:**
```cpp
#include <iostream>
#include <vector>
using namespace std;

int partition(vector<int>& arr, int low, int high) {
    int pivot = arr[high];
    int i = low - 1;
    for (int j = low; j < high; j++) {
        if (arr[j] < pivot) {
            i++;
            swap(arr[i], arr[j]);
        }
    }
    swap(arr[i + 1], arr[high]);
    return i + 1;
}

void quickSort(vector<int>& arr, int low, int high) {
    if (low < high) {
        int pi = partition(arr, low, high);
        quickSort(arr, low, pi - 1);
        quickSort(arr, pi + 1, high);
    }
}

int main() {
    vector<int> arr = {10, 7, 8, 9, 1, 5};
    quickSort(arr, 0, arr.size() - 1);
    for (int num : arr) {
        cout << num << " ";
    }
    return 0;
}
```

#### 6. Heap Sort
Heap Sort uses a binary heap data structure to sort elements. It first builds a max heap and then repeatedly extracts the maximum element to build the sorted array.

**Time Complexity:**
- Best Case: O(n log n)
- Average Case: O(n log n)
- Worst Case: O(n log n)

**Space Complexity:** O(1) (in-place sorting)

**C++ Code Example:**
```cpp
#include <iostream>
#include <vector>
using namespace std;

void heapify(vector<int>& arr, int n, int i) {
    int largest = i;
    int left = 2 * i + 1;
    int right = 2 * i + 2;

    if (left < n && arr[left] > arr[largest]) largest = left;
    if (right < n && arr[right] > arr[largest]) largest = right;

    if (largest != i) {
        swap(arr[i], arr[largest]);
        heapify(arr, n, largest);
    }
}

void heapSort(vector<int>& arr) {
    int n = arr.size();
    for (int i = n / 2 - 1; i >= 0; i--) heapify(arr, n, i);
    for (int i = n - 1; i > 0; i--) {
        swap(arr[0], arr[i]);
        heapify(arr, i, 0);
    }
}

int main() {
    vector<int> arr = {12, 11, 13, 5, 6, 7};
    heapSort(arr);
    for (int num : arr) {
        cout << num << " ";
    }
    return 0;
}
```

[Back to Top](#)

---

### Two Pointers Technique

The Two Pointers Technique is a common algorithmic approach used to solve problems involving arrays or lists. It involves using two pointers to traverse the data structure, often from opposite ends or in a specific direction, to achieve an optimal solution.

#### When to Use:
- Problems involving sorted arrays or lists.
- Finding pairs or triplets that satisfy a condition.
- Removing duplicates or partitioning arrays.

#### Example 1: Finding a Pair with a Given Sum
Given a sorted array, find if there exists a pair of numbers that add up to a target sum.

**C++ Code Example:**
```cpp
#include <iostream>
#include <vector>
using namespace std;

bool hasPairWithSum(const vector<int>& arr, int target) {
    int left = 0, right = arr.size() - 1;
    while (left < right) {
        int sum = arr[left] + arr[right];
        if (sum == target) return true;
        else if (sum < target) left++;
        else right--;
    }
    return false;
}

int main() {
    vector<int> arr = {1, 2, 3, 4, 6};
    int target = 8;
    cout << (hasPairWithSum(arr, target) ? "Yes" : "No") << endl;
    return 0;
}
```

#### Example 2: Removing Duplicates from a Sorted Array
**C++ Code Example:**
```cpp
#include <iostream>
#include <vector>
using namespace std;

int removeDuplicates(vector<int>& arr) {
    if (arr.empty()) return 0;
    int uniqueIndex = 0;
    for (int i = 1; i < arr.size(); i++) {
        if (arr[i] != arr[uniqueIndex]) {
            uniqueIndex++;
            arr[uniqueIndex] = arr[i];
        }
    }
    return uniqueIndex + 1;
}

int main() {
    vector<int> arr = {1, 1, 2, 2, 3, 4, 4};
    int newLength = removeDuplicates(arr);
    for (int i = 0; i < newLength; i++) {
        cout << arr[i] << " ";
    }
    return 0;
}
```

[Back to Top](#)

---

### Sliding Window Technique

The Sliding Window Technique is a powerful method used to solve problems involving subarrays or substrings. It involves maintaining a window (a range of elements) that slides over the data structure to find an optimal solution.

#### When to Use:
- Problems involving contiguous subarrays or substrings.
- Finding maximum, minimum, or specific properties of subarrays.
- Optimizing time complexity for brute-force solutions.

#### Example 1: Maximum Sum of a Subarray of Size K
Given an array, find the maximum sum of any subarray of size K.

**C++ Code Example:**
```cpp
#include <iostream>
#include <vector>
using namespace std;

int maxSumSubarray(const vector<int>& arr, int k) {
    int maxSum = 0, windowSum = 0;
    for (int i = 0; i < k; i++) {
        windowSum += arr[i];
    }
    maxSum = windowSum;
    for (int i = k; i < arr.size(); i++) {
        windowSum += arr[i] - arr[i - k];
        maxSum = max(maxSum, windowSum);
    }
    return maxSum;
}

int main() {
    vector<int> arr = {2, 1, 5, 1, 3, 2};
    int k = 3;
    cout << "Maximum sum: " << maxSumSubarray(arr, k) << endl;
    return 0;
}
```

#### Example 2: Longest Substring with K Distinct Characters
Given a string, find the length of the longest substring that contains at most K distinct characters.

**C++ Code Example:**
```cpp
#include <iostream>
#include <unordered_map>
#include <string>
using namespace std;

int longestSubstringWithKDistinct(const string& s, int k) {
    unordered_map<char, int> charCount;
    int maxLength = 0, left = 0;
    for (int right = 0; right < s.size(); right++) {
        charCount[s[right]]++;
        while (charCount.size() > k) {
            charCount[s[left]]--;
            if (charCount[s[left]] == 0) {
                charCount.erase(s[left]);
            }
            left++;
        }
        maxLength = max(maxLength, right - left + 1);
    }
    return maxLength;
}

int main() {
    string s = "araaci";
    int k = 2;
    cout << "Longest substring length: " << longestSubstringWithKDistinct(s, k) << endl;
    return 0;
}
```

[Back to Top](#)

---

### Prefix Sum

The Prefix Sum technique is a powerful tool for solving problems involving cumulative sums. It involves precomputing an array of prefix sums to answer range sum queries efficiently.

#### When to Use:
- Problems involving range sums.
- Optimizing brute-force solutions for sum-related queries.

#### Example: Range Sum Query
Given an array, find the sum of elements between indices `i` and `j` (inclusive).

**C++ Code Example:**
```cpp
#include <iostream>
#include <vector>
using namespace std;

vector<int> computePrefixSum(const vector<int>& arr) {
    vector<int> prefixSum(arr.size());
    prefixSum[0] = arr[0];
    for (int i = 1; i < arr.size(); i++) {
        prefixSum[i] = prefixSum[i - 1] + arr[i];
    }
    return prefixSum;
}

int rangeSum(const vector<int>& prefixSum, int i, int j) {
    if (i == 0) return prefixSum[j];
    return prefixSum[j] - prefixSum[i - 1];
}

int main() {
    vector<int> arr = {1, 2, 3, 4, 5};
    vector<int> prefixSum = computePrefixSum(arr);
    cout << "Sum of range (1, 3): " << rangeSum(prefixSum, 1, 3) << endl;
    return 0;
}
```

[Back to Top](#)

### Fast & Slow Pointer (Tortoise & Hare)

The Fast & Slow Pointer technique is used to detect cycles in linked lists or arrays. It involves two pointers moving at different speeds.

#### When to Use:
- Detecting cycles in linked lists.
- Finding the starting point of a cycle.

#### Example: Detecting a Cycle in a Linked List
**C++ Code Example:**
```cpp
#include <iostream>
using namespace std;

struct ListNode {
    int val;
    ListNode* next;
    ListNode(int x) : val(x), next(nullptr) {}
};

bool hasCycle(ListNode* head) {
    ListNode *slow = head, *fast = head;
    while (fast && fast->next) {
        slow = slow->next;
        fast = fast->next->next;
        if (slow == fast) return true;
    }
    return false;
}

int main() {
    ListNode* head = new ListNode(1);
    head->next = new ListNode(2);
    head->next->next = head; // Creates a cycle
    cout << (hasCycle(head) ? "Cycle detected" : "No cycle") << endl;
    return 0;
}
```

[Back to Top](#)

### Binary Search on Answer

Binary Search on Answer is a technique used to solve optimization problems by searching for the smallest or largest feasible solution.

#### When to Use:
- Problems involving a monotonic function.
- Finding the minimum or maximum value that satisfies a condition.

#### Example: Minimum Capacity to Ship Packages Within D Days
**C++ Code Example:**
```cpp
#include <iostream>
#include <vector>
using namespace std;

bool canShip(const vector<int>& weights, int days, int capacity) {
    int currentWeight = 0, requiredDays = 1;
    for (int weight : weights) {
        if (currentWeight + weight > capacity) {
            requiredDays++;
            currentWeight = 0;
        }
        currentWeight += weight;
    }
    return requiredDays <= days;
}

int shipWithinDays(const vector<int>& weights, int days) {
    int left = *max_element(weights.begin(), weights.end());
    int right = accumulate(weights.begin(), weights.end(), 0);
    while (left < right) {
        int mid = left + (right - left) / 2;
        if (canShip(weights, days, mid)) {
            right = mid;
        } else {
            left = mid + 1;
        }
    }
    return left;
}

int main() {
    vector<int> weights = {1, 2, 3, 4, 5, 6, 7, 8, 9, 10};
    int days = 5;
    cout << "Minimum capacity: " << shipWithinDays(weights, days) << endl;
    return 0;
}
```

[Back to Top](#)

### Linked List Reversal

Reversing a linked list is a fundamental operation in data structures. It involves reversing the direction of the `next` pointers.

#### Example: Iterative Reversal
**C++ Code Example:**
```cpp
#include <iostream>
using namespace std;

struct ListNode {
    int val;
    ListNode* next;
    ListNode(int x) : val(x), next(nullptr) {}
};

ListNode* reverseList(ListNode* head) {
    ListNode *prev = nullptr, *current = head;
    while (current) {
        ListNode* nextNode = current->next;
        current->next = prev;
        prev = current;
        current = nextNode;
    }
    return prev;
}

int main() {
    ListNode* head = new ListNode(1);
    head->next = new ListNode(2);
    head->next->next = new ListNode(3);
    head = reverseList(head);
    while (head) {
        cout << head->val << " ";
        head = head->next;
    }
    return 0;
}
```

[Back to Top](#)

### Trees

#### Binary Trees
A Binary Tree is a tree data structure where each node has at most two children.

#### Binary Search Trees (BST)
A Binary Search Tree is a binary tree where the left child contains values less than the parent, and the right child contains values greater than the parent.

#### Tree Traversals
Tree traversal is the process of visiting all nodes in a tree in a specific order.

##### Preorder Traversal
**C++ Code Example:**
```cpp
#include <iostream>
using namespace std;

struct TreeNode {
    int val;
    TreeNode* left;
    TreeNode* right;
    TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
};

void preorder(TreeNode* root) {
    if (!root) return;
    cout << root->val << " ";
    preorder(root->left);
    preorder(root->right);
}

int main() {
    TreeNode* root = new TreeNode(1);
    root->left = new TreeNode(2);
    root->right = new TreeNode(3);
    preorder(root);
    return 0;
}
```

##### Inorder Traversal
**C++ Code Example:**
```cpp
void inorder(TreeNode* root) {
    if (!root) return;
    inorder(root->left);
    cout << root->val << " ";
    inorder(root->right);
}
```

##### Postorder Traversal
**C++ Code Example:**
```cpp
void postorder(TreeNode* root) {
    if (!root) return;
    postorder(root->left);
    postorder(root->right);
    cout << root->val << " ";
}
```

##### Level Order Traversal
**C++ Code Example:**
```cpp
#include <iostream>
#include <queue>
using namespace std;

void levelOrder(TreeNode* root) {
    if (!root) return;
    queue<TreeNode*> q;
    q.push(root);
    while (!q.empty()) {
        TreeNode* current = q.front();
        q.pop();
        cout << current->val << " ";
        if (current->left) q.push(current->left);
        if (current->right) q.push(current->right);
    }
}
```

[Back to Top](#)
