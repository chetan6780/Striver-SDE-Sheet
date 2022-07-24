# KMP Algorithm

Given two strings needle and haystack, return the index of the first occurrence of needle in haystack, or -1 if needle is not part of haystack.(strStr - leetcode)

### strstr() using strstr() 😂

-   Using strstr() cpp stl 😆.

### Code

```cpp
class Solution {
public:
    int strStr(string haystack, string needle)
    {
        if (strstr(haystack.c_str(), needle.c_str()) == NULL)
            return -1;
        else
            return strstr(haystack.c_str(), needle.c_str()) - haystack.c_str();
    }
};
```

### strstr() implementation

### Code

```cpp
class Solution {
public:
    int strStr(string haystack, string needle)
    {
        if (needle.empty())
            return 0;
        if (haystack.empty())
            return -1;
        int i = 0;
        int j = 0;
        int n = haystack.size(), m = needle.size();
        while (i < n && j < m) {
            if (haystack[i] == needle[j]) {
                i++;
                j++;
            } else {
                i = i - j + 1;
                j = 0;
            }
        }
        if (j == m)
            return i - j;
        else
            return -1;
    }
};
```

### KMP - Knuth-Morris-Pratt

-   [leetcode discuss](https://leetcode.com/problems/implement-strstr/discuss/12956/C%2B%2B-Brute-Force-and-KMP)
-   [Very helpful - KMP on jBoxer's blog](http://jakeboxer.com/blog/2009/12/13/the-knuth-morris-pratt-algorithm-in-my-own-words/)
-   [GFG - KMP Algorithm for Pattern Searching](https://www.geeksforgeeks.org/kmp-algorithm-for-pattern-searching/)

### Code

```cpp
class Solution {
public:
    int strStr(string haystack, string needle) {
        int m = haystack.size(), n = needle.size();
        if (!n) {
            return 0;
        }
        vector<int> lps = kmpProcess(needle);
        for (int i = 0, j = 0; i < m;) {
            if (haystack[i] == needle[j]) {
                i++, j++;
            }
            if (j == n) {
                return i - j;
            }
            if (i < m && haystack[i] != needle[j]) {
                j ? j = lps[j - 1] : i++;
            }
        }
        return -1;
    }
private:
    vector<int> kmpProcess(string needle) {
        int n = needle.size();
        vector<int> lps(n, 0);
        for (int i = 1, len = 0; i < n;) {
            if (needle[i] == needle[len]) {
                lps[i++] = ++len;
            } else if (len) {
                len = lps[len - 1];
            } else {
                lps[i++] = 0;
            }
        }
        return lps;
    }
};
```

### Codestudio Solution

```cpp
void computeLPSArray(string p, int M, int lps[])
{
    // length of the previous longest prefix suffix
    int len = 0;
    int i = 1;
    lps[0] = 0; // lps[0] is always 0

    // the loop calculates lps[i] for i = 1 to M-1
    while (i < M) {
        if (p[i] == p[len]) {
            len++;
            lps[i] = len;
            i++;
        } else // (pat[i] != pat[len])
        {
            // This is tricky. Consider the example.
            // AAACAAAA and i = 7. The idea is similar
            // to search step.
            if (len != 0) {
                len = lps[len - 1];

                // Also, note that we do not increment
                // i here
            } else // if (len == 0)
            {
                lps[i] = len;
                i++;
            }
        }
    }
}

bool findPattern(string p, string s)
{
    int M = p.length();
    int N = s.length();
    int lps[M];
    int j = 0;
    int i = 0;
    computeLPSArray(p, M, lps);
    while (i < N) {
        if (p[j] == s[i]) {
            j++;
            i++;
        }
        if (j == M) {
            return true;
        } else if (i < N && p[j] != s[i]) {
            if (j != 0)
                j = lps[j - 1];
            else
                i = i + 1;
        }
    }
    return false;
}
```
