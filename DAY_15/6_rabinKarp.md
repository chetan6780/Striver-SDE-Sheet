# Rabin Karp algorithm for pattern matching

### Tushar Roy

-   Easy explanation of the algorithm - [Video](https://www.youtube.com/watch?v=H4VrKHVG5qI&t)

### Code

```cpp
class RabinKarpSearch {
    long long createHash(string str, int end)
    {
        long hash = 0;
        for (int i = 0; i < end; i++) {
            hash += str[i] * pow(101, i);
        }
        return hash;
    }

    long long recalculateHash(string str, int oldIndex, int newIndex, long oldHash, int patternLen)
    {
        long long newHash = oldHash - str[oldIndex];
        newHash = newHash / 101;
        newHash += str[newIndex] * pow(101, patternLen - 1);
        return newHash;
    }


    bool checkEqual(string str1, int start1, int end1, string str2, int start2, int end2)
    {
        if (end1 - start1 != end2 - start2) {
            return false;
        }
        while (start1 <= end1 && start2 <= end2) {
            if (str1[start1] != str2[start2]) {
                return false;
            }
            start1++;
            start2++;
        }
        return true;
    }

public:
    int patternSearch(string text, string pattern)
    {
        int n = text.size();
        int m = pattern.size();

        long patternHash = createHash(pattern, m );
        long textHash = createHash(text, m);

        for (int i = 1; i <= n - m + 1; i++) {
            if (patternHash == textHash && checkEqual(text, i - 1, i + m - 2, pattern, 0, m - 1)) {
                return i - 1;
            }
            if (i < n - m + 1) {
                textHash = recalculateHash(text, i - 1, i + m - 1, textHash, m);
            }
        }
        return -1;
    }
};
```

### Codestudio Solution

### Code

```cpp
#include <bits/stdc++.h>
const int base = 31;
const int q = 29;
void rabinkarp(string& pattern, string& text, vector<int>& ans)
{
    int j;
    int h = 1;
    int patHashVal = 0; // hashvalue of string pattern
    int textHashVal = 0; // hashvalue of string text
    int n = text.size();
    int m = pattern.size();

    // The value of h would be "pow(base, m-1)%q"
    for (int i = 0; i < m - 1; i++)
        h = (h * base) % q;

    // Calculate hash value for pattern and text (first set of hashvalue of size m )
    for (int i = 0; i < m; i++) {
        patHashVal = (base * patHashVal + pattern[i]) % q;
        textHashVal = (base * textHashVal + text[i]) % q;
    }

    // Slide the pattern over text one by one
    for (int i = 0; i <= n - m; i++) {
        if (patHashVal == textHashVal) {
            for (j = 0; j < m; j++) {
                if (text[i + j] != pattern[j])
                    break;
            }
            if (j == m)
                ans.push_back(i);
        }

        if (i < n - m) {
            textHashVal = textHashVal - h * text[i];
            textHashVal = (base * textHashVal + text[i + m]) % q;
            if (textHashVal < 0)
                textHashVal = textHashVal + q;
        }
    }
}
vector<int> stringMatch(string& str, string& pat)
{
    vector<int> ans;
    rabinkarp(pat, str, ans);
    return ans;
}
```
