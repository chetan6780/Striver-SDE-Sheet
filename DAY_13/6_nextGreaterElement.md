# Next Greater Element I

### Brute force

-   We can find the next grater element with the help of two for loops.
-   For every element find its next greater element.
-   **TC:O(N^2)**
-   **SC:O(1)**

### Code

```cpp
class Solution {
public:
    vector<int> nextGreaterElement(vector<int>& nums1, vector<int>& nums2) {
        vector<int> ans;
        int n = nums1.size();
        int m = nums2.size();
        bool find = false;
        bool found = false;
        for(int i = 0; i< n;i++){
            for(int j = 0; j< m;j++){
                if(find && nums2[j]>nums1[i]){
                    ans.push_back(nums2[j]);
                    found = true;
                    break;
                }
                if(nums1[i]==nums2[j]){
                    find = true;
                }
            }
            if(!found){
                ans.push_back(-1);
            }
            find = false;
            found = false;
        }
        return ans;
    }
};
```

### Monotonic stack + map

-   We can use the concept of monotonic stack to solve this problem.
-   We create decreasing stack in which bottom element is greatest while top is smallest.
-   Push element in stack if its less than its top.
-   else pop elements from stack until we find the element which is greater than current element, while popping we also update the map to store the answer.
-   finally traverse through first vector and get values from map.
-   **TC:O(N)**
-   **SC:O(N)**, for stack and map

### Code

```cpp
class Solution {
public:
    vector<int> nextGreaterElement(vector<int>& nums1, vector<int>& nums2)
    {
        unordered_map<int, int> mp;
        stack<int> st; // decreasing stack bottom to top
        int n = nums2.size();
        for (int i = 0; i < n; i++) {
            // pop till we find a number which is greater than current number
            while (!st.empty() && nums2[i] > st.top()) {
                mp[st.top()] = nums2[i];
                st.pop();
            }
            st.push(nums2[i]);
        }
        vector<int> ans;
        for (auto x : nums1) {
            ans.push_back(mp.count(x) ? mp[x] : -1);
        }
        return ans;
    }
};
```

### Codestudio

```cpp
#include <bits/stdc++.h>

vector<int> nextGreater(vector<int>& arr, int n)
{
    vector<int> ans(n, -1);
    stack<int> st;
    for (int i = n - 1; i >= 0; i--)
    {
        while (!st.empty() && st.top() <= arr[i])
            st.pop();
        if (!st.empty())
            ans[i] = st.top();
        st.push(arr[i]);
    }
    return ans;
}
```
