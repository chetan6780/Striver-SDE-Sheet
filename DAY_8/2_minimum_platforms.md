# Minimum number of platforms

Given the arrival and departure times of all trains that reach a railway station, the task is to find the minimum number of platforms required for the railway station so that no train waits.

### Algorithm

-   Sort the arrival and departure times of trains.
-   Create two pointers i=1, and j=0 and a variable to store ans and current count platforms.
-   Run a loop while i<n and j<n and compare the ith element of arrival array and jth element of departure array.
-   If the arrival time is less than or equal to departure then one more platform is needed so increase the count, i.e. plat++ and increment i
-   Else if the arrival time greater than departure then one less platform is needed so decrease the count, i.e. plat– and increment j
-   Update the ans, i.e ans = max(ans, plat).
-   **Time Complexity: O(n log n)**
-   **space Complexity: O(1)**

### Code

```cpp
int findPlatform(int arr[], int dep[], int n)
{
    sort(arr, arr + n);
    sort(dep, dep + n);

    int pltNeeded = 1, result = 1;
    int i = 1, j = 0;

    while (i < n && j < n) {
        if (arr[i] <= dep[j]) {
            pltNeeded++;
            i++;
        } else if (arr[i] > dep[j]) {
            pltNeeded--;
            j++;
        }
        result = max(result, pltNeeded);
    }

    return result;
}
```
