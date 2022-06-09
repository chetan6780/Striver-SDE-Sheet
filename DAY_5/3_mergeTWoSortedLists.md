# Merge Two Sorted Lists

Merge two sorted linked lists and return it as a sorted list. The list should be made by splicing together the nodes of the first two lists.

### O(N+M) Time and O(N+M) space

-   If any list is empty, return the other list
-   Create dummy node to store new sorted lists
-   traverse until one of the list is empty
    -   if l1 is smaller, add l1 to new list, and move l1 to its next node
    -   if l2 is smaller, add l2 to new list, and move l2 to its next node
    -   move dummy pointer
-   if l2 is empty, add l1 to new list
-   if l1 is empty, add l2 to new list
-   Return next pointer of dummy node

### Code

```cpp
class Solution{
public:
    ListNode *mergeTwoLists(ListNode *l1, ListNode *l2){
        // If any list is empty, return the other list
        if (l1 == NULL) return l2;
        if (l2 == NULL) return l1;

        // Create dummy node to store new sorted lists
        ListNode *dummyNode = new ListNode();
        ListNode *dmptr = dummyNode; // pointer to dummyNode

        // traverse until one of the list is empty
        while (l1 != NULL && l2 != NULL){
            // if l1 is smaller, add l1 to new list, and move l1 to its next node
            if (l1->val <= l2->val){
                dmptr->next = new ListNode(l1->val);
                l1 = l1->next;
            }
            // if l2 is smaller, add l2 to new list, and move l2 to its next node
            else{
                dmptr->next = new ListNode(l2->val);
                l2 = l2->next;
            }
            // move dummy pointer
            dmptr = dmptr->next;
        }

        // if l2 is empty, add l1 to new list
        if (l1 != NULL)
            dmptr->next = l1;
        // if l1 is empty, add l2 to new list
        if (l2 != NULL)
            dmptr->next = l2;

        // Return next pointer of dummy node
        return dummyNode->next;
    }
};
```

### O(N+M) Time and O(1) space, in-place

-   if any list is empty, return the other list
-   l1 will always contain list of smaller value
    -   l1 will contain smaller val always;
    -   store l1 in result;
-   until any list is empty, run loop
    -   Create a temp node which points to nullptr
    -   while l1 has smaller element than l2, assign l1 to temp
    -   after loop l2 will have smaller value than l1
    -   by swapping l1 and l2, l1 will contain smaller value
-   return final result which is pointer to l1 list

### Code

```cpp
class Solution{
public:
    ListNode *mergeTwoLists(ListNode *l1, ListNode *l2){
        // if any list is empty, return the other list
        if (l1 == NULL) return l2;
        if (l2 == NULL) return l1;

        // l1 will always contain list of smaller value
        if (l1->val > l2->val)swap(l1, l2);   // l1 will contain smaller val always;
        ListNode *res = l1; // store l1 in result;

        // until any list is empty, run loop
        while (l1 != NULL && l2 != NULL){
            // Create a temp node which points to nullptr
            ListNode *temp = NULL;
            // while l1 has smaller element than l2, assign l1 to temp
            while (l1 != NULL && l1->val <= l2->val){
                temp = l1;
                l1 = l1->next;
            }
            // after loop l2 will have smaller value than l1
            temp->next = l2;
            // by swapping l1 and l2, l1 will contain smaller value
            swap(l1, l2);
        }
        //  return final result which is pointer to l1 list
        return res;
    }
};
```

```cpp
#include <bits/stdc++.h>
Node<int>* sortTwoLists(Node<int>* first, Node<int>* second)
{
    if(!first) return second;
    if(!second) return first;

    if(first->data > second->data) swap(first, second);
    Node<int>* res = first;

    while(first && second){
        Node<int>* temp = nullptr;
        while(first && first->data<=second->data){
            temp = first;
            first = first->next;
        }
        temp->next = second;
        swap(first, second);
    }
    return res;
}
```

### O(N+M) Time and O(1) Space, Recursive

-   We will recursively join two linked list such that they will be always sorted.

### Code

```cpp
class Solution{
public:
    ListNode *mergeTwoLists(ListNode *l1, ListNode *l2){
        if (l1 == NULL) return l2;
        if (l2 == NULL) return l1;

        // If l1 is smaller than l2 (val)
        if (l1->val <= l2->val){ // l1 move ahead with 1 node less.
            l1->next = mergeTwoLists(l1->next, l2);
            return l1;
        }
        else{ // l2 move ahead with 1 node less.
            l2->next = mergeTwoLists(l1, l2->next);
            return l2;
        }
    }
};
```
