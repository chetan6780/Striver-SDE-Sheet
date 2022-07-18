# stack using queue

### 2 Queue

```cpp
#include <bits/stdc++.h>

class Stack {
    queue<int> q1, q2;

public:
    Stack(){}

    int getSize()
    {
        return q1.size();
    }

    bool isEmpty()
    {
        return q1.empty();
    }

    void push(int element)
    {
        q2.push(element);
        while (!q1.empty()) {
            q2.push(q1.front());
            q1.pop();
        }
        swap(q1,q2);
    }

    int pop()
    {
        if (!isEmpty()) {
            int temp = q1.front();
            q1.pop();
            return temp;
        }
        return -1;
    }

    int top()
    {
        if (!isEmpty()) {
            return q1.front();
        }
        return -1;
    }
};
```

### 1 Queue

```cpp
#include <bits/stdc++.h>

class Stack {
    queue<int> q1;

public:
    Stack() {}

    int getSize()
    {
        return q1.size();
    }

    bool isEmpty()
    {
        return q1.empty();
    }

    void push(int element)
    {   // Optimized 1 Queue here
        int sz = q1.size();
        q1.push(element);
        for (int i = 0; i < sz; i++) {
            int temp = q1.front();
            q1.pop();
            q1.push(temp);
        }
    }

    int pop()
    {
        if (!isEmpty()) {
            int temp = q1.front();
            q1.pop();
            return temp;
        }
        return -1;
    }

    int top()
    {
        if (!isEmpty()) {
            return q1.front();
        }
        return -1;
    }
};
```
