# [94. Binary Tree Inorder Traversal](https://leetcode.com/problems/binary-tree-inorder-traversal/) 🌟

Given the root of a binary tree, return the inorder traversal of its nodes' values.

### Definition for a binary tree node.

```cpp
struct TreeNode {
    int val;
    TreeNode *left;
    TreeNode *right;
    TreeNode() : val(0), left(nullptr), right(nullptr) {}
    TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
    TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
};
```

### O(N) Time and O(N) auxillary space, recursive

-   if root is null, Return.
-   Traverse Left subtree.
-   Visit the root (store data).
-   Traverse Right subtree.

### Code

```cpp
class Solution {
private:
    void inorder(TreeNode* root, vector<int> &ans){
        if(!root) return;
        inorder(root->left,ans);
        ans.push_back(root->val);
        inorder(root->right,ans);
    }
public:
    vector<int> inorderTraversal(TreeNode* root) {
        vector<int> ans;
        inorder(root,ans);
        return ans;
    }
};
```

### O(N) Time and O(N) Space, itterative

-   if root is null, Return.
-   while true
    -   if left node present, then traverse all the way left.& push node in the stack.
    -   if stack is empty, break the loop.
    -   get the top in node variable and push it in ans vector.
    -   now move to the right.
-   return inorder(ans) vector.

### Code

```cpp
class Solution{
public:
    vector<int> inorderTraversal(TreeNode *root){
        TreeNode *node = root;
        stack<TreeNode *> st;
        vector<int> inorder;

        while (true){
            while (node){
                st.push(node);
                node = node->left;
            }
            if (st.empty())
                break;
            node = st.top();
            st.pop();
            inorder.push_back(node->val);
            node = node->right;
        }
        return inorder;
    }
};
```

### Same solution as above but code difference

```cpp
class Solution{
public:
    vector<int> inorderTraversal(TreeNode *root){
        stack<TreeNode *> st;
        vector<int> inorder;
        TreeNode *node = root;

        while (true){
            if (node!=NULL){
                st.push(node);
                node = node->left;
            }else{
            if (st.empty())
                break;
            node = st.top();
            st.pop();
            inorder.push_back(node->val);
            node = node->right;
            }
        }
        return inorder;
    }
};
```

**Codestudio:**

```cpp
vector<int> getInOrderTraversal(TreeNode* root)
{
    vector<int> ans;
    if (!root)
        return ans;
    stack<TreeNode*> st;
    TreeNode* node = root;
    while (node || !st.empty()) {
        while (node) {
            st.push(node);
            node = node->left;
        }
        node = st.top();
        st.pop();
        ans.push_back(node->data);
        node = node->right;
    }
}
```

### O(N) Time and O(1) Space, Morris Traversal

-   Morris Traversal use the concept of Threaded Binary Tree. Here we bind the left and right pointers of the tree to the parent node.
-   [This video](https://www.youtube.com/watch?v=wGXB9OWhPTg) helps in understanding the idea.

### Code

```cpp
class Solution {
public:
    vector<int> inorderTraversal(TreeNode* root) {
        vector<int> inorder;
        while (root) {
            if (!root -> left) {
                inorder.push_back(root -> val);
                root = root -> right;
            } else {
                TreeNode* predecessor = root -> left;
                while (predecessor -> right && predecessor -> right != root) {
                    predecessor = predecessor -> right;
                }
                if (!predecessor -> right) {
                    predecessor -> right = root;
                    root = root -> left;
                } else {
                    predecessor -> right = NULL;
                    inorder.push_back(root -> val);
                    root = root -> right;
                }
            }
        }
        return inorder;
    }
};
```
