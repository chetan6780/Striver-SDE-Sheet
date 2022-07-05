# Single Element in a Sorted Array

You are given a sorted array consisting of only integers where every element appears exactly twice, except for one element which appears exactly once.

Return the single element that appears only once.

Your solution must run in `O(log n)` time and `O(1)` space.

### Brute force

-   check for duplicates element using 2 for loops.
-   **TC: O(N^2)**
-   **SC: O(1)**

### Hashmap

-   use hashmap to store the frequency of each element.
-   in hashmap if frequency is 1 then return the element.
-   **TC: O(N)**
-   **SC: O(N)**

### linear search

-   We can linearly search the array for the element.
-   for each time we increment the i by 2 and check for adjacent elements.
-   if the element is not equal to the previous element then we return the current element.
-   **TC: O(N)**
-   **SC: O(1)**

### Bit Manipulation(XOR)

-   We know that xor of 2 same numbers is 0.In the question it is given that all number except the ans appear twice.
-   So we can use XOR to find the ans.
-   **TC: O(N)**
-   **SC: O(1)**

```cpp
class Solution {
public:
    int singleNonDuplicate(vector<int>& nums) {
        int ans = 0;
        for(auto x:nums) ans^=x;
        return ans;
    }
};
```

### Binary Search

-   We can observe that before unique elements every repeated element starts with even index and after unique elements every repeated element starts with odd index.
-   so we can just binary search the ans based on the even and odd indexes.
-   **TC: O(logN)**
-   **SC: O(1)**

```cpp
class Solution {
public:
    int singleNonDuplicate(vector<int>& nums)
    {
        int low = 0, high = nums.size() - 2;
        while (low <= high) {
            int mid = (low + high) >> 1;
            if (nums[mid] == nums[mid ^ 1]) {
                low = mid + 1;
            } else {
                high = mid - 1;
            }
        }
        return nums[low];
    }
};
```

### Read:

-   [[C++] 7 Simple Solutions w/ Explanation | Brute + Hashmap + XOR + Linear + 2 Binary Search](https://leetcode.com/problems/single-element-in-a-sorted-array/discuss/1587270/C%2B%2B-5-Simple-Solutions-w-Explanation-or-Hashmap-%2B-XOR-%2B-Linear-Search-%2B-Binary-Search)
