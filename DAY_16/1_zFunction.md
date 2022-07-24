# Z Function

You’re given a string S of length N and a string P of length M. Your task is to find the number of occurrences of P in S in linear time.(z-function - codestudio)

### Z-function

-   [GFG - Z algorithm (Linear time pattern searching Algorithm)](https://www.geeksforgeeks.org/z-algorithm-linear-time-pattern-searching-algorithm/)
-   [Tushar Roy - Z-Algorithm](https://www.youtube.com/watch?v=CpZh4eF8QBw)

### Code

```cpp
vector<int> Making_Z_Table(string s)
{
    int n = s.length();
    int l = 0, r = 0;

    vector<int> z(n, 0);
    for (int i = 1; i < n; i++) {
        if (i > r) {
            l = r = i;
            while (r < n && s[r] == s[r - l])
                r++;

            z[i] = (r - l);
            r--;
        } else {
            int idx = (i - l);
            if (i + z[idx] <= r) {
                z[i] = z[idx];
            } else {
                l = i;
                while (r < n && s[r] == s[r - l])
                    r++;

                z[i] = (r - l);
                r--;
            }
        }
    }

    return z;
}

int zAlgorithm(string s, string pat, int n, int m)
{
    string total = pat + "$" + s;

    vector<int> z_table = Making_Z_Table(total);

    // Uncomment below line to see z-table
    // for(int i = 0; i < z_table.size(); i++)
    //     cout << z_table[i] << " ";
    // cout << endl;

    vector<int> ans;

    for (int i = 0; i < z_table.size(); i++) {
        if (z_table[i] == pat.length()) {
            int remove_relative = i - pat.length() - 1;

            ans.push_back(remove_relative);
        }
    }

    return (int)ans.size();
}
```
