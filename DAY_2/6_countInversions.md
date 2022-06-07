# Count Inversions

Given an array of integers. Find the Inversion Count in the array.

**Inversion Count:** For an array, inversion count indicates _how far (or close) the array is from being sorted_. If array is already _sorted_ then the inversion count is _0_. If an array is _sorted in the reverse order_ then the inversion count is the _maximum_.
Formally, two elements `a[i]` and `a[j]` form an inversion if `a[i] > a[j]` and `i < j`.

### Brute force (TLE)

-   find all i,j where `a[i]>a[j]`.
-   **TC: O(N^2)**
-   **SC: O(1)**

```cpp
typedef long long ll;
ll inversionCount(ll arr[], ll N)
{
    ll cnt = 0;
    for (ll i = 0; i < N; i++) {
        for (ll j = i + 1; j < N; j++) {
            if (arr[i] > arr[j])
                cnt++;
        }
    }
    return cnt;
}
```

### Using Merge Sort (AC)

-   **Merge sort:**
    -   We break array in 2 parts `(low,mid)` and `(mid+1,high)`, here `mid=(low+high)/2` always, until only 1 element remain in both array.
    -   Then in `merge function` we merge them by swapping or by comparing.
-   **TC: O(N\*logN)**, Complexity of merge sort.
-   **SC: O(N)**, If we are not allowed to modify the array we take the extra space.else it is **O(1)** space.

### Code

```cpp
typedef long long ll;

ll merge(ll arr[], ll temp[], ll left, ll mid, ll right)
{
    ll i, j, k;
    ll inv_count = 0;

    i = left; /* i is index for left subarray*/
    j = mid;  /* j is index for right subarray*/
    k = left; /* k is index for resultant merged subarray*/

    while ((i < mid) && (j <= right)) { // this is merge part
        if (arr[i] <= arr[j]) {
            temp[k++] = arr[i++];
        } else {
            temp[k++] = arr[j++];
            inv_count += (mid - i);
        }
    }

    // Copy the remaining elements of left subarray
    while (i < mid)
        temp[k++] = arr[i++];

    // Copy the remaining elements of right subarray
    while (j <= right)
        temp[k++] = arr[j++];

    // Copy back the merged elements to original array
    for (i = left; i <= right; i++)
        arr[i] = temp[i];

    return inv_count;
}

ll _mergeSort(ll arr[], ll temp[], ll left, ll right)
{
    ll mid, inv_count = 0;
    if (right > left) {
        // Divide the array into two parts and call
        mid = (right + left) / 2;

        // Inversion count = inversions(leftHalf) + Inversion(rightHalf)
        inv_count += _mergeSort(arr, temp, left, mid);
        inv_count += _mergeSort(arr, temp, mid + 1, right);

        // Merge the two parts
        inv_count += merge(arr, temp, left, mid + 1, right);
    }
    return inv_count;
}

ll inversionCount(ll arr[], ll N)
{
    ll* temp = (ll*)malloc(sizeof(ll) * N); // temporary array
    return _mergeSort(arr, temp, 0, N - 1);
}
```
