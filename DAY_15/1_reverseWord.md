# Reverse word in a string

You are given a string of length N. You need to reverse the string word by word. There can be multiple spaces between two words and there can be leading or trailing spaces but in the output reversed string you need to put a single space between two words, and your reversed string should not contain leading or trailing spaces.

### Vector Solution

### Code

```cpp
#include <bits/stdc++.h>

string reverseString(string str)
{
    vector<string> vs;
    string word = "";
    int n = str.length();
    for (int i = 0; i < n; i++) {
        if (str[i] == ' ') {
            vs.push_back(word);
            word = "";
            while(str[i] == ' ')
                i++;
            i--;
        } else {
            word += str[i];
        }
    }
    if (word != "")
        vs.push_back(word);
    reverse(vs.begin(), vs.end());
    string res = "";
    for (auto x : vs) {
        res += x;
        res += " ";
    }
    return res;
}
```

### Stack Solution

-   Instead of reversing the vector, we can use stack to reverse the string.

### Space Optimization

-   [Best Explanation](<https://leetcode.com/problems/reverse-words-in-a-string/discuss/1531693/C%2B%2B-2-solutions-O(1)-space-Picture-explain-Clean-and-Concise>)

### Code

```cpp
class Solution {
public:
    string reverseWords(string s)
    {
        reverse(s.begin(), s.end());
        int l = 0, r = 0, i = 0, n = s.size();
        while (i < n) {
            while (i < n && s[i] != ' ')
                s[r++] = s[i++];

            if (l < r) {
                reverse(s.begin() + l, s.begin() + r);
                if (r == n)
                    break;
                s[r++] = ' ';
                l = r;
            }
            ++i;
        }
        if (r > 0 && s[r - 1] == ' ')
            --r;
        s.resize(r);
        return s;
    }
};
```
