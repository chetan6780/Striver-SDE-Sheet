# Merge Intervals

Given an array of intervals where intervals[i] = [start i, end i], merge all overlapping intervals, and return an array of the non-overlapping intervals that cover all the intervals in the input.

### O(N^2) Time Solution

-   Brute force.
-   sort the intervals by start time.
-   for every interval i, check if it overlaps with any interval j.
-   if it does, merge the two intervals.
-   if it doesn't, add it to the result.

### O(NlogN) Time O(N) Space Solution

-   Check for invalid case.
-   Sort the intervals by start time.
-   Take first pair of interval in `nextInterval`.
-   Iterate over intervals and check if `currInterval[0]<=nextInterval[1]`.
-   if they overlap, then change `nextInterval` pair to `max(nextInterval[1],currInterval[1])`.
-   else push `nextInterval` pair to result and change `nextInterval` pair to `currInterval`.

### Code

```cpp
// codestudio
vector<vector<int>> mergeIntervals(vector<vector<int>>& intervals)
{
    int n = intervals.size();
    vector<vector<int>> ans;
    sort(intervals.begin(), intervals.end());

    vector<int> nextInterval = intervals[0]; // first pair
    for (auto& interval : intervals) {
        if (interval[0] <= nextInterval[1]) {
            nextInterval[1] = max(nextInterval[1], interval[1]);
        } else {
            ans.push_back(nextInterval);
            nextInterval = interval;
        }
    }
    ans.push_back(nextInterval);
    return ans;
}
```

### O(NlogN) Time O(1) Space Solution

-   If we not consider the vector ans, which we have to return this problem can be solved without using `nextInterval` vector.
-   We can simply use `vector.back()` and do the operations on it.

### Code

```cpp
class Solution {
public:
    vector<vector<int>> merge(vector<vector<int>>& intervals)
    {
        int n = intervals.size();
        if (n <= 1) return intervals;

        sort(intervals.begin(), intervals.end());
        vector<vector<int>> ans;

        ans.push_back(intervals[0]);
        for (int i = 1; i < n; i++) {
            if (intervals[i][0] <= ans.back()[1])
                ans.back()[1] = max(ans.back()[1], intervals[i][1]);
            else
                ans.push_back(intervals[i]);
        }
        return ans;
    }
};
```
