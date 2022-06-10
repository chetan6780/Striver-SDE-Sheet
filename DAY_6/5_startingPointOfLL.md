# Linked List Cycle II

Given the head of a linked list, return the node where the cycle begins. If there is no cycle, return null.

There is a cycle in a linked list if there is some node in the list that can be reached again by continuously following the next pointer. Internally, pos is used to denote the index of the node that tail's next pointer is connected to (0-indexed). It is -1 if there is no cycle. Note that pos is not passed as a parameter.

Do not modify the linked list.

### fast ans slow pointer Solution

-   We can use fast and slow pointer method to find the cycle.
-   We move fast by 2 steps and slow by 1 step.
-   When they both are equal, we have found the cycle, else we return null.
-   If cycle found set fast pointer to head again and move both by 1 step.
-   when both of then are equal, we have found the start of the cycle.
-   return the fast/slow pointer.
-   **TC: O(N)**
-   **SC: O(1)**

```cpp
class Solution {
public:
    ListNode* detectCycle(ListNode* head)
    {
        // base case
        if (head == NULL || head->next == NULL) return NULL;

        ListNode *slow = head, *fast = head;
        while (fast->next != NULL && fast->next->next != NULL) {
            slow = slow->next;
            fast = fast->next->next;
            if (slow == fast) {
                fast = head;
                while (slow != fast) {
                    slow = slow->next;
                    fast = fast->next;
                }
                return fast;
            }
        }
        return NULL;
    }
};
```
