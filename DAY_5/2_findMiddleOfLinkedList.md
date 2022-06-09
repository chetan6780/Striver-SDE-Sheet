# Middle of the Linked List

Given the head of a singly linked list, return the middle node of the linked list.
If there are two middle nodes, return the **second middle node**.

### O(N) Time solution

-   We can traverse through the whole linked list and count the number of node.
-   Then we travel from start until we reach to the middle.
-   Then return temp, which is the middle node.

### Code

```cpp
class Solution{
public:
    ListNode *middleNode(ListNode *head){
        int n = 0;
        ListNode *temp = head;
        while (temp != NULL){
            n++;
            temp = temp->next;
        }
        int mid = n / 2;

        temp = head;
        while (mid--){
            temp = temp->next;
        }

        return temp;
    }
};
```

### O(N) Slow and Fast pointer

-   **NOTE: It works for all `Find middle` Questions.**
-   Each time, slow go 1 steps while fast go 2 steps.
-   When fast arrives at the end, slow will arrive right in the middle.
-   `fast != NULL` for odd number of nodes.
-   `fast->next != NULL` for even number of nodes.

### Code

```cpp
class Solution{
public:
    ListNode *middleNode(ListNode *head){
        int n = 0;
        ListNode *slow = head, *fast = head;
        while (fast != NULL && fast->next != NULL){
            slow = slow->next;
            fast = fast->next->next;
        }
        return slow;
    }
};
```
