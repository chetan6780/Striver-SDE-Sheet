# Kth element of two sorted arrays

Given two sorted arrays arr1 and arr2 of size N and M respectively and an element K. The task is to find the element that would be at the k’th position of the final sorted array.

### Naive Solution and Better Naive Solution

-   The solutions are same as previous problem, but here we need to return `arr[k-1]`.
-   Both Solutions are accepted on GFG but will be partially accepted on Codestudio.
-   We need to optimize i to `O(log(min(n,m)))`.

### Optimization using Binary Search

-   **TC:** `O(log(min(n,m)))`
-   **SC:** `O(1)`

### Codestudio

```cpp
#include <bits/stdc++.h>
int ninjaAndLadoos(vector<int>& row1, vector<int>& row2, int m, int n, int k)
{
    if(m < n) {
        return ninjaAndLadoos(row2, row1, n, m, k);
    }

    int low = max(0,k-n), high = min(k,m);

    while(low <= high) {
        int cut1 = (low + high) >> 1;
        int cut2 = k - cut1;
        int l1 = cut1 == 0 ? INT_MIN : row1[cut1 - 1];
        int l2 = cut2 == 0 ? INT_MIN : row2[cut2 - 1];
        int r1 = cut1 == m ? INT_MAX : row1[cut1];
        int r2 = cut2 == n ? INT_MAX : row2[cut2];

        if(l1 <= r2 && l2 <= r1) {
            return max(l1, l2);
        }
        else if (l1 > r2) {
            high = cut1 - 1;
        }
        else {
            low = cut1 + 1;
        }
    }
    return 1;
}
```
