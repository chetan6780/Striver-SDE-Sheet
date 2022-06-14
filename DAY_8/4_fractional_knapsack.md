# Fractional Knapsack Problem

Given weights and values of n items, we need to put these items in a knapsack of capacity W to get the maximum total value in the knapsack.

### Algorithm

1. Just sort the items by decreasing order of value/weight.
2. Get max portion of item.
3. Use double to not loose precision.
4. If item cannot fit, full take its fraction.

-   Time Complexity: O(n log n)
-   Space complexity: O(1)

### Code

```cpp
struct Item
{
    int value, weight;

    // Constructor
    Item(int value, int weight)
    {
        this->value = value;
        this->weight = weight;
    }
};

bool cmp(struct Item a, struct Item b)
{
    double r1 = (double)a.value / (double)a.weight;
    double r2 = (double)b.value / (double)b.weight;
    return r1 > r2;
}

double fractionalKnapsack(int W, struct Item arr[], int n)
{
    sort(arr, arr + n, cmp);

    int curWeight = 0;
    double finalvalue = 0.0;

    for (int i = 0; i < n; i++)
    {
        if (curWeight + arr[i].weight <= W)
        {
            curWeight += arr[i].weight;
            finalvalue += arr[i].value;
        }
        else
        {
            int remain = W - curWeight;
            finalvalue += arr[i].value * ((double)remain / (double)arr[i].weight);
            break;
        }
    }

    return finalvalue;
}
```

### Codestudio

```cpp
#include <bits/stdc++.h>

bool cmp(pair<int,int>a,pair<int,int>b){
    double r1=(double)a.second/(double)a.first;
    double r2=(double)b.second/(double)b.first;
    return r1>r2;
}


double maximumValue(vector<pair<int, int>>& arr, int n, int W)
{
    sort(arr.begin(), arr.end(), cmp);

    int curWeight = 0;
    double finalValue = 0.0;

    for (int i = 0; i < n; i++) {
        if (curWeight + arr[i].first <= W) {
            curWeight += arr[i].first;
            finalValue += arr[i].second;
        } else {
            int remain = W - curWeight;
            finalValue += arr[i].second * ((double)remain / (double)arr[i].first);
            break;
        }
    }

    return finalValue;
}
```
