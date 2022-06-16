# Subset Sums

Given a list arr of N integers, print sums of all subsets in it.

### Brute force

-   Generate all subsets of the given set ans print the sum of each subset.
-   We can generate all the subset with bit manipulation method.
-   **TC: O(2^N \* N)**

### Recursive Solution

-   By observation, we can say that there are only two choices for the element in the arr, either we pick it or we don't pick it.
-   Here the base condition will be, if we reach at the `last+1`(N) index then we can add the sum in the ans.
-   So, we can write trivial recursive function to solve this problem.
-   `void recFunc(int ind, int sum, vector<int> &arr, int N, vector<int> &sumArr)`, Where only **ind** and **sum** will change in almost every recursive call and other remain same.
-   **TC: O(2^N)**
-   **ASC: O(2^N)**, Recursion stack.

### Code

```cpp
class Solution {
private:
    void subsetSumsRec(int ind, int sum, vector<int> &arr, int N, vector<int> &sumArr)
    {
        // Base condition
        if (ind == N) {
            sumArr.push_back(sum);
            return;
        }

        // pick element - (ind+1,sum+arr[ind])
        subsetSumsRec(ind + 1, sum + arr[ind], arr, N, sumArr);

        // not pick element - (ind+1,sum)
        subsetSumsRec(ind + 1, sum, arr, N, sumArr);
    }

public:
    vector<int> subsetSums(vector<int> arr, int N)
    {
        vector<int> sumArr;
        subsetSumsRec(0, 0, arr, N, sumArr);
        sort(sumArr.begin(), sumArr.end());
        return sumArr;
    }
};
```
