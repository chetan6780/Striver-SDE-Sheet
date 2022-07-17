# Find median in Data stream

You are given a stream of 'N' integers. For every 'i-th' integer added to the running list of integers, print the resulting median.
Print only the integer part of the median.

### Priority Queue

-   **One of the most beautiful problem on heap 😍😃**
-   To solve this problem just need to keep in mid some rules.
-   maintain **Max Heap** to the **left side** of median and **Min Heap** to the **right side** of median.
    -   num lesser than median should always go on left side. **`(num < median)go left <-`**
    -   num greater than median should always go on right side. **`(num > median)go right ->`**
    -   Do above operations maintaining **difference in size of heaps to be <=1**, means shift element from one heap to other, if required.
-   If both heap have **same size**, then median is **average of top of both heaps**.
-   Else it is **top of heap with most elements**.
-   One more thing to remember is, **if both heaps do not have same size then after one operation their size become equal** and vise-versa.

### Code

```cpp
#include <bits/stdc++.h>
void findMedian(int* arr, int n)
{
    if (n == 0) return;

    priority_queue<int> maxHeap;
    // maxHeap - maintaining left side, always return max of left side.
    priority_queue<int, vector<int>, greater<int>> minHeap;
    // minHeap - maintaining right side, always return min of right side.

    int median = arr[0]; // median
    cout << median << " ";
    maxHeap.push(arr[0]);

    for (int i = 1; i < n; i++) {
        int num = arr[i];
        if (maxHeap.size() > minHeap.size()) {
            // Left part is greater
            if (median > num) {
                // num lesser than median should always go on left side
                minHeap.push(maxHeap.top());
                maxHeap.pop();
                maxHeap.push(num);
            } else {
                minHeap.push(num);
            }
            median = (minHeap.top() + maxHeap.top()) / 2;
        } else if (maxHeap.size() < minHeap.size()) {
            // right part is greater
            if (num > median) {
                // num greater than median should always go on right side
                maxHeap.push(minHeap.top());
                minHeap.pop();
                minHeap.push(num);
            } else {
                maxHeap.push(num);
            }
            median = (maxHeap.top() + minHeap.top()) / 2;
        } else {
            // both part is equals
            if (num < median) {
                // num lesser than median should always go on left side
                maxHeap.push(num);
                median = maxHeap.top();
            } else {
                // num greater than median should always go on right side
                minHeap.push(num);
                median = minHeap.top();
            }
        }
        cout << median << " ";
    }
}
```

### More approaches

-   [GFG - Median in a stream of integers](https://www.geeksforgeeks.org/median-of-stream-of-integers-running-integers/)
-   [GFG - Median of Stream of Running Integers using STL](https://www.geeksforgeeks.org/median-of-stream-of-running-integers-using-stl/)
