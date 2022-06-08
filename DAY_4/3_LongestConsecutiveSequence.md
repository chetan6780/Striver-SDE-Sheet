# Longest Consecutive Sequence

Given an unsorted array of integers nums, return the length of the longest consecutive elements sequence.

You must write an algorithm that runs in **`O(N)`** time.

### Naive Sorting Solution

-   sort the sequence and find the consecutive subsequences and out of them return the length of the longest consecutive subsequence.
-   **TC: O(NlogN)**

### Hash table O(N) Time solution

-   we create hash table of `nums`.
-   for every element we check if `num-1` is present or not.
-   if its not present then from `num` we count `num,num+1,num+2,...` consecutive elements.
-   when `num+..` not found we update our `ans`.
-   `return ans`.

### Code

```cpp
class Solution {
public:
    int longestConsecutive(vector<int>& nums) {
        int n = nums.size(), cnt=0, ans=0;
        if(n==0)return 0;
        unordered_set<int> st;
        for(auto x:nums)st.insert(x);
        for(auto x:nums){
            if(st.count(x-1)!=1){
                int currentNum = x;
                cnt=1;
                while(st.count(currentNum+1)){
                    currentNum++;
                    cnt++;
                }
                ans=max(ans,cnt);
            }
        }
        return ans;
    }
};
```
