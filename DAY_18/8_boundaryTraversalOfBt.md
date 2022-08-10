# Boundary Traversal of Binary Tree

### Solution

-   Add left boundaries.
-   Add leave nodes.
-   Add right boundaries.

### Code

```cpp
#include <bits/stdc++.h>

bool isLeaf(TreeNode<int>* root){
    if(root->left == NULL && root->right == NULL){
        return true;
    }
    return false;
}

void addLeftBoundary(TreeNode<int>* root , vector<int> &res){
    TreeNode<int>* curr = root->left;
    while(curr){
        if(isLeaf(curr)==false)res.push_back(curr->data);
        if(curr->left)curr = curr->left;
        else curr = curr->right;
    }
}

void addRightBoundary(TreeNode<int>* root , vector<int> &res){
    TreeNode<int>* curr = root->right;
    stack<TreeNode<int>*> st;
    while(curr){
        if(isLeaf(curr)==false)st.push(curr);
        if(curr->right)curr = curr->right;
        else curr = curr->left;
    }
    while(!st.empty()){
        res.push_back(st.top()->data);
        st.pop();
    }
}

void addLeaves(TreeNode<int>* root , vector<int> &res){
    if(!root)return;
    if(isLeaf(root)==true){
        res.push_back(root->data);
        return;
    }
    if(root->left)addLeaves(root->left,res);
    if(root->right)addLeaves(root->right,res);
}


vector<int> traverseBoundary(TreeNode<int>* root){
    vector<int> res;
    if(!root)return res;
    if(isLeaf(root)==false){
        res.push_back(root->data);
    }
    addLeftBoundary(root,res);
    addLeaves(root,res);
    addRightBoundary(root,res);
    return res;
}
```
