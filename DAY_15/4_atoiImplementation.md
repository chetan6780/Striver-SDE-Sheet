# String to Integer (atoi)

Implement the myAtoi(string s) function, which converts a string to a 32-bit signed integer (similar to C/C++'s atoi function).

The algorithm for `myAtoi(string s)` is as follows:

> In an Interview be sure you confirm following assumptions with the interviewer

1. Read in and ignore any leading whitespace.
2. Check if the next character (if not already at the end of the string) is '-' or '+'. Read this character in if it is either. This determines if the final result is negative or positive respectively. Assume the result is positive if neither is present.
3. Read in next the characters until the next non-digit character or the end of the input is reached. The rest of the string is ignored.
4. Convert these digits into an integer (i.e. "123" -> 123, "0032" -> 32). If no digits were read, then the integer is 0. Change the sign as necessary (from step 2).
5. If the integer is out of the 32-bit signed integer range [-231, 231 - 1], then clamp the integer so that it remains in the range. Specifically, integers less than -231 should be clamped to -231, and integers greater than 231 - 1 should be clamped to 231 - 1.
6. Return the integer as the final result.

### Solution

We only need to handle four cases:

-   discards all leading whitespace
-   sign of the number
-   overflow
-   invalid input

```cpp
class Solution {
public:
    int myAtoi(string s)
    {
        int sign = 1, num = 0, i = 0;

        while (s[i] == ' ') i++;

        if (s[i] == '-' || s[i] == '+') {
            if (s[i] == '-') sign = -1;
            i++;
        }

        while (s[i] >= '0' && s[i] <= '9') {
            // To handle overflow
            if ((num > INT_MAX / 10) || ((num == INT_MAX / 10) && (s[i] - '0' > 7))) {
                return (sign == 1) ? INT_MAX : INT_MIN;
            }
            num = 10 * num + (s[i++] - '0');
        }
        return num * sign;
    }
};
```

### Codestudio

-   Codestudio problem is not exact implementation of atoi but it's like find numbers in string.

### Code

```cpp
int atoi(string str)
{
    int sign = 1;
    int i = 0;
    int ans = 0;
    if (str[i] == '-') {
        sign = -1;
        i++;
    }
    for (; i < str.length(); i++) {
        if (str[i] - '0' >= 0 && str[i] - '0' <= 9) {
            ans = ans * 10 + str[i] - '0';
        }
    }
    return ans * sign;
}
```
