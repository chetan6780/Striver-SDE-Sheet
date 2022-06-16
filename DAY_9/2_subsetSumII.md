# Subsets II

Given an integer array nums that may contain duplicates, return all possible subsets (the power set).

The solution set **must not** contain duplicate subsets. Return the solution in any order.

**NOTE: Time and space complexity for this problem may be wrong**

### Brute Force

-   Use the pick and non pick technique to generate all subsets.
-   then store them in the set so the duplicate subsets we get removed.
-   **TC: O(2^N)**
-   **SC: O(2^N)**, Extra set

---

### Optimized Recursive solution (backtracking)

-   We can handle the case of not getting duplicates in the recursion itself.
-   we take the element and check if we took it before or not, except for the first element.
-   If element is duplicate then we continue to the next element.
-   else we add that element and recur for the next subset.
-   After the recursion we remove the element.
-   Here is example explanation of backtracking:
    ```cpp
    subsets([1,2,3,4]) = []
                     // push(1)
                     [1, subsets([2,3,4])] // if push N times in subsets([2,3,4]), the pop times is also N, so vec is also [1] after backtrack.
                     // pop(), push(2)
                     [2, subsets([3,4])]
                     // pop(), push(3)
                     [3, subsets([4])]
                     // pop(), push(4)
                     [4, subsets([])]
                     // pop()
    ```
-   **TC: O(2^N)**
-   **SC: O(2^N)**

```cpp
class Solution {
private:
    void findSubsets(int ind, vector<int>& nums, vector<int>& res, vector<vector<int>>& ans)
    {
        ans.push_back(res); // push the empty subset;
        int n = nums.size();

        for (int i = ind; i < n; i++) {
            if (i != ind && nums[i] == nums[i - 1])
                continue; // handling duplicates
            res.push_back(nums[i]); // DO
            findSubsets(i + 1, nums, res, ans); // RECUR
            res.pop_back(); // UNDO/Backtrack
        }
    }

public:
    vector<vector<int>> subsetsWithDup(vector<int>& nums)
    {
        vector<vector<int>> ans;
        vector<int> res;

        sort(nums.begin(), nums.end());
        findSubsets(0, nums, res, ans);
        return ans;
    }
};
```
