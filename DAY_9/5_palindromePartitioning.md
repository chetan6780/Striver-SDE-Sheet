# [131. Palindrome Partitioning](https://leetcode.com/problems/palindrome-partitioning/) 🌟🌟

Given a string `s`, partition `s` such that every substring of the partition is a palindrome. Return all possible **palindrome** partitioning of `s`.

A **palindrome** string is a string that reads the same backward as forward.

### Backtracking solution

-   For a given string, we can generate all possible palindrome partitioning of the string.
-   To do so we partition string from starting index to end index, such that it is a palindrome.
-   We do same for all position of string from starting index to end index.
-   The base case arises when we reach the end of the string.

### Code

```cpp
class Solution {
public:
    vector<vector<string>> partition(string s)
    {
        vector<vector<string>> result;
        vector<string> currentList;
        dfs(result, s, 0, currentList);
        return result;
    }

    void dfs(vector<vector<string>>& result, string& s, int start, vector<string>& currentList)
    {
        if (start >= s.length()) {
            result.push_back(currentList);
            return;
        }
        for (int end = start; end < s.length(); end++) {
            if (isPalindrome(s, start, end)) {
                currentList.push_back(s.substr(start, end - start + 1)); // DO
                dfs(result, s, end + 1, currentList); // RECUR
                currentList.pop_back(); // BACKTRACK
            }
        }
    }

    bool isPalindrome(string& s, int low, int high)
    {
        while (low < high) {
            if (s[low++] != s[high--])
                return false;
        }
        return true;
    }
};
```

### Must Read

-   [Java: Backtracking Template -- General Approach](https://leetcode.com/problems/palindrome-partitioning/discuss/182307/Java%3A-Backtracking-Template-General-Approach)
-   [Python: Backtracking Template -- General Approach](https://leetcode.com/problems/palindrome-partitioning/discuss/182310/Python%3A-Backtracking-Template-General-Approach)
