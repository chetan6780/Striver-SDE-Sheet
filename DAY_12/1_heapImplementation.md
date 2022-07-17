# Min heap and Max heap implementation

### Max heap implementation

-   [Reference - Coding Ninjas](https://www.codingninjas.com/codestudio/library/implementation-of-heap)
-   Self explanatory Code.

### Code

```cpp
// C++ program to depict the implementation of a heap.
#include <bits/stdc++.h>
using namespace std;

// A class for Max Heap.
class MaxHeap {
    int* arr; // A pointer pointing to the elements in the array in the heap.
    int maxSize; // Maximum possible size of the Max Heap.
    int heapSize; // Number of elements in the Max heap currently.

public:
    MaxHeap(int maxSize); // Constructor function.

    // Heapifies a sub-tree taking the given index as the root.
    void MaxHeapify(int); // TC: O(log n)

    int parent(int i){ // Returns the index of the parent of the element at ith index.
        return (i - 1) / 2;
    }

    int lChild(int i){ // Returns the index of the left child.
        return (2 * i + 1);
    }

    int rChild(int i){ // Returns the index of the right child.
        return (2 * i + 2);
    }

    int removeMax(); // TC: O(log n)
    void updateKey(int i, int newVal); // TC: O(log n)
    void deleteKey(int i); // TC: O(log n)
    void insertKey(int num); // TC: O(log n)

    int getMax(){ // Returns the maximum element in the heap.
        return arr[0]; // TC: O(1)
    }

    int curSize(){ // Returns the size of the heap.
        return heapSize; // TC: O(1)
    }
};

// Constructor function builds a heap from a given array a[] of the specified size.
MaxHeap::MaxHeap(int totalSize)
{
    heapSize = 0;
    maxSize = totalSize;
    arr = new int[totalSize];
}

// To heapify the subtree this method is called recursively
void MaxHeap::MaxHeapify(int i)
{   // TC: O(log n)
    int l = lChild(i);
    int r = rChild(i);
    int largest = i;

    if (l < heapSize && arr[l] > arr[i])
        largest = l;

    if (r < heapSize && arr[r] > arr[largest])
        largest = r;

    if (largest != i) {
        swap(arr[i], arr[largest]);
        MaxHeapify(largest);
    }
}

// Inserting a new key 'x'.
void MaxHeap::insertKey(int x)
{   // TC: O(log n)
    // To check whether the key can be inserted or not.
    if (heapSize == maxSize) {
        cout << "\nOverflow: Could not insertKey\n";
        return;
    }

    // The new key is initially inserted at the end.
    heapSize++;
    int i = heapSize - 1;
    arr[i] = x;

    // The max heap property is checked and if violation occurs, it is restored.
    while (i != 0 && arr[parent(i)] < arr[i]) {
        swap(arr[i], arr[parent(i)]);
        i = parent(i);
    }
}

// Increases value of key at index 'i' to new_val.
void MaxHeap::updateKey(int i, int newVal)
{   // TC: O(log n)
    arr[i] = newVal;

    while (i != 0 && arr[parent(i)] < arr[i]) {
        swap(arr[i], arr[parent(i)]);
        i = parent(i);
    }
}

// To remove the root node which contains the maximum element of the Max Heap.
int MaxHeap::removeMax()
{   // TC: O(log n)
    // Checking whether the heap array is empty or not.
    if (heapSize <= 0)
        return INT_MIN;
    if (heapSize == 1) {
        heapSize--;
        return arr[0];
    }

    // Storing the maximum element to remove it.
    int root = arr[0];
    arr[0] = arr[heapSize - 1];
    heapSize--;

    // To restore the property of the Max heap.
    MaxHeapify(0); // 0 is the index of the root of the Max heap.

    return root;
}

// In order to delete a key at a given index i.
void MaxHeap::deleteKey(int i)
{   // TC: O(log n)
    // It increases the value of the key to infinity and then removes the maximum value.
    updateKey(i, INT_MAX);
    removeMax();
}
```

### Applications

-   Used in operating systems for scheduling jobs on a priority basis.
-   Used in graph algorithms like Dijkstra’s Algorithm (to find the shortest path), Minimum Spanning Tree, and Prim's Algorithm.
-   Used to perform heap sort.
-   Used to implement priority queues

---

### Codestudio - Min heap Problem

### Code

```cpp

class MinHeap {
    int* arr;
    int maxSize;
    int currSize;

public:
    MinHeap(int maxSize)
    {
        this->maxSize = maxSize;
        this->currSize = 0;
        arr = new int[maxSize];
    }
    void minHeapify(int i)
    {
        int l = 2 * i + 1;
        int r = 2 * i + 2;
        int smallest = i;

        if (l < currSize && arr[l] < arr[smallest]) {
            smallest = l;
        }
        if (r < currSize && arr[r] < arr[smallest]) {
            smallest = r;
        }
        if (smallest != i) {
            swap(arr[i], arr[smallest]);
            minHeapify(smallest);
        }
    }
    int getMin()
    {
        if (currSize == 0) {
            cout << "Heap is empty" << endl;
            return -1;
        }
        return arr[0];
    }
    void insert(int x)
    {
        if (currSize == maxSize) {
            cout << "Heap is full" << endl;
            return;
        }
        arr[currSize] = x;
        currSize++;
        int i = currSize - 1;
        while (i > 0 && arr[i] < arr[(i - 1) / 2]) {
            swap(arr[i], arr[(i - 1) / 2]);
            i = (i - 1) / 2;
        }
    }

    int updateKey(int i, int newVal)
    {
        if (i < 0 || i >= currSize) {
            cout << "Invalid index" << endl;
            return -1;
        }
        arr[i] = newVal;
        while (i > 0 && arr[i] < arr[(i - 1) / 2]) {
            swap(arr[i], arr[(i - 1) / 2]);
            i = (i - 1) / 2;
        }
        return 0;
    }
    int deleteKey(int i)
    {
        if (i < 0 || i >= currSize) {
            cout << "Invalid index" << endl;
            return -1;
        }
        arr[i] = arr[currSize - 1];
        currSize--;
        minHeapify(i);
        return 0;
    }
    int removeMin()
    {
        if (currSize == 0) {
            cout << "Heap is empty" << endl;
            return -1;
        }
        int min = arr[0];
        arr[0] = arr[currSize - 1];
        currSize--;
        minHeapify(0);
        return min;
    }
};

vector<int> minHeap(int n, vector<vector<int>>& q)
{
    MinHeap h(100000);
    vector<int> ans;
    for (int i = 0; i < q.size(); i++) {
        if (q[i][0] == 0)
            h.insert(q[i][1]);
        else if (q[i][0] == 1) {
            int x = h.removeMin();
            cout << x <<" ";
        }
    }
    return ans;
}
```

### Alternate implementation

```cpp
void heapify_down(vector<int>& heap, int i)
{
    int left = 2 * i + 1;
    int right = 2 * i + 2;
    int smallest = i;

    if (left < heap.size() && heap[left] < heap[i]) {
        smallest = left;
    }

    if (right < heap.size() && heap[right] < heap[smallest]) {
        smallest = right;
    }

    if (smallest != i) {
        swap(heap[i], heap[smallest]);
        heapify_down(heap, smallest);
    }
}

// Recursive heapify-up algorithm
void heapify_up(vector<int>& heap, int i)
{
    if (i && heap[(i - 1) / 2] > heap[i]) {
        swap(heap[i], heap[(i - 1) / 2]);
        heapify_up(heap, (i - 1) / 2);
    }
}

// insert key into the heap
void push(vector<int>& heap, int key)
{
    heap.push_back(key);

    int index = heap.size() - 1;
    heapify_up(heap, index);
}

// Function to remove an element with the lowest priority (present at the root)
void pop(vector<int>& heap)
{
    heap[0] = heap.back();
    heap.pop_back();

    heapify_down(heap, 0);
}

vector<int> minHeap(int n, vector<vector<int>>& q)
{
    vector<int> heap, ans;
    for (int i = 0; i < q.size(); i++) {
        if (q[i][0]) {
            ans.push_back(heap[0]);
            pop(heap);
        } else {
            push(heap, q[i][1]);
        }
    }
    return ans;
}
```
