# Count the number of subarrays having a given XOR

Given an array of integers arr[] and a number m, count the number of subarrays having XOR of their elements as m.

### Note: This problem covers many concepts of subarray and xor.

### Brute force

-   Generate all the subarrays and count the number of subarrays which have XOR of their elements as m;
-   We can use kadane's algorithm to generate all the subarrays.

### Hashing solution

-   **TC: O(N)**
-   **SC: O(N)**
-   find explanation in [strivers video](https://www.youtube.com/watch?v=lO9R5CaGRPY).

```cpp
int countSubarrayWithXOR(vector<int>& a, int b)
{
    map<int, int> freq;
    int cnt = 0, xorr = 0;
    for (auto x : a) {
        xorr = xorr ^ x;

        if (xorr == b)
            cnt++;

        if (freq.count(xorr ^ b))
            cnt += freq[xorr ^ b];

        freq[xorr] += 1;
    }
    return cnt;
}
```
