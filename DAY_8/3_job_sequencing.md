# Job sequencing problem

Given a set of N jobs where each jobi has a deadline and profit associated with it. Each job takes 1 unit of time to complete and only one job can be scheduled at a time. We earn the profit if and only if the job is completed by its deadline. The task is to find the number of jobs done and the maximum profit obtainable.

### Algorithm

1. Sort all jobs in decreasing order of profit.
2. Iterate on jobs in decreasing order of profit.For each job , do the following :

For each job find an empty time slot from deadline to 0. If found empty slot put the job in the slot and mark this slot filled.

### Code

```cpp
struct Job {
    char id;
    int dead;
    int profit;
};

bool comparison(Job a, Job b)
{
    return (a.profit > b.profit);
}

vector<int> JobScheduling(Job arr[], int n)
{
    vector<int> v;
    sort(arr, arr + n, comparison);
    int mx = arr[0].dead;

    for (int i = 1; i < n; i++)
        mx = max(mx, arr[i].dead);

    int slot[mx + 1];

    for (int i = 0; i <= mx; i++)
        slot[i] = -1;

    int countJobs = 0, jobProfit = 0;

    for (int i = 0; i < n; i++) {
        for (int j = arr[i].dead; j > 0; j--) {
            if (slot[j] == -1) {
                slot[j] = i;
                countJobs++;
                jobProfit += arr[i].profit;
                break;
            }
        }
    }
    v.push_back(countJobs);
    v.push_back(jobProfit);
    return v;
}
```

### Codestudio

```cpp
#include <bits/stdc++.h>

struct jobStruct {
    int deadline;
    int profit;
};

bool static comparator(struct jobStruct f1, jobStruct f2)
{
    return f1.profit > f2.profit;
}

int jobScheduling(vector<vector<int>>& jobs)
{
    int n = jobs.size();
    struct jobStruct job[n];
    for (int i = 0; i < n; i++) {
        job[i].deadline = jobs[i][0];
        job[i].profit = jobs[i][1];
    }

    sort(job, job + n, comparator);

    int mx = 0;
    for (int i = 0; i < n; i++) {
        mx = max(mx, job[i].deadline);
    }

    vector<int> slot(mx + 1, -1);
    int jobProfit = 0;
    for (int i = 0; i < n; i++) {
        for (int j = job[i].deadline; j > 0; j--) {
            if (slot[j] == -1) {
                slot[j] = 0;
                jobProfit += job[i].profit;
                break;
            }
        }
    }
    return jobProfit;
}
```

### using disjoint set

-   GFG: [link](https://www.geeksforgeeks.org/job-sequencing-using-disjoint-set-union/)
