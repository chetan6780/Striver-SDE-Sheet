# [144. Binary Tree Preorder Traversal](https://leetcode.com/problems/binary-tree-preorder-traversal/) 🌟

Given the root of a binary tree, return the preorder traversal of its nodes' values.

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

### O(N) Time O(N) space (function call stack), Recursive

-   if root is null, Return.
-   Visit the root (store data).
-   Traverse Left subtree.
-   Traverse Right subtree.

```cpp
class Solution {
public:
    vector<int> preorderTraversal(TreeNode* root) {
        vector<int> nodes;
        preorder(root, nodes);
        return nodes;
    }
private:
    void preorder(TreeNode* root, vector<int>& nodes) {
        if (!root) return;

        nodes.push_back(root -> val);
        preorder(root -> left, nodes);
        preorder(root -> right, nodes);
    }
};
```

### O(N) Time and O(N) extra space

-   Create a vector to store values and stack for operations
-   if tree is empty, return empty vector
-   else push root into stack
-   while stack is not empty
    -   pop the top element from stack
    -   push the value of the popped element into vector
    -   we want left to the top of stack, so we store it last so it appear on the top of stack
    -   if right node is not empty, push it into stack
    -   if left node is not empty, push it into stack

### Code

```cpp
class Solution{
public:
    vector<int> preorderTraversal(TreeNode *root){
        // Create a vector to store values and stack for operations
        vector<int> preorder;
        stack<TreeNode *> st;

        // if tree is empty, return empty vector
        if (root == NULL)
            return preorder;
        // else push root into stack
        st.push(root);

        // while stack is not empty
        while (!st.empty()){
            // pop the top element from stack
            TreeNode *node = st.top();
            st.pop();
            // push the value of the popped element into vector
            preorder.push_back(node->val);
            // we want left to the top of stack, so we store it last so it appear on the top of stack
            // if right node is not empty, push it into stack
            if (node->right != NULL)
                st.push(node->right);
            // if left node is not empty, push it into stack
            if (node->left != NULL)
                st.push(node->left);
        }
        return preorder;
    }
};
```

**Codestudio:**

```cpp
vector<int> getPreOrderTraversal(TreeNode* root)
{
    vector<int> ans;
    if (!root) return ans;
    stack<TreeNode*> st;
    TreeNode* node = root;
    while (node || !st.empty())
    {
        while (node)
        {
            ans.push_back(node->data);
            st.push(node);
            node = node->left;
        }
        node = st.top();
        st.pop();
        node = node->right;
    }
    return ans;
}
```

### Morris traversal - O(N) time and O(N) space.

-   Morris Traversal use the concept of Threaded Binary Tree. Here we bind the left and right pointers of the tree to the parent node.
-   [This video](https://www.youtube.com/watch?v=wGXB9OWhPTg) helps in understanding the idea.

```cpp
class Solution {
public:
    vector<int> preorderTraversal(TreeNode* root) {
        vector<int> nodes;
        while (root) {
            if (root -> left) {
                TreeNode* pre = root -> left;
                while (pre -> right && pre -> right != root) {
                    pre = pre -> right;
                }
                if (!pre -> right) {
                    pre -> right = root;
                    nodes.push_back(root -> val);
                    root = root -> left;
                } else {
                    pre -> right = NULL;
                    root = root -> right;
                }
            } else {
                nodes.push_back(root -> val);
                root = root -> right;
            }
        }
        return nodes;
    }
};
```
