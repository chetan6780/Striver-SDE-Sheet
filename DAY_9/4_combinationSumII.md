# Combination Sum II

Given a collection of candidate numbers (candidates) and a target number (target), find all unique combinations in candidates where the candidate numbers sum to target.

Each number in candidates may only be used once in the combination.

**Note:** The solution set must not contain duplicate combinations.

### Backtracking

-   for a number we have 2 choices either:
    -   we choose it
    -   we don't choose it
-   Also we cannot chose same element more than once.
-   if current element is less than target we can choose it.
-   else we can't choose it.
-   Base case arises when target is 0, we add the vector in answer.

### Code

```cpp

class Solution {
private:
    void helper(vector<int>& candidates, int target, int ind, vector<int>& path, vector<vector<int>>& res)
    {
        if (target == 0) {
            res.push_back(path);
            return;
        }

        for (int i = ind; i < candidates.size(); i++) {
            if (i > ind && candidates[i] == candidates[i - 1]) continue; // To Avoid Duplicates
            if (target < candidates[i]) break;

            path.push_back(candidates[i]); // DO
            helper(candidates, target - candidates[i], i + 1, path, res); // RECUR
            path.pop_back(); // UNDO/BACKTRACK
        }
    }

public:
    vector<vector<int>> combinationSum2(vector<int>& candidates, int target)
    {
        vector<vector<int>> res;
        vector<int> path;
        sort(candidates.begin(), candidates.end());
        helper(candidates, target, 0, path, res);
        return res;
    }
};
```
