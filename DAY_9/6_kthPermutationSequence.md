# Permutation Sequence

The set [1, 2, 3, ..., n] contains a total of n! unique permutations.

By listing and labeling all of the permutations in order, we get the following sequence for n = 3:

```
"123"
"132"
"213"
"231"
"312"
"321"
```

Given n and k, return the kth permutation sequence.

### Brute Force

-   Generate all the possible permutation.
-   Sort the permutations.
-   Return the kth permutation.
-   **TC: O(N! \* N) + O(N! Log N!)**, O(N!) - generate every possible permutation , another O(N) time is to make a deep copy and store every sequence in the data structure. Also, O(N! Log N!) time required to sort the data structure
-   **SC: O(N!)**

### Optimized

-   **Time Complexity: O(N) \* O(N) = O(N^2)**
-   **Space Complexity: O(N)**

```cpp
class Solution {
public:
    string getPermutation(int n, int k)
    {
        int fact = 1;
        vector<int> numbers;
        for (int i = 1; i < n; i++) {
            fact = fact * i;
            numbers.push_back(i);
        }
        numbers.push_back(n);
        string ans = "";
        k--;
        while (true) {
            ans += to_string(numbers[k / fact]);
            numbers.erase(numbers.begin() + k / fact);

            if (numbers.size() == 0) break;

            k %= fact;
            fact /= numbers.size();
        }
        return ans;
    }
};
```
