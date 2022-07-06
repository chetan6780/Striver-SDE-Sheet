# Allocate Pages/Books

### Binary Search

### Code

```cpp
#include <bits/stdc++.h>

bool isPossible(int n, int m, vector<int> time, long long int mid)
{
    int day = 1;
    long long reqTime = 0;
    for (int i = 0; i < m; i++) {
        if (reqTime + time[i] <= mid) {
            reqTime += time[i];
        } else {
            day++;
            if (day > n || time[i] > mid) {
                return false;
            }
            reqTime = time[i];
        }
    }
    return true;
}
long long ayushGivesNinjatest(int n, int m, vector<int> time)
{
    long long start = 0;
    long long end = accumulate(time.begin(), time.end(), 0LL);

    long long ans = -1;
    while (start <= end) {
        long long mid = start + (end - start) / 2;
        if (isPossible(n, m, time, mid)) {
            ans = mid;
            end = mid - 1;
        } else {
            start = mid + 1;
        }
    }
    return ans;
}
```
