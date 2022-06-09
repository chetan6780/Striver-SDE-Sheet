# Delete Node in a Linked List

Write a function to delete a node in a singly-linked list. You will not be given access to the head of the list, instead you will be given access to the node to be deleted directly.

It is guaranteed that the node to be deleted is not a tail node in the list.

### Solution

-   We just need to copy the next node's value to the current node and then delete the next node.

### Code

```cpp
class Solution {
public:
    void deleteNode(ListNode* node){
        node->val = node->next->val;
        node->next = node->next->next;
    }
};
```

### MUST READ:

**let's analyze why this problem **isn't** a good interview question.**

```
The whole point of asking any candidates a linked list problem is to test if the candidates think about edge cases, including:

1. Dereferencing Null Pointer, usually targeting tail pointer
2. When given Head is None
3. When there are duplications in the list
```

> This question specifically mentioned all the above edge cases and extracted them out for you Someone who can solve this problem might not even think of all the edge cases, which can backfire on them in real interview settings
