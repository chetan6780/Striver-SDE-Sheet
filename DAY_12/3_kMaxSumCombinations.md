# K Max Sum Combinations

You are given two arrays/lists ‘A’ and ‘B’ of size ‘N’ each. You are also given an integer ‘K’. You have to find the ‘K’ maximum and valid sum combinations from all the possible sum combinations of the arrays/lists ‘A’ and ‘B’.
Sum combination is made by adding one element from array ‘A’ and another element from array ‘B’.

### Priority Queue (TLE)

-   We can calculate all possible sum combinations of arrays and push them into max heap.
-   Top k elements of the max heap will be our required ans.
-   **TC: O(N^2 \* log(K))**

### Code

```cpp
#include <bits/stdc++.h>
vector<int> kMaxSumCombination(vector<int>& a, vector<int>& b, int n, int k)
{
    priority_queue<int> pq;
    for (auto x : a) {
        for (auto y : b) {
            pq.push(x + y);
        }
    }
    vector<int> ans;
    while (k--) {
        ans.push_back(pq.top());
        pq.pop();
    }
    return ans;
}
```

### Priority Queue (min heap) (TLE)

-   Instead of max heap we can use min heap as well which gives same result and complexity.

### Code

```cpp
#include <bits/stdc++.h>
vector<int> kMaxSumCombination(vector<int>& a, vector<int>& b, int n, int k)
{
    priority_queue<int, vector<int>, greater<int>> pq;
    for (auto x : a) {
        for (auto y : b) {
            pq.push(x + y);
            if (pq.size() > k)
                pq.pop();
        }
    }
    vector<int> ans(k, 0);
    for (int i = k - 1; i >= 0; i--) {
        ans[i] = pq.top();
        pq.pop();
    }
    return ans;
}
```

### Optimized Priority Queue

-   To reduce complexity we can reduce number of push operations.
-   If our heap has smaller size than k then push sum in heap.
-   else if sum of element is greater than top element of heap then pop top element and push new sum.
-   Here we are using min heap so top element will be smallest element always.

### Code

```cpp
#include <bits/stdc++.h>

vector<int> kMaxSumCombination(vector<int>& a, vector<int>& b, int n, int k)
{
    priority_queue<int, vector<int>, greater<int>> pq;
    for (auto x : a) {
        for (auto y : b) {
            if (pq.size() < k)
                pq.push(x + y);
            else if (x + y > pq.top()) {
                pq.pop();
                pq.push(x + y);
            }
        }
    }
    vector<int> ans(k, 0);
    for (int i = k - 1; i >= 0; i--) {
        ans[i] = pq.top();
        pq.pop();
    }
    return ans;
}
```
