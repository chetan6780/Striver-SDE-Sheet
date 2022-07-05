# Search in rotated sorted array

### Linear search

-   Straight forward linear search.
-   **TC: O(N)**
-   **SC: O(1)**

### Binary Search

### Code

```cpp
class Solution {
public:
    int search(vector<int>& nums, int target)
    {
        int n = nums.size();
        int l = 0, r = n - 1;
        while (l <= r) {
            int m = l + (r - l) / 2;
            if (nums[m] == target)
                return m;
            if (nums[m] < nums[r]) {
                if (nums[m] < target && target <= nums[r])
                    l = m + 1;
                else
                    r = m - 1;
            } else if (nums[m] > nums[r]) {
                if (nums[l] <= target && target < nums[m])
                    r = m - 1;
                else
                    l = m + 1;
            } else
                r--;
        }
        return -1;
    }
};
```

### Codestudio

```cpp
int search(int* arr, int n, int key)
{
    int l = 0, r = n - 1;
    while (l <= r) {
        int mid = l + (r - l) / 2;
        if (arr[mid] == key)
            return mid;

        else if (arr[l] <= arr[mid]) {
            if (arr[l] <= key && key <= arr[mid])
                r = mid - 1;
            else
                l = mid + 1;
        } else {
            if (arr[mid] <= key && key <= arr[r])
                l = mid + 1;
            else
                r = mid - 1;
        }
    }
    return -1;
}
```
