# Valid Parentheses

Given a string s containing just the characters '(', ')', '{', '}', '[' and ']', determine if the input string is valid.

An input string is valid if:

1. Open brackets must be closed by the same type of brackets.
2. Open brackets must be closed in the correct order.

### O(N) Time and O(N) Space, straightforward solution

- if the string is empty, return true
- if the string has an odd number of characters, return false
- Create a stack to store parenthesis.
- if character is any opening parenthesis, push it to the stack
- after first if, if stack is empty, which means the character is closing parenthesis, return false
- else
  - current character is matching parenthesis of top char of stack, pop that opening character from stack.
  - else push it in the stack.
- return true if stack is empty else false.

### Code

```cpp
class Solution{
public:
    bool isValid(string s){
        stack<char> st;
        int n = s.size();
        if ((n & 1))
            return false;
        for (int i = 0; i < n; i++){
            if (s[i] == '(' || s[i] == '[' || s[i] == '{'){
                st.push(s[i]);
            }
            else{
                if (st.empty()) return false;
                if ((s[i] == ')' && st.top() == '(') || (s[i] == ']' && st.top() == '[') || (s[i] == '}' && st.top() == '{')){
                    st.pop();
                }else{
                    st.push(s[i]);
                }
            }
        }
        return st.empty();
    }
};
```

### Some slight simplification

- we don't need to push extra closing parenthesis in the stack, if extra parenthesis appears return false.

### Code

```cpp
class Solution{
public:
    bool isValid(string s){
        stack<char> st;
        int n = s.size();
        if ((n & 1)) return false;
        for (int i = 0; i < n; i++){
            if (s[i] == '(' || s[i] == '[' || s[i] == '{'){
                st.push(s[i]);
            }
            else{
                if (st.empty() || (s[i] == ')' && st.top() != '(') || (s[i] == ']' && st.top() != '[') || (s[i] == '}' && st.top() != '{'))
                    return false;
                st.pop();
            }
        }
        return st.empty();
    }
};
```

### Code

```cpp
class Solution {
public:
    bool isValid(string s) {
        stack<char> st;
        for(auto x: s){
            if(x == '('||x == '['||x == '{')
                st.push(x);
            else{
                if(st.empty())
                    return false;
                char c = st.top();
                st.pop();
                if(c == '(' && x != ')')
                    return false;
                if(c == '[' && x != ']')
                    return false;
                if(c == '{' && x != '}')
                    return false;
            }
        }
        return st.empty();
    }
};
```

