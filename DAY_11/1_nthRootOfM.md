# N'th root of M

### Binary Search

-   Simple binary search algorithm, but here we need to run while loop till the difference between the left and right is greater than epsilon.
-   **TC: N \* log(M \* 10^d)**, where d is decimal places of M. N is n.
-   **SC: O(1)**.

### Code

```cpp
long double power(long double mid, int n)
{
    long double ans = 1.0;
    while (n--)
        ans *= mid;
    return ans;
}

long double findNthRootOfM(int n, long long m)
{
    long double low = 1.0, high = (long double)m, eps = 1e-9;
    while ((high - low) > eps) {
        long double mid = (high - low) / 2.0 + low;
        if (power(mid, n) > (long double)m)
            high = mid;
        else
            low = mid;
    }
    return low;
}
```
