### Aggressive Cows/Chess Tournament

There is a new barn with N stalls and C cows. The stalls are located on a straight line at positions `x1,….,xN (0 <= xi <= 1,000,000,000)`. We want to assign the cows to the stalls, such that the minimum distance between any two of them is as large as possible. What is the largest minimum distance?

### Brute force

-   For every distance between 1 to `maxDist` try to find the minimum distance between any two cows by placing cows d distance apart.
-   **TC: O(n\*c)**
-   **SC: O(1)**

### Code

```cpp
bool isPossible(vector<int> inp, int dist, int cows)
{
    int n = inp.size();
    int k = inp[0];
    cows--;
    for (int i = 1; i < n; i++) {
        if (inp[i] - k >= dist) {
            cows--;
            if (!cows) {
                return true;
            }
            k = inp[i];
        }
    }
    return false;
}

int chessTournament(vector<int> positions, int n, int c)
{
    int ans = INT_MIN;
    sort(positions.begin(), positions.end());
    int maxDist = positions[n - 1] - positions[0];

    for (int d = 1; d <= maxDist; d++) {
        bool possible = isPossible(positions, d, c);
        if (possible) {
            ans = max(ans, d);
        }
    }
    return ans;
}
```

### Binary Search

-   **TC: O(n\*log(c))**

### Code

```cpp
bool isPossible(vector<int> inp, int dist, int cows)
{
    int n = inp.size();
    int k = inp[0];
    cows--;
    for (int i = 1; i < n; i++) {
        if (inp[i] - k >= dist) {
            cows--;
            if (!cows) {
                return true;
            }
            k = inp[i];
        }
    }
    return false;
}

int chessTournament(vector<int> positions, int n, int c)
{
    sort(positions.begin(), positions.end());

    int low = 1, high = positions[n - 1] - positions[0];
    while (low <= high) {
        int mid = (low + high) >> 1;
        if (isPossible(positions, mid, c)) {
            low = mid + 1;
        } else {
            high = mid - 1;
        }
    }
    return high;
}
```
