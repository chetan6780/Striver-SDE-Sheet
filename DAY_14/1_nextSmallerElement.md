# Next smaller element

You are given an array 'ARR' of integers of length N. Your task is to find the next smaller element for each of the array elements.
Next Smaller Element for an array element is the first element to the right of that element which has a value strictly smaller than that element.
If for any array element the next smaller element does not exist, you should print -1 for that array element.

### Stack

-   similar to next greater element, just need to change sign of comparison between `st.top()` and `arr[i]`

### Code - 1

```cpp
vector<int> nextSmallerElement(vector<int>& arr, int n)
{
    vector<int> ans(n, -1);
    stack<int> st;
    for (int i = n - 1; i >= 0; i--) {
        while (!st.empty() && st.top() >= arr[i])
            st.pop();
        if (!st.empty())
            ans[i] = st.top();
        st.push(arr[i]);
    }
    return ans;
}
```

### Code - 2

```cpp
#include <bits/stdc++.h>

vector<int> nextSmallerElement(vector<int>& arr, int n)
{
    vector<int> ans(n);
    stack<int> st;
    st.push(-1);
    for (int i = n - 1; i >= 0; i--) {
        while (st.top() >= arr[i])
            st.pop();
        ans[i] = st.top();
        st.push(arr[i]);
    }
    return ans;
}#include <bits/stdc++.h>

vector<int> nextSmallerElement(vector<int>& arr, int n)
{
    vector<int> ans(n);
    stack<int> st;
    st.push(-1);
    for (int i = n - 1; i >= 0; i--) {
        while (st.top() >= arr[i])
            st.pop();
        ans[i] = st.top();
        st.push(arr[i]);
    }
    return ans;
}
```
