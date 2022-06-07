# Reverse Pairs

Given an integer array `nums`, return the number of reverse pairs in the array.

A reverse pair is a pair `(i, j)` where `0 <= i < j < nums.length` and `nums[i] > 2 * nums[j]`

### Brute force

-   for every i we check the condition and increment the counter.
-   **Time complexity: O(n^2)**
-   **Space complexity: O(1)**

### Code (TLE + int overflow(2\*cnt))

```cpp
class Solution {
public:
    int reversePairs(vector<int>& nums){
        int cnt = 0;
        int n = nums.size();
        for (int i = 0; i < n; i++) {
            for (int j = i + 1; j < n; j++) {
                if (nums[i] > 2 * nums[j]) cnt++;
            }
        }
        return cnt;
    }
};
```

### Using Merge Sort modification

-   In the Merge function, we will be using low, mid, high values to count the total number of inversion pairs for the Left half and Right half of the Array.
-   Now, after the above task, we need to Merge the both Left and Right sub-arrays using a temporary vector.
-   After this, we need to copy back the temporary vector to the Original Array. Then finally we return the number of pairs we counted.
-   **TC: O(NlogN)**
-   **SC: O(N)**, if we use temp array.

### Code

```cpp

class Solution {
public:
    int merge(vector<int>& nums, int low, int mid, int high)
    {
        int cnt = 0;
        int j = mid + 1;
        for (int i = low; i <= mid; i++) {
            while (j <= high && nums[i] > 2LL * nums[j]) {
                j++;
            }
            cnt += (j - (mid + 1)); // add j-i in count
        }

        // Below is the merge code
        vector<int> temp;
        int left = low, right = mid + 1;
        while (left <= mid && right <= high) {
            if (nums[left] <= nums[right]) {
                temp.push_back(nums[left++]);
            } else {
                temp.push_back(nums[right++]);
            }
        }

        while (left <= mid) {
            temp.push_back(nums[left++]);
        }
        while (right <= high) {
            temp.push_back(nums[right++]);
        }

        for (int i = low; i <= high; i++) {
            nums[i] = temp[i - low];
        }
        return cnt;
    }
    int mergeSort(vector<int>& nums, int low, int high)
    {
        if (low >= high) return 0;
        int mid = (low + high) / 2;
        int inv = mergeSort(nums, low, mid);
        inv += mergeSort(nums, mid + 1, high);
        inv += merge(nums, low, mid, high);
        return inv;
    }
    int reversePairs(vector<int>& nums)
    {
        return mergeSort(nums, 0, nums.size() - 1);
    }
};
```
