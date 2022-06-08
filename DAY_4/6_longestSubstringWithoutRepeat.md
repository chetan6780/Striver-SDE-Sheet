# Longest Substring Without Repeating Characters

Given a string s, find the length of the longest substring without repeating characters.

### O(N^3) Time, O(N) space

-   Brute force
-   We can consider all substrings one by one and check for each substring whether it contains all unique characters or not.
-   There will be n\*(n+1)/2 substrings.
-   Whether a substring contains all unique characters or not can be checked in linear time by scanning it from left to right and keeping a map of visited characters.
-   Time complexity of this solution would be O(n^3).

### Code

```cpp
bool areDistinct(string s, int i, int j){
    // Note : Default values in visited are false
    vector<bool> vis(26);

    for (int k = i; k < j+1; k++) {
        if (vis[s[k] - 'a'] == true) return false;
        vis[s[k] - 'a'] = true;
    }
    return true;
}

int longestUniqueSubstr(string str)
{
    int n = str.size();
    int res = 0;
    for (int i = 0; i < n; i++)
        for (int j = i; j < n; j++)
            if (areDistinct(str, i, j))
                res = max(res, j - i + 1);
    return res;
}
```

### O(N^2) Time O(N) space, Sliding window

-   For every i in string we check, **How long the substring starting with index i have unique characters**

### Code

```cpp
int longestUniqueSubstr(string s){
    int n = s.size();
    int res = 0;

    for (int i = 0; i < n; i++){
        vector<bool> vis(256);
        for (int j = i; j < n; j++) {

            // If current character is visited Break the loop
            if (vis[s[j]] == true)
                break;
            // Else update the result  and mark current character as visited.
            else {
                res = max(res, j - i + 1);
                vis[s[j]] = true;
            }
        }

        // Remove the first character of previous window
        vis[s[i]] = false;
    }

    return res;
}
```

### O(N) Time O(N) space, Sliding window

-   We keep track of unique characters in a hashmap(unordered_set).
-   l is left index and r is right index, these indicates unique substring's start and end.
-   if r'th character is not present in set, we add it and increment r also update `maxLength = max(maxLength, r-l);`
-   if r'th character is present in set, we remove it from set and increment l pointer.
-   finally return maxLength.

### Code

```cpp
class Solution{
public:
    int lengthOfLongestSubstring(string s){
        int n = s.length();
        unordered_set<int> st;

        int l = 0, r = 0, mx = 0;
        while (l < n && r < n){
            if (st.count(s[r]) == 0){
                st.insert(s[r++]);
                mx = max(mx, r - l);
            }
            else{
                st.erase(s[l++]);
            }
        }
        return mx;
    }
};
```
