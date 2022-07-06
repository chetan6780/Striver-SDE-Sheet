# Median of two sorted arrays

Given two sorted arrays nums1 and nums2 of size m and n respectively, return the median of the two sorted arrays.

The overall run time complexity should be O(log (m+n)).

### Naive Solution

-   Store elements of both array in a single array, sort it , find median.
-   **TC: O((m+n)log(m+n))**
-   **SC: O(m+n)**

### Code

```cpp
class Solution {
public:
    double findMedianSortedArrays(vector<int>& nums1, vector<int>& nums2)
    {
        vector<int> ans;
        ans.insert(ans.end(), nums1.begin(), nums1.end());
        ans.insert(ans.end(), nums2.begin(), nums2.end());
        sort(ans.begin(), ans.end());

        int n = ans.size();
        if (n & 1) {
            return ans[n / 2];
        } else {
            return (ans[n / 2] + ans[(n - 1) / 2]) / (double)2;
        }

        return 0;
    }
};
```

### Better Naive Solution

-   Instead of adding and them sorting, we can add elements such that new array is sorted. (like merge sort)
-   **TC:O(m+n)**
-   **SC:O(m+n)**

### Code

```cpp
class Solution {
    void mergeTwoSortedArray(vector<int>& a, vector<int>& b, vector<int>& res)
    {
        int n = a.size(), m = b.size();
        int i = 0, j = 0;
        while (i < n && j < m) {
            if (a[i] < b[j]) {
                res.push_back(a[i]);
                i++;
            } else {
                res.push_back(b[j]);
                j++;
            }
        }
        while (i < n) {
            res.push_back(a[i]);
            i++;
        }
        while (j < m) {
            res.push_back(b[j]);
            j++;
        }
    }

public:
    double findMedianSortedArrays(vector<int>& nums1, vector<int>& nums2)
    {
        vector<int> res;
        mergeTwoSortedArray(nums1, nums2, res);

        int n = res.size();
        if (n & 1) {
            return res[n / 2];
        } else {
            return (res[n / 2] + res[(n - 1) / 2]) / 2.0;
        }

        return 0;
    }
};
```

### Efficient Solution

-   **TC:O(log(m+n))**
-   **SC:O(1)**

```cpp
class Solution {
public:
    double findMedianSortedArrays(vector<int>& nums1, vector<int>& nums2)
    {
        int m = nums1.size();
        int n = nums2.size();
        if (m > n)
            return findMedianSortedArrays(nums2, nums1);
        int low = 0, high = m, medianPos = ((m + n) + 1) / 2;
        while (low <= high) {
            int cut1 = (low + high) >> 1;
            int cut2 = medianPos - cut1;

            int l1 = (cut1 == 0) ? INT_MIN : nums1[cut1 - 1];
            int l2 = (cut2 == 0) ? INT_MIN : nums2[cut2 - 1];
            int r1 = (cut1 == m) ? INT_MAX : nums1[cut1];
            int r2 = (cut2 == n) ? INT_MAX : nums2[cut2];

            if (l1 <= r2 && l2 <= r1) {
                if ((m + n) % 2 != 0)
                    return max(l1, l2);
                else
                    return (max(l1, l2) + min(r1, r2)) / 2.0;
            } else if (l1 > r2)
                high = cut1 - 1;
            else
                low = cut1 + 1;
        }
        return 0.0;
    }
};
```
