# Repeating and missing number

Given an unsorted array of size n. Array elements are in the range from 1 to n. One number from set {1, 2, …n} is missing and one number occurs twice in the array. Find these two numbers.

### O(N LogN) by sorting

-   Sort the array
-   Check if the number is repeated or missing

### O(N) Time and O(N) Space by Hashing

-   Create a vector of size n and store the frequencies of each element in it.
-   If frequency is 0 it is missing and if frequency is 2 it is repeated.

### O(N) Time Creating equations

-   For 1st equation, We can take sum of n numbers by n\*(n+1)/2 and then subtract the sum of all the elements in the array.
-   For 2nd equation, we can take sum of squares of n elements and subtract the sum of all the elements in the array.
-   So we get `x - y = a1` and `x^2 - y^2 = a2` then we solve theses two equations and get `x + y = a3`.
-   Then we solve `x + y = a3` and `x - y = a1` to get x and y, Where **x=Missing and y=Repeated**.![tempSketch](https://i.imgur.com/5kRqcYN.png)
-   **LIMITATION :** Since we are calculating sum of squares, it **can exceed the range of int**. So we need to use **long long int**.

### O(N) Time Using XOR

-   XOR all the elements of array, store it in x.
-   XOR all the elements till n, store it in y.
-   When we XOR x and y we get `x^y = a`.
-   All the bits that are set in `a` will be set in either x or y.
-   divide the elements of the array in two sets one set of elements with same bit set and other set with same bit not set.
-   Do the same for the 1 to n.
-   Now if we do XOR of all the elements in first set, we will get x, and by doing same in other set we will get y.
-   By doing so, we will get x in one set and y in another set.

### Code

```cpp
// codestudio
#include <bits/stdc++.h>
pair<int, int> missingAndRepeating(vector<int>& arr, int n)
{
    int x = 0, y = 0; // repeating and missing numbers resp.
    int i;
    int xorNum = 0, setBit;

    // xor of all numbers
    for (auto num : arr) xorNum ^= num;
    // xor with 1 to n
    for (int i = 1; i <= n; i++) xorNum ^= i;

    // get rightmost set bit no.
    setBit = xorNum & ~(xorNum - 1);

    // compare and divide into 2 sets
    for (int i = 0; i < n; i++) {
        if (arr[i] & setBit) {
            x ^= arr[i];
        } else {
            y ^= arr[i];
        }
    }
    for (i = 1; i <= n; i++) {
        if (i & setBit)
            x ^= i;
        else
            y ^= i;
    }

    // number may be swap, recheck to confirm
    int xCnt = 0;
    for (auto num : arr) {
        if (num == x) xCnt++;
    }

    if (xCnt != 0) return { y, x };
    return { x, y };
}
```

### Extra links

-   [GFG](https://www.geeksforgeeks.org/efficiently-merging-two-sorted-arrays-with-o1-extra-space/)
