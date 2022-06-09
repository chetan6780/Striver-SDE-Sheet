# Add Two Numbers

You are given two non-empty linked lists representing two non-negative integers. The digits are stored in reverse order, and each of their nodes contains a single digit. Add the two numbers and return the sum as a linked list.

You may assume the two numbers do not contain any leading zero, except the number 0 itself.

### This question only have optimal solution

-   In an interview you should kill some time and ask interviewer some questions.
-   like what if l1 have more length than l2, or vice versa or what if both have same length, and other edge cases.
-   **TC: O(max(n1,n2))**
-   **SC: O(len(l1) + len(l2))**

### Code

```cpp
class Solution {
public:
    ListNode* addTwoNumbers(ListNode* l1, ListNode* l2)
    {
        // create a dummy node and temp pointer to point it.
        ListNode* dummy = new ListNode();
        ListNode* temp = dummy;
        int carry = 0; // Initialize carry with 0

        // until both l1 and l2 are not null and carry is 0
        while ((l1 != NULL || l2 != NULL) || carry) {
            int sum = 0; // Initialize sum with 0

            if (l1 != NULL) { // add l1->val in sum if its not null
                sum += l1->val;
                l1 = l1->next;
            }

            if (l2 != NULL) { // add l2->val in sum if its not null
                sum += l2->val;
                l2 = l2->next;
            }

            sum += carry; // add carry in sum
            carry = sum / 10;  // update carry with sum/10
            ListNode* node = new ListNode(sum % 10); // create a new node with sum%10
            temp->next = node; // point temp->next to node
            temp = temp->next; // point temp to node
        }
        return dummy->next; // return dummy->next
    }
};
```
