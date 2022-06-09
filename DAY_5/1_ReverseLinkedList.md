# Reverse Linked List

Given the head of a singly linked list, reverse the list, and return the reversed list.

### O(N) Time and O(1) space, iterative

-   Initialize three pointers prev as NULL, curr as head and next as NULL.
-   Iterate through the linked list. In loop, do following.
    -   Before changing next of current, store next node
        next = curr->next
    -   Now change next of current This is where actual reversing happens
        curr->next = prev
    -   Move prev and curr one step forward
        prev = curr
        curr = next

### Code

```cpp
class Solution {
public:
    ListNode* reverseList(ListNode* head) {
        ListNode *prev = NULL,*next=NULL,*curr=head;
        while(curr!=NULL){
            next=curr->next;
            curr->next=prev;
            prev=curr;
            curr=next;
        }
        return prev;
    }
};
```

### O(N) Time and O(1) space, recursive

1. Divide the list in two parts - first node and
   rest of the linked list.
2. Call reverse for the rest of the linked list.
3. Link rest to first.
4. Fix head pointer.

### Code

```cpp
class Solution {
public:
    ListNode* reverseList(ListNode* head) {
        if(head==NULL || head->next==NULL) return head;

        ListNode *rest = reverseList(head->next);

        head->next->next=head;
        head->next=NULL;

        return rest;
    }
};
```
