# Largest subarray with 0 sum

Given an array having both positive and negative integers. The task is to compute the length of the largest subarray with sum 0.

### Brute force

-   We generate all subarrays and find the largest subarray with 0 sum.
-   We can generate subarrays with **O(N^3), O(N^2)-using kadanes algorithm**

### Hashing Solution

-   kind of extension of kadanes algorithm
-   **TC: O(N lonN)**
-   **SC: O(N)** for map

### Code

```cpp
#include <bits/stdc++.h>
int LongestSubsetWithZeroSum(vector<int> arr)
{
    int n = arr.size();
    int sum = 0, mxLen = 0;
    unordered_map<int, int> mp;
    for (int i = 0; i < n; i++) {
        sum += arr[i];
        if (sum == 0) mxLen = i + 1;
        else {
            if (mp.count(sum)) {
                mxLen = max(mxLen, i - mp[sum]);
            } else {
                mp[sum] = i;
            }
        }
    }
    return mxLen;
}
```
