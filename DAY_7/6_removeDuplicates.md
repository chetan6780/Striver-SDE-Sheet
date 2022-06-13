# Remove Duplicates from Sorted Array

Given an integer array nums sorted in non-decreasing order, remove the duplicates in-place such that each unique element appears only once. The relative order of the elements should be kept the same.

Since it is impossible to change the length of the array in some languages, you must instead have the result be placed in the first part of the array nums. More formally, if there are k elements after removing the duplicates, then the first k elements of nums should hold the final result. It does not matter what you leave beyond the first k elements.

Return k after placing the final result in the first k slots of nums.

Do not allocate extra space for another array. You must do this by modifying the input array in-place with O(1) extra memory.

### Naive Solution

-   Store the elements in a set. then add them in the original vector in sorted order.
-   return the size of the set.
-   **TC: O(N log N)**, N for the traversal and log N for inserting elements in the set.
-   **SC: O(N)**, N for the set.

### Code

```cpp
class Solution {
public:
    int removeDuplicates(vector<int>& nums) {
        set<int> st;
        for(auto &x: nums) st.insert(x);
        int i=0;
        for(auto &x: st) nums[i++]=x;
        return st.size();
    }
};
```

### 2 pointer solution

-   Place pointe i to start and j to start + 1.
-   If nums[i] == nums[j], increment j.
-   else increment i and set nums[i] = nums[j].
-   return i + 1.
-   **TC: O(N)**, N for the traversal.
-   **SC: O(1)**, since we are modifying the array in place.

### Code

```cpp
class Solution {
public:
    int removeDuplicates(vector<int>& nums)
    {
        int n = nums.size(), i = 0;
        if (n == 0) return 0;
        for (int j = 1; j < n; j++) { // notice: loop is for J
            if (nums[i] != nums[j]) nums[++i] = nums[j];
        }
        return i + 1;
    }
};
```
