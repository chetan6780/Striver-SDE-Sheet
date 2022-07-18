# Implementation of Stack using Array

### Array

```cpp
// Stack class.
class Stack {
    int stSize;
    int* arr;
    int topIdx;

public:
    Stack(int capacity)
    {
        topIdx = -1;
        stSize = capacity;
        arr = new int[stSize];
    }

    void push(int num)
    {
        if (topIdx < stSize - 1) {
            topIdx++;
            arr[topIdx] = num;
        }
    }

    int pop()
    {
        if (topIdx >= 0) {
            int temp = arr[topIdx];
            topIdx--;
            return temp;
        }
        return -1;
    }

    int top()
    {
        if (topIdx >= 0) {
            return arr[topIdx];
        }
        return -1;
    }

    int isEmpty()
    {
        return topIdx == -1;
    }

    int isFull()
    {
        return topIdx == stSize - 1;
    }
};
```

### Vector

```cpp
// Stack class.
class Stack {
    vector<int> st;
    int stSize;

public:
    Stack(int capacity)
    {
        stSize = capacity;
    }

    void push(int num)
    {
        if (!isFull()) {
            st.push_back(num);
        }
    }

    int pop()
    {
        if (!isEmpty()) {
            int num = st.back();
            st.pop_back();
            return num;
        }
        return -1;
    }

    int top()
    {
        if (!isEmpty()) {

            int num = st.back();
            return num;
        }
        return -1;
    }

    int isEmpty()
    {
        return st.empty();
    }

    int isFull()
    {
        return st.size() == stSize;
    }
};
```
