# Longest Palindromic Substring

Given a string s, return the longest palindromic substring in s.

### Brute Force

-   Generate all substrings and check for longest palindromic substring.
-   **TC: O(n^3)**

### Dynamic Programming

-   For a string to be palindromic, it must be symmetric around the center.
-   So, in `xaaax` if `aaa` is a palindrome ans first x == second x, then `xaaax` is a palindrome.
-   We build dp table to check if string is palindrome or not by above method.
-   fill diagonal elements with 1s because they are palindromes(single character).
-   also fill the upper layer of diagonal with appropriate values.
-   a substring is palindrome if `s[i]==s[j] && dp[i + 1][j - 1]==1`.
-   For [simple detailed explanation](https://www.youtube.com/watch?v=UflHuQj6MVA).
-   **TC: O(N^2)**
-   **SC: O(N^2)**

### Code

```cpp
class Solution {
public:
    string longestPalindrome(string s)
    {
        int n = s.size();
        if (n == 0) return "";

        vector<vector<int>> dp(n, vector<int>(n, 0));
        for (int i = 0; i < n; i++) { //  for length 1
            dp[i][i] = 1;
        }
        int start = 0, maxLength = 1, flag = 1;
        for (int i = 0; i < n; i++) { // for length 2
            if (s[i] == s[i + 1]) {
                dp[i][i + 1] = 1;
                if (flag) {
                    start = i;
                    maxLength = 2;
                    flag = 0;
                }
            }
        }
        // for length greater than 2
        for (int len = 3; len <= n; len++) {
            for (int i = 0; i < n - len + 1; i++) {
                int j = i + len - 1;
                if (s[i] == s[j] && dp[i + 1][j - 1]) {
                    dp[i][j] = 1;
                    if (len > maxLength) {
                        start = i;
                        maxLength = len;
                    }
                }
            }
        }
        return s.substr(start, maxLength);
    }
};
```

### Expand around the center O(1) space

-   we traverse the string and expand around the center to find the longest palindrome.
-   [GFG: Expand around the center O(1) space](https://www.geeksforgeeks.org/longest-palindromic-substring-set-2/)

### Code - Codestudio

```cpp
#include <bits/stdc++.h>

string expandAroundCenter(int l, int r, string s)
{
    while (l >= 0 && r <= s.size()) {
        if (s[l] != s[r]) {
            break;
        }
        l--;
        r++;
    }
    return s.substr(l + 1, r - l - 1);
}
string longestPalinSubstring(string str)
{
    string longestSubstr = "";
    int n = str.size();

    for (int i = 0; i < n; i++) {
        string oddLenSubstr = expandAroundCenter(i, i, str);
        string evenSubstr = expandAroundCenter(i, i + 1, str);

        if (oddLenSubstr.size() > longestSubstr.size()) {
            longestSubstr = oddLenSubstr;
        }
        if (evenSubstr.size() > longestSubstr.size()) {
            longestSubstr = evenSubstr;
        }
    }
    return longestSubstr;
}
```
