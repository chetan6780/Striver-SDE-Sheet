# Merge k sorted arrays

You have been given ‘K’ different arrays/lists, which are sorted individually (in ascending order). You need to merge all the given arrays/list such that the output array/list should be sorted in ascending order.

### Naive solution

-   store all elements in a single array and sort it. Return the sorted array.
-   **TC:O(n\*k\*log(n\*k))**
-   **SC:O(n\*k)**

### Merge 2 sorted array

-   Divide array into two halves
-   Merge the two halves
-   **TC: O( n _ k _ log k)**
-   **SC: O( n _ k _ log k)**

### Code

```cpp
#include <bits/stdc++.h>
vector<int> mergeTwoSortedArr(vector<int>& a, vector<int>& b)
{
    vector<int> res;
    int n = a.size();
    int m = b.size();
    int i = 0, j = 0;
    while (i < n && j < m) {
        if (a[i] < b[j]) {
            res.push_back(a[i]);
            i++;
        } else {
            res.push_back(b[j]);
            j++;
        }
    }
    while (i < n) {
        res.push_back(a[i]);
        i++;
    }
    while (j < m) {
        res.push_back(b[j]);
        j++;
    }
    return res;
}

vector<int> mergeKArrays(vector<vector<int>>& kArr, int i, int j)
{
    if (i == j) {
        return kArr[i];
    }
    int mid = (i + j) / 2;
    vector<int> left = mergeKArrays(kArr, i, mid);
    vector<int> right = mergeKArrays(kArr, mid + 1, j);
    return mergeTwoSortedArr(left, right);
}

vector<int> mergeKSortedArrays(vector<vector<int>>& kArrays, int k)
{
    return mergeKArrays(kArrays, 0, k - 1);
}
```

### Priority Queue

-   push all elements of each vector in min heap.
-   store all elements from min heap to vector and return it.
-   The complexity of this solution is same as above but it arrays are of different size then this solution is better.

### Code

```cpp
#include <bits/stdc++.h>
vector<int> mergeKSortedArrays(vector<vector<int>>& kArrays, int k)
{
    priority_queue<int, vector<int>, greater<int>> pq;
    for (auto x : kArrays) {
        for (auto y : x) {
            pq.push(y);
        }
    }
    vector<int> ans;
    while (!pq.empty()) {
        ans.push_back(pq.top());
        pq.pop();
    }
    return ans;
}
```
