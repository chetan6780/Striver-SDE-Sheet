# 74. Search a 2D Matrix

Write an efficient algorithm that searches for a value in an m x n matrix. This matrix has the following properties:

- Integers in each row are sorted from left to right.
- The first integer of each row is greater than the last integer of the previous row.

### O(N\*M) Time and constant space solution

- Brute force.
- Traverse through the matrix and check for the target.
- If the target is found, return true.
- finally return false.

### O(N\*logM) Time and constant space solution

- Search using binary search.

### Code

```cpp
class Solution{
    bool binarySearch(vector<int> &nums, int target){
        int n = nums.size(), l = 0, r = n - 1;
        while (l <= r){
            int mid = l + (r - l) / 2;
            if (nums[mid] == target)
                return true;
            else if (target > nums[mid])
                l = mid + 1;
            else
                r = mid - 1;
        }
        return false;
    }

public:
    bool searchMatrix(vector<vector<int>> &matrix, int target){
        int n = matrix.size(), m = matrix[0].size();
        for (int i = 0; i < n; i++){
            if (matrix[i][0] <= target && target <= matrix[i][m - 1])
                return binarySearch(matrix[i], target);
        }
        return false;
    }
};
```

### O(log(N\*M)) Time and O(1) space

- Complete Binary search on matrix.
- mid/m : row , mid%m : column

### Code

```cpp
class Solution{
public:
    bool searchMatrix(vector<vector<int>> &matrix, int target){
        int n = matrix.size(), m = matrix[0].size();
        int l = 0, h = (n * m) - 1;

        while (l <= h){
            int mid = l + (h - l) / 2;
            if (matrix[mid / m][mid % m] == target)
                return true;
            else if (matrix[mid / m][mid % m] < target)
                l = mid + 1;
            else
                h = mid - 1;
        }
        return false;
    }
};
```
