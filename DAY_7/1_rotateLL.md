# Rotate Linked list

Given the `head` of a linked list, rotate the list to the right by `k` places.

### Brute force

-   Pick up the last node and put it to the first, do this k times.
-   **TC: O(k\*N)**
-   **SC: O(1)**

### Optimized

-   Get the length of the linked list.
-   point last nodes next to head.
-   point the len-kth nodes next to null
-   **TC: O(N)**
-   **SC: O(1)**

### Code

```cpp
class Solution {
public:
    ListNode* rotateRight(ListNode* head, int k) {
        // edge cases
        if (!head || !head->next || k == 0) return head;

        // compute the length
        ListNode *cur = head;
        int len = 1;
        while (cur->next && ++len)
            cur = cur->next;

        // go till that node
        cur->next = head;
        k = k % len;
        k = len - k;
        while (k--) cur = cur->next;

        // make the node head and break connection
        head = cur->next;
        cur->next = NULL;

        return head;
    }
};
```
