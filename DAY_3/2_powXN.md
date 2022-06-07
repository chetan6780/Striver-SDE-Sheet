# 50. Pow(x, n)

Implement `pow(x, n)`, which calculates `x` raised to the power `n` (i.e., `x^n`).

### O(N) Time Brute force

-   if n is `0`, return `1.0`
-   set `ans = x`
-   We iterate N times and multiply `ans` with `x`.
-   If **N is negative**, we convert it to **positive** and then multiply with `x` and finally return `1/result`.
-   But there is one **edge case**, given that `n` is `integer` and range of integers is **-2,147,483,648 to 2,147,483,647** so if we convert -2,147,483,648 to positive, it will **overflow**.
-   To tackle this edge case, we can use **long** type.

### Code (TLE)

```cpp
class Solution {
public:
    double myPow(double x, int n)
    {
        if (n == 0) return 1.0;
        double ans = x;
        // long long tempN = (n > 0) ? n : -n; // DON'T-int overflow
        long long tempN = n;
        if(tempN<) tempN = -tempN; // DO
        bool neg = (n > 0) ? false : true;
        for (int i = 2; i <= tempN; i++) {
            ans *= x;
        }
        if (neg) {
            ans = 1.0 / ans;
        }
        return ans;
    }
};
```

### O(log2N) optimized

-   Math concept `2^5 = 2*(2^4) = 2*(4^2) = 2*16 = 32`
-   if n is even we can divide it half and do multiplication
-   if n is odd we can multiply 1 x with ans and reduce it to even number.
-   when it will be 0 we stop the loop.

```cpp
class Solution {
public:
    double myPow(double x, int n)
    {
        double ans = 1.0;
        long long tempN = n;
        if (tempN < 0) tempN = -1 * tempN;
        while (tempN) {
            if (tempN % 2 == 1) { //odd
                ans *= x;
                tempN -= 1;
            } else { // even
                x *= x;
                tempN /= 2;
            }
        }
        if (n < 0) ans = 1.0 / ans;
        return ans;
    }
};
```

### Recursive

### Code

```cpp
class Solution {
public:
    double myPow(double x, int n)
    {
        if (n < 0) return 1 / x * myPow(1 / x, -(n + 1));
        if (n == 0) return 1;
        if (n == 2) return x * x;
        if (n % 2 == 0)
            return myPow(myPow(x, n / 2), 2);
        return x * myPow(myPow(x, n / 2), 2);
    }
};
```

### Codestudio - Modular Exponentiation

-   Fast modular exponentiation
-   start with ans = 1;
-   while n > 0
    -   if n is odd, ans = ans \* x
    -   else x = x^2
    -   use 1LL to avoid overflow, ans mod them with m
    -   reduce n to n/2
-   return ans

```cpp
int modularExponentiation(int x, int n, int m)
{
    int ans = 1;
    while (n > 0) {
        if (n & 1) ans = (1LL * ans * x % m);
        x = (1LL * x * x) % m;
        n >>= 1;
    }
    return ans;
}
```
