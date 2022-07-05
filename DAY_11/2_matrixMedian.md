# Matrix Median

You have been given a matrix of ‘N’ rows and ‘M’ columns filled up with integers where every row is sorted in non-decreasing order. Your task is to find the overall median of the matrix i.e if all elements of the matrix are written in a single line, then you need to return the median of that linear array.
The median of a finite list of numbers is the "middle" number when those numbers are listed in order from smallest to greatest. If there is an odd number of observations, the middle one is picked. For example, consider the list of numbers [1, 3, 3, 6, 7, 8, 9]. This list contains seven numbers. The median is the fourth of them, which is 6.

### Brute force

-   Add all elements of the matrix to a single array and sort it.
-   Return the middle element of the sorted array.
-   **TC: O(N log N)**, N = total number of elements in the matrix **(N=n\*m)**.
-   **SC: O(N)**, N = total number of elements in the matrix **(N=n\*m)**.

### Code

```cpp
int getMedian(vector<vector<int>>& matrix)
{
    vector<int> ans;
    int n = matrix.size(), m = matrix[0].size();
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < m; j++) {
            ans.push_back(matrix[i][j]);
        }
    }
    n = ans.size();
    sort(ans.begin(), ans.end());
    return ans[(n / 2)];
}
```

### Binary Search

-   Find minimum and maximum element in the matrix.
    -   Compare first element of rows to get min element.
    -   Compare last element of rows to get max element.
-   Binary search between min and max element.
    -   Calculate mid.
    -   Calculate elements less than or equal to mid. (We can use upper_bound())
-   For number to be median, the count should be `n*m/2`.
    -   If count is less them median must be grater than current number.
    -   Else it is greater than current number.
-   Return min element, which is our median.
-   **TC: O(32 \* n \* log(m))** The upper bound function will take log(m) time and is performed for each row. And since the numbers will be max of 32 bit, so binary search of numbers from min to max will be performed in at most **32** `(log2(2^32) = 32)` operations.
-   **SC: O(1)**

### Code

```cpp
int getMedian(vector<vector<int>>& matrix)
{
    int n = matrix.size();
    int m = matrix[0].size();

    int mn = INT_MAX, mx = INT_MIN;
    for (int i = 0; i < n; i++) {
        // Get min element
        if (matrix[i][0] < mn)
            mn = matrix[i][0];

        // Get max element
        if (matrix[i][m - 1] > mx)
            mx = matrix[i][m - 1];
    }

    int reqCount = (n * m + 1) / 2;
    while (mn < mx) {
        int mid = mn + (mx - mn) / 2;
        int count = 0;

        // count elements smaller that or equal to mid
        for (int i = 0; i < n; i++) {
            count += upper_bound(matrix[i].begin(), matrix[i].end(), mid) - matrix[i].begin();
        }

        if (count < reqCount)
            mn = mid + 1;
        else
            mx = mid;
    }
    return mn;
}
```
