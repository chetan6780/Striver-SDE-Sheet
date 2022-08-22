# Next Permutation

Implement **next permutation**, which rearranges numbers into the lexicographically next greater permutation of numbers.

If such an arrangement is not possible, it must rearrange it as the lowest possible order (i.e., sorted in ascending order).

The replacement must be in place and use only constant extra memory.

### Brute Force

-   We first generate all the permutations and store them in permutations vector.
-   Then we find the given vector in the permutations vector.if we found then we return its next vector as answer.
-   If given the last vector return the first vector from the permutations vector.
-   **TC: O(N!\*N)** - Because there are N! orders and N is the length of every array.
-   **SC: O(N!)** - To store all permutations, there are N! permutations.

##### Get all permutations with recursion

```cpp
void allPermutations(vector<vector<int>> ans, vector<int> nums, int ind)
{
    if (ind == nums.size())
    {
        ans.push_back(nums);
        return;
    }
    for (int i = ind; i < nums.size(); i++)
    {
        swap(nums[ind], nums[i]);
        allPermutations(ans, nums, ind + 1);
        swap(nums[ind], nums[i]);
    }
}
```

---

### O(N) Time solution.

-   INTUITION:- If we Observe the dictionary of order(permeation order) we can find that there is always Triangle like structure.
-   Just make permutation of `{1,2,3}` or `{1,2,3,4}` and observe the pattern.

```
1  2  3     2  1  3     3  1  2
1  3  2     2  3  1     3  2  1
-------------------------------
1 2 3 4     2 3 1 4     3 4 1 2
1 2 4 3     2 3 4 1     3 4 2 1
1 3 2 4     2 4 1 3     4 1 2 3
1 3 4 2     2 4 3 1     4 1 3 2
1 4 2 3     3 1 2 4     4 2 1 3
1 4 3 2     3 1 4 2     4 2 3 1
2 1 3 4     3 2 1 4     4 3 1 2
2 1 4 3     3 2 4 1     4 3 2 1
```

-   ALGORITHM:-
    1. **From end** find the **largest index** `k` such that `nums[k] < nums[k + 1]`.
       If no such index exists, just **reverse** `nums` and done.
    2. **From end** find the **largest index** `l > k` such that `nums[k] < nums[l]`.
    3. **Swap** `nums[k]` and `nums[l]`.
    4. **Reverse** the sub-array `nums[(k + 1):end]`.

### Code

```cpp
class Solution {
public:
    void nextPermutation(vector<int>& nums)
    {
        int n = nums.size();
        int k, l;

        // Step-1 : find index k before peak point from end;
        for (k = n - 2; k >= 0; k--) {
            if (nums[k] < nums[k + 1]) {
                break;
            }
        }

        if (k < 0) {
            reverse(nums.begin(), nums.end());
        } else {
            // step-2: find index l (l>k) from end which have greater element than at index k;
            for (l = n - 1; l > k; l--) {
                if (nums[k] < nums[l]) {
                    break;
                }
            }

            // Step-3: swap kth and lth element
            swap(nums[k], nums[l]);

            // Step-4: reverse vector from k+1 to end
            reverse(nums.begin() + k + 1, nums.end());
        }
    }
};
```

### Inbuilt next_permutation function

-   we can also solve the problem in-place using in-built `next_permutation(a.being(),a.end())` function in c++.
-   But in an interview this is not expected.

### Code

```cpp
class Solution {
public:
    void nextPermutation(vector<int>& nums){
        next_permutation(nums.begin(), nums.end());
    }
};
```
