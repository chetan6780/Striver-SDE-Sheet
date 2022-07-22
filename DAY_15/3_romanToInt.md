# Roman to integer

Given a string that represents a roman number. Convert the roman number to an integer and return it.
Roman numerals are represented by seven different symbols: I, V, X, L, C, D, and M.

### Solution

-   If number less than next number appears then subtract the next number from the current number else add them.

### Code

```cpp
#include <bits/stdc++.h>
int romanToInt(string s)
{
    map<char, int> mp = { { 'I', 1 },
        { 'V', 5 },
        { 'X', 10 },
        { 'L', 50 },
        { 'C', 100 },
        { 'D', 500 },
        { 'M', 1000 } };
    int ans = 0;
    int n = s.size();
    ans += mp[s[n - 1]];
    for (int i = n - 2; i >= 0; i--) {
        if (mp[s[i + 1]] > mp[s[i]]) {
            ans -= mp[s[i]];
        } else {
            ans += mp[s[i]];
        }
    }
    return ans;
}
```

---

# Int to roman

### Code

```cpp
string intToRoman(int n)
{
    string strRomans[] = { "M", "CM", "D", "CD", "C", "XC", "L", "XL", "X", "IX", "V", "IV", "I" };
    int values[] = { 1000, 900, 500, 400, 100, 90, 50, 40, 10, 9, 5, 4, 1 };
    string res = "";
    for (auto i = 0; i < 13; ++i) {
        while (n - values[i] >= 0) {
            res += strRomans[i];
            n -= values[i];
        }
    }
    return res;
}
```
