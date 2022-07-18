# Sort a stack

### Recursive Solution

1. Insert function.

    - If stack is empty _OR_ `x` is the largest element, then we can directly insert it at last position.
    - else we need to insert `x` at it's correct position.
    - Get the top element of the stack and reduce its size by 1.
    - Insert `x` recursively.
    - finally insert value which is poped.

2. Sort function.
    - If stack contains only one element then it is sorted iteself.Return.
    - Get the last element of the stack.
    - Reduce the size of input for recursion.
    - Recursively sort remaining the stack which has one element less.
    - Insert the element in sorted stack at its right position.

### Code

```cpp
#include <bits/stdc++.h>

void insertSorted(stack<int>& st, int x) {
    if (st.empty() || st.top() <= x) {
        st.push(x);
    } else {
        int temp = st.top();
        st.pop();
        insertSorted(st, x);
        st.push(temp);
    }
}

void sortStack(stack<int>& stack)
{
    if (stack.empty())
        return;
    int x = stack.top();
    stack.pop();
    sortStack(stack);
    insertSorted(stack, x);
}
```
