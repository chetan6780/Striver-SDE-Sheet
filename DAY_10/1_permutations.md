# Permutations

Given an array nums of distinct integers, return all the possible permutations. You can return the answer in any order.

### Backtracking

-   Backtracking is a general technique for solving problems that uses DFS and finds **ALL POSSIBLE SOLUTIONS**.
-   General idea:
    ```
    Step 1: DO
    Step 2: RECUR
    Step 3: UNDO
    ```
    Make sure to use base conditions.

### Code

```cpp
class Solution{
    	void backtrackDfs(vector<int> &nums, int start, vector<vector<int>> &res){
		int n = nums.size();
		if (start >= n){
			res.push_back(nums);
			return;
		}

		for (int i = start; i < n; i++){
			swap(nums[start], nums[i]); // DO
			backtrackDfs(nums, start + 1, res); // RECUR
			swap(nums[start], nums[i]); // UNDO
		}
	}
public:
	vector<vector<int>> permute(vector<int> &nums){
		vector<vector<int>> res;
		backtrackDfs(nums, 0, res);
		return res;
	}
};
```

### Informative leetcode posts:

-   [A general approach to backtracking questions in Java (Subsets, Permutations, Combination Sum, Palindrome Partitioning)](<https://leetcode.com/problems/permutations/discuss/18239/A-general-approach-to-backtracking-questions-in-Java-(Subsets-Permutations-Combination-Sum-Palindrome-Partioning)>)

-   [Backtrack Summary: General Solution for 10 Questions!!!!!!!! Python (Combination Sum, Subsets, Permutation, Palindrome)](<https://leetcode.com/problems/permutations/discuss/18284/Backtrack-Summary%3A-General-Solution-for-10-Questions!!!!!!!!-Python-(Combination-Sum-Subsets-Permutation-Palindrome)>)
