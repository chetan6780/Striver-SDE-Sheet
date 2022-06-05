# Pascal's Triangle

### Straightforward solution

### Code

```cpp
// codestudio
#include <bits/stdc++.h>
vector<vector<long long int>> printPascal(int n)
{
    vector<vector<long long int>> ans;
    if (n >= 1) ans.push_back({ 1 });
    if (n >= 2) ans.push_back({ 1, 1 });
    for (int i = 2; i < n; i++) {
        vector<long long int> row(i + 1, 1);
        for (int j = 1; j < i; j++) {
            row[j] = ans[i - 1][j - 1] + ans[i - 1][j];
        }
        ans.push_back(row);
    }
    return ans;
}
```

### Code

```cpp
// leetcode
class Solution{
public:
    vector<vector<int>> generate(int n){
        vector<vector<int>> ans;
        for (int i = 0; i < n; i++){
            ans.push_back(vector<int>(i + 1, 1));
            for (int j = 1; j < i; j++)
                ans[i][j] = ans[i - 1][j - 1] + ans[i - 1][j];
        }
        return ans;
    }
};
```

#### We can find any element(a[i][j]) in O(1) time using the formula (r-1)C(c-1) i.e (r-1)!/(c-1)!

-   Ex. 3rd element of 5th row -> c=2,r=4 -> (4\*3)/(2\*1) = 6.
