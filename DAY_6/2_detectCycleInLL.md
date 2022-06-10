# Linked List Cycle

Given head, the head of a linked list, determine if the linked list has a cycle in it.

There is a cycle in a linked list if there is some node in the list that can be reached again by continuously following the next pointer. Internally, pos is used to denote the index of the node that tail's next pointer is connected to. Note that pos is not passed as a parameter.

Return true if there is a cycle in the linked list. Otherwise, return false.

### O(N) Time and O(N) space

- If there is a cycle in given linked list then same node must appear more than once.
- so, we create an unordered_set of nodes ands while traversing the list we check if the node is already present in the linked list.
- if its present we return true else we insert it into the unordered_set.
- finally after completing loop we return false. because there is no cycle.

### Code

```cpp
class Solution{
public:
    bool hasCycle(ListNode *head){
        unordered_set<ListNode *> s;
        ListNode *temp = head;
        while (temp != NULL){
            if (s.count(temp))
                return true;
            s.insert(temp);
            temp = temp->next;
        }
        return false;
    }
};
```

### O(N) Time and O(1) space - floyd's cycle detection algorithm

- Here fast pointer move 2 steps and slow pointer moves one step.
- If they meet each other while traversing then loop that means there is a cycle else not.

### Code

```cpp
class Solution{
public:
    bool hasCycle(ListNode *head){
        if (!head)
            return false;

        ListNode *slow = head, *fast = head;
        while (fast->next && fast->next->next){
            slow = slow->next;
            fast = fast->next->next;
            if (slow == fast)
                return true;
        }
        return false;
    }
};
```
