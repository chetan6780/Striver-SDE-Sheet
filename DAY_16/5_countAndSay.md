# Count and Say

### Recursive approach!

1. What do we know and how can we use it.

    - Let's stat with example, suppose we have 4'th term "1211", how can we find 5'th term, then 6'th and so on.
        - **4'th** - "1211"
        - **5'th** - "1-1 1-2 2-1s" = "111221"
        - **6'th** - "3-1s 2-2s 1-1" = "312211"
        - **7'th** - "<ins>1-3</ins> <ins>1-1</ins> <ins>2-2s</ins> <ins>2-1s</ins>" = "13 11 22 21" = "13112221"
    - So from "n-1'th" term, we can find "n'th" term.
    - We just need to **count the number** and **say the number.**

2. Algorithm.
    - **Base case:** for n = 1, we just return "1"
    - Get "n-1'th" term.
    - count the numbers of "n-1'th" term and get _count-say_ string.
    - return final result as _count-say_ string.

### Code

```cpp
class Solution {
    // Simple function which return 'count-say` string.
    // Just read it you will get the idea.
    string countSayStrFun(string s)
    {
        int count = 1;
        string res = "";
        int n = s.size();
        for (int i = 1; i < n; i++) {
            if (s[i] == s[i - 1]) {
                count++;
            } else {
                res += to_string(count) + s[i - 1];
                count = 1;
            }
        }
        res += to_string(count) + s[s.size() - 1];
        return res;
    }

public:
    string countAndSay(int n)
    {
        if (n == 1) return "1"; // base case - first term is "1"

        // believe that it will return n-1'th term
        string s = countAndSay(n - 1);

        // Now just count the numbers and say the number.
        string countSayStr = countSayStrFun(s);

        return countSayStr;
    }
};
```

### Iterative approach

-   Same as recursive approach.

```cpp
class Solution {
public:
    string countAndSay(int n)
    {
        string s = "1";
        for (int i = 1; i < n; i++) {
            string t = "";
            int cnt = 1;
            for (int j = 1; j < s.size(); j++) {
                if (s[j] == s[j - 1])
                    cnt++;
                else {
                    t += to_string(cnt) + s[j - 1];
                    cnt = 1;
                }
            }
            t += to_string(cnt) + s[s.size() - 1];
            s = t;
        }
        return s;
    }
};
```
