# Maximum of minimum for every window size

You are given an array of ‘N’ integers, you need to find the maximum of minimum for every window size. The size of the window should vary from 1 to ‘N’ only.

### Monotonic Stack

### Code

```cpp
#include <bits/stdc++.h>

void prevSmallerFun(vector<int>& nums, vector<int>& res)
{
    int n = nums.size();
    stack<int> st;
    for (int i = 0; i < n; i++) {
        while (!st.empty() && nums[st.top()] >= nums[i]) {
            st.pop();
        }
        res[i] = st.empty() ? -1 : st.top();
        st.push(i);
    }
}

void nextSmallerFun(vector<int>& nums, vector<int>& res)
{
    stack<int> st;
    int n = nums.size();
    for (int i = n - 1; i >= 0; i--) {
        while (!st.empty() && nums[st.top()] >= nums[i]) {
            st.pop();
        }
        res[i] = st.empty() ? n : st.top();
        st.push(i);
    }
}

vector<int> maxMinWindow(vector<int> a, int n)
{
    vector<int> res(n, INT_MIN);
    vector<int> nextSmaller(n, -1), prevSmaller(n, n);

    nextSmallerFun(a, nextSmaller);
    prevSmallerFun(a, prevSmaller);

    for (int i = 0; i < n; i++) {
        int len = nextSmaller[i] - prevSmaller[i] - 1;
        res[len - 1] = max(res[len - 1], a[i]);
    }
    for (int i = n - 2; i >= 0; i--) {
        res[i] = max(res[i], res[i + 1]);
    }
    return res;
}
```
