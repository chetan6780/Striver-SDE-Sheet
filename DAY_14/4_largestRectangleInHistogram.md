# Largest Rectangle in Histogram

Given an array of integers heights representing the histogram's bar height where the width of each bar is 1, return the area of the largest rectangle in the histogram.

### Brute force

-   For every element in array find how much it can go to left and how much it can go to right.
-   Then the area is the product of `a[i] * (right - left + 1)`.
-   **TC: O(n\*n)**
-   **SC: O(1)**

### Stack Solution

-   Using monotonic stack pre calculate the left and right smaller element indexes.
-   The the maximum area is the product of `a[i] * (right - left + 1)`.
-   **TC: O(n)**
-   **SC: O(n)**, O(3\*n)

```cpp
class Solution {
public:
    int largestRectangleArea(vector<int>& heights)
    {
        int n = heights.size();
        vector<int> smallerLeft(n), smallerRight(n);
        stack<int> st; // monotonic stack - increasing order bottom-top

        for (int i = 0; i < n; i++) { // find next smaller element to the left
            while (!st.empty() && heights[st.top()] >= heights[i]) {
                st.pop();
            }
            smallerLeft[i] = st.empty() ? -1 : st.top();
            st.push(i);
        }
        while (!st.empty())
            st.pop();

        for (int i = n - 1; i >= 0; i--) { // find next smaller element to the right
            while (!st.empty() && heights[st.top()] >= heights[i]) {
                st.pop();
            }
            smallerRight[i] = st.empty() ? n : st.top();
            st.push(i);
        }

        int maxArea = 0;
        for (int i = 0; i < n; i++) {
            maxArea = max(maxArea, (smallerRight[i] - smallerLeft[i] - 1) * heights[i]);
        }
        return maxArea;
    }
};
```

### stack solution 2

-   Single pass solution
-   for an element their next smaller element and prev smaller element can be found in stack.
-   Check [this video](https://youtu.be/jC_cWLy7jSI) for more details.
-   **TC: O(n)**, Single pass
-   **SC: O(n)**

```cpp
class Solution {
public:
    int largestRectangleArea(vector<int>& heights)
    {
        int n = heights.size();
        if (n == 0) return 0;
        stack<int> st;

        int maxArea = 0;
        for (int i = 0; i <= n; i++) {
            int height = (i == n) ? 0 : heights[i];
            while (!st.empty() && height <= heights[st.top()]) {
                int height = heights[st.top()];
                st.pop();
                int width = st.empty() ? i : i - st.top() - 1;
                maxArea = max(maxArea, height * width);
            }
            st.push(i);
        }
        return maxArea;
    }
};
```
