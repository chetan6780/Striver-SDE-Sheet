# Palindrome Linked List

Given the `head` of a singly linked list, return `true` if it is a palindrome.

### Brute force

-   Store the element of the linked list in the array or string and check if the array is palindrome.
-   **TC: O(N)**
-   **SC: O(N)**

### Optimized

-   Use two pointers to traverse the linked list.
-   We find the middle of linked list and reverse the second half of the linked list.
-   Then we compare the first half and the second half of the linked list.
-   if the second half of the linked list reaches to null return true. Otherwise return false.
-   **TC: O(N)**
-   **SC: O(1)**

### Code

```cpp
class Solution {
    ListNode* reverseList(ListNode* head)
    {
        ListNode* prev = NULL;
        ListNode* next = NULL;
        while (head != NULL) {
            next = head->next;
            head->next = prev;
            prev = head;
            head = next;
        }
        return prev;
    }

public:
    bool isPalindrome(ListNode* head)
    {
        if (head == NULL || head->next == NULL) return true;

        ListNode *slow = head, *fast = head;
        while (fast->next != NULL && fast->next->next != NULL) {
            slow = slow->next;
            fast = fast->next->next;
        }

        slow->next = reverseList(slow->next);
        slow = slow->next;

        while (slow != NULL) {
            if (head->val != slow->val) return false;
            head = head->next;
            slow = slow->next;
        }
        return true;
    }
};
```
