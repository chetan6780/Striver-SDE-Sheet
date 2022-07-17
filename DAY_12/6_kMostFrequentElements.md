# K Most Frequent Elements

You are given an Integer array ‘ARR’ and an Integer ‘K’. Your task is to find the ‘K’ most frequent elements in ‘ARR’. Return the elements sorted in ascending order.

### Priority Queue + Map

-   Self explanatory code.

### Code

```cpp
#include <bits/stdc++.h>
vector<int> KMostFrequent(int n, int k, vector<int>& arr)
{
    map<int, int> mp;
    for (int i = 0; i < n; i++) {
        mp[arr[i]]++;
    }
    vector<int> ans;
    priority_queue<pair<int, int>> pq;
    for (auto it : mp) {
        pq.push({it.second, it.first});
    }
    for (int i = 0; i < k; i++) {
        ans.push_back(pq.top().second);
        pq.pop();
    }
    sort(ans.begin(), ans.end());
    return ans;
}
```
