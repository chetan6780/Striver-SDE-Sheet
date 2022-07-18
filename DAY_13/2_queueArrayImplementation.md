# Implementation of Queue using Array

### Array

```cpp
class Queue {
    int* arr;
    int start, end;

public:
    Queue()
    {
        arr = new int[5001]; // Required size
        start = 0;
        end = 0;
    }

    bool isEmpty()
    {
        return start == end;
    }

    void enqueue(int data)
    {
        arr[end++] = data;
    }

    int dequeue()
    {
        if (!isEmpty())
            return arr[start++];
        return -1;
    }

    int front()
    {
        if (!isEmpty())
            return arr[start];
        return -1;
    }
};
```

### Vector

```cpp
class Queue {
    vector<int> q;

public:
    Queue()
    {
        q.resize(0);
    }

    bool isEmpty()
    {
        return q.size() == 0;
    }

    void enqueue(int data)
    {
        q.push_back(data);
    }

    int dequeue()
    {
        if (!isEmpty()) {
            int data = q[0];
            q.erase(q.begin());
            return data;
        }
        return -1;
    }

    int front()
    {
        if (!isEmpty()) {
            return q[0];
        }
        return -1;
    }
};
```
