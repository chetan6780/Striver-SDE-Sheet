# 4Sum

Given an array nums of n integers, return an array of all the unique quadruplets `[nums[a], nums[b], nums[c], nums[d]]` such that:

-   `0 <= a, b, c, d < n`
-   `a, b, c,` and `d` are **distinct**.
-   `nums[a] + nums[b] + nums[c] + nums[d] == target`

You may return the answer in any order.

### O(N^4) brute force

-   using 4 for loops we can solve this question.

### Sort + 3ptr + BinarySearch (int overflow)

-   we keep i,j,k pointers and find l using binary search.
-   **TC: O(N^3)** - 2 loops and finding 2 elements in O(N) time.
-   **SC: O(N^2)** - set of vectors

### TIP:

-   We can use following code to remove duplicates from vector.
-   ```cpp
    sort(v.begin(), v.end());
    v.erase(unique(v.begin(), v.end()), v.end());
    ```
-   See my [GFG Solution](https://practice.geeksforgeeks.org/problems/find-all-four-sum-numbers1732/1) for better understanding.

### Sort + 2 Pointers

-   we keep i,j pointers and find l and r using binary search.
-   We can **overcome int overflow** by calculating target in every loop.(see code)
-   We can also overcome extra space by processing pointers until duplicates occurs.(see code)
-   **TC: O(N^3)** - 2loops and finding 2 elements in O(N) time.
-   **SC: O(1)**

### Code

```cpp
class Solution {
public:
    vector<vector<int>> fourSum(vector<int>& num, int target)
    {
        vector<vector<int>> res;
        if (num.empty()) return res;
        int n = num.size();
        sort(num.begin(), num.end());

        for (int i = 0; i < n; i++) {
            for (int j = i + 1; j < n; j++) {
                int target_2 = target - (num[i] + num[j]);

                int l = j + 1;
                int r = n - 1;
                while (l < r) {
                    int twoSum = num[l] + num[r];
                    if (twoSum < target_2)
                        l++;
                    else if (twoSum > target_2)
                        r--;
                    else {
                        vector<int> quadruplet(4, 0);
                        quadruplet[0] = num[i];
                        quadruplet[1] = num[j];
                        quadruplet[2] = num[l];
                        quadruplet[3] = num[r];
                        res.push_back(quadruplet);

                        // Processing the duplicates of number 3
                        while (l < r && num[l] == quadruplet[2])
                            l++;
                        // Processing the duplicates of number 4
                        while (l < r && num[r] == quadruplet[3])
                            r--;
                    }
                }
                // Processing the duplicates of number 2
                while (j + 1 < n && num[j + 1] == num[j])
                    j++;
            }
            // Processing the duplicates of number 1
            while (i + 1 < n && num[i + 1] == num[i])
                i++;
        }
        return res;
    }
};
```

### O(N^2) Time super optimized

-   Store all sum of pair in map.
-   them again traverse all the pairs and find `target-arr[i]-arr[j]` in map.
-   If element is found, confirm that all array elements are distinct.
-   If they are return Yes, else No.

### Code

```cpp
// codestudio
#include <bits/stdc++.h>
string fourSum(vector<int> arr, int target, int n)
{
    unordered_map<int, pair<int, int>> mp;
    for (int i = 0; i < n - 1; i++)
        for (int j = i + 1; j < n; j++)
            mp[arr[i] + arr[j]] = { i, j };

    for (int i = 0; i < n - 1; i++) {
        for (int j = i + 1; j < n; j++) {
            int target_2 = target - (arr[i] + arr[j]);
            if (mp.count(target_2)) {
                pair<int, int> p = mp[target_2];
                // Check if all are distinct elements
                if (p.first != i && p.first != j && p.second != i && p.second != j)
                    return "Yes";
            }
        }
    }
    return "No";
}
```
