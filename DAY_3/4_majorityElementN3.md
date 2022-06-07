# Majority Element II

-   **GOOGLE QUESTION**

Given an integer array of size n, find all elements that appear more than ⌊ n/3 ⌋ times.

### Brute force

-   We check for all the elements, if it appears more than n/3 times, we add it to the result vector.
-   **TC: O(N^2)**
-   **SC:O(1)**

### O(N) Time and O(1) space

-   we Can take a vector or unordered_map to store the frequency of each element.
-   We traverse the hash map/ vector to find the n/3 frequency.
-   if we found we return the element.
-   **TC: O(N)**
-   **SC: O(N)**

### Code

```cpp
class Solution {
public:
    vector<int> majorityElement(vector<int>& nums) {
        int n = nums.size();
        n/=3;
        vector<int> ans;
        unordered_map<int,int> mp;
        for(int x:nums) mp[x]++;
        for(auto [x,f]:mp) {
            if(f>n) ans.push_back(x);
        }
        return ans;
    }
};
```

### Moore's Voting Algorithm

-   **TC:O(N)**
-   **SC:O(1)**
-   The intuition and method is same as `majority element` problem but here we maintain 2 cnt variables and 2 candidate because mathematically we cant have more than 2 elements whose count is >N/3.

```cpp
class Solution {
public:
    vector<int> majorityElement(vector<int>& nums)
    {
        int cand1 = -1, cand2 = -1, cnt1 = 0, cnt2 = 0, n = nums.size();
        for (int x : nums) {
            if (x == cand1) cnt1++;
            else if (x == cand2) cnt2++;
            else if (cnt1 == 0) {
                cand1 = x;
                cnt1 = 1;
            } else if (cnt2 == 0) {
                cand2 = x;
                cnt2 = 1;
            } else {
                cnt1--, cnt2--;
            }
        }
        vector<int> ans;
        cnt1 = 0, cnt2 = 0;
        for (int x : nums) {
            if (x == cand1) cnt1++;
            else if (x == cand2) cnt2++;
        }
        if (cnt1 > n / 3) ans.push_back(cand1);
        if (cnt2 > n / 3) ans.push_back(cand2);
        return ans;
    }
};
```
