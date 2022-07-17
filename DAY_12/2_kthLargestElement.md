# kth largest element

Given an integer array nums and an integer k, return the kth largest element in the array.

Note that it is the kth largest element in the sorted order, not the kth distinct element.

### Sorting

-   Sort array in descending order, return the kth element.
-   **TC: O(n log n)**
-   **SC: O(1)**

### Min Heap (priority queue)

### Code

```cpp
class Solution {
public:
    int findKthLargest(vector<int>& nums, int k)
    {
        // min heap
        priority_queue<int, vector<int>, greater<int>> pq;
        int i = 0, n = nums.size();
        while (i < n) {
            pq.push(nums[i]);
            i++;
            if (pq.size() > k)
                pq.pop();
        }
        return pq.top();
    }
};
```

### Max Heap (priority queue)

### Code

```cpp
class Solution {
public:
    int findKthLargest(vector<int>& nums, int k) {
        // Max heap
        priority_queue<int> pq;
        for(auto x:nums){
            pq.push(x);
        }
        while(--k){
            pq.pop();
        }
        return pq.top();
    }
};
```
