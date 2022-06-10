# Flattening a Linked List

### Solution

-   Start from last two linked list and merge them into one linked list.
-   recursively do it for all other linked list form end.
-   to merge linked list we will use merge sort algo.
-   We use modified merge sort for linked list to flatten the linked list and also maintain sorted order.

```cpp
Node* mergeTwoLists(Node* a, Node* b) {

    Node *temp = new Node(0);
    Node *res = temp;

    while(a != NULL && b != NULL) {
        if(a->data < b->data) {
            temp->bottom = a;
            temp = temp->bottom;
            a = a->bottom;
        }
        else {
            temp->bottom = b;
            temp = temp->bottom;
            b = b->bottom;
        }
    }

    if(a) temp->bottom = a;
    else temp->bottom = b;

    return res -> bottom;

}
Node *flatten(Node *root)
{
        if (root == NULL || root->next == NULL)
            return root;

        // go to the extreme right(end)
        root->next = flatten(root->next);

        // now merge last two linked lists
        root = mergeTwoLists(root, root->next);

        // return root of the merged list
        return root;
}
```

### Codestudio

```cpp
#include <bits/stdc++.h>
Node* merge(Node* a, Node* b){
    Node* temp = new Node(0), *res = temp;
    while(a&&b){
        if(a->data < b->data){
            temp->child = a;
            temp = temp->child;
            a = a->child;
        }else{
            temp->child = b;
            temp = temp->child;
            b = b->child;
        }
        temp->next = NULL;
    }
    if(a) temp->child = a;
    else temp->child = b;
    return res->child;
}

Node* flattenLinkedList(Node* head)
{
    if(head==NULL || head->next==NULL)return head;
    head->next = flattenLinkedList(head->next);
    head= merge(head,head->next);
    return head;
}
```
