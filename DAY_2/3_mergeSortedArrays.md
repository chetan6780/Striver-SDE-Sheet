# Merge Sorted Array

### O(M+N) Time and O(M+N) space

-   Create new array with m+n elements.
-   Traverse through both the given array, find min and insert in the new array.

### O(M\*N) without using extra Space

-   Traverse through both the given array
-   If arr1[i]>arr2[i] then swap the elements and sort the second array.(here sorting means just put swapped element at its right position not real sorting)

### O(M+N) Time and O(1) Space

-   self explanatory.

### Code

```cpp
// leetcode
class Solution{
public:
    void merge(vector<int> &nums1, int m, vector<int> &nums2, int n)
    {
        int a = m - 1; // last index of nums1
        int b = n - 1; // last index of nums2
        int i = m + n - 1; // last index of extended nums1(with 0 wala)
        while (a >= 0 && b >= 0) // while we not reach start of any array
        {
            if (nums1[a] > nums2[b])
            {
                nums1[i] = nums1[a];
                i--, a--;
            }
            else
            {
                nums1[i] = nums2[b];
                i--, b--;
            }
        }
        while (b >= 0) // if there are elements remaining in b then put them in back
        {
            nums1[i] = nums2[b];
            i--, b--;
        }
    }
};
```

### Using GAP algorithm

-   **O(Log2N \* O(N))** time and **O(1)** space
-   We Will take GAP between two pointers and if the are not sorted we swap them.
-   first **GAP = ceil(n1+n2/2)** then next time it will be **half of previous GAP**.
-   If GAP is **1** then next time we **stop**.

---

### GFG Question

-   We point i to the last of array 1 and j to the start of array 2.
-   in while loop , if arr1[i]>arr2[j] then swap the elements.
-   finally sort the second array.
-   **Time Complexity**: O(NlogN)
-   **Space Complexity**: O(1)

```cpp
class Solution{
public:
	//Function to merge the arrays.
	void merge(long long arr1[], long long arr2[], int n, int m){
		// code here
		long long i = n - 1, j = 0;
		while (i >= 0 && j < m){
			if (arr1[i] > arr2[j]){
				swap(arr1[i], arr2[j]);
			}
			i--, j++;
		}
		sort(arr1, arr1 + n);
		sort(arr2, arr2 + m);
	}
};
```

### Reference

-   [GFG](https://www.geeksforgeeks.org/efficiently-merging-two-sorted-arrays-with-o1-extra-space/)
