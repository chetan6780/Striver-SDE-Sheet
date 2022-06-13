# Trapping Rain Water

Given n non-negative integers representing an elevation map where the width of each bar is `1`, compute how much water it can trap after raining.

### Brute force

-   For every index find the max water that can be trapped.
-   This can be done with the formula `min(maxLeft(i),maxRight(i))-a[i]`
-   **TC: O(N^2)**, 2nd loop for finding left and right max.
-   **SC: O(1)**

### PrefixSum Optimized

-   We can pre-compute left max in an array and right max from back into the another array, so the 2nd loop is not necessary.
-   **TC: O(N)**
-   **SC: O(N)**

### 2-pointer

-   We can find left max and right max with 2 pointer approach.
-   Explained in code.
-   **TC: O(N)**
-   **SC: O(1)**

### Code

```cpp
class Solution {
public:
    int trap(vector<int>& height)
    {
        int n = height.size();
        int left = 0, right = n - 1;
        int res = 0;
        int maxLeft = 0, maxRight = 0;

        while (left <= right) {
            if (height[left] <= height[right]) { // update max left
                if (height[left] > maxLeft) maxLeft = height[left];
                else res += maxLeft - height[left];
                left++;
            } else { // update max right
                if (height[right] > maxRight) maxRight = height[right];
                else res += maxRight - height[right];
                right--;
            }
        }
        return res;
    }
};
```
