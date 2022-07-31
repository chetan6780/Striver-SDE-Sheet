# [145. Binary Tree Postorder Traversal](https://leetcode.com/problems/binary-tree-postorder-traversal/) 🌟

Given the root of a binary tree, return the postorder traversal of its nodes' values.

### O(N) Time and O(N) Auxiliary Space, recursive

-   if root is null return.
-   travel to left.
-   travel to right.
-   store the value.

### Code

```cpp
class Solution {
private:
    void postorder(TreeNode* root, vector<int> &ans){
        if(!root)return;
        postorder(root->left,ans);
        postorder(root->right,ans);
        ans.push_back(root->val);
    }
public:
    vector<int> postorderTraversal(TreeNode* root) {
        vector<int> ans;
        postorder(root,ans);
        return ans;
    }
};
```

### O(N) Time and O(2N) space, Iterative

**NOTE:** _Here instead of ***2 Stack*** I have used ***1 Stack and 1 vector*** and reversed the vector at the end._

More detail explanation watch [this](https://www.youtube.com/watch?v=2YBhNLodD8Q) 4 min video.

### Code

```cpp
class Solution{
public:
    vector<int> postorderTraversal(TreeNode *root){
        vector<int> postorder;
        stack<TreeNode *> st;

        if (root == NULL)
            return postorder;
        st.push(root);

        while (!st.empty()){
            TreeNode *node = st.top();
            st.pop();
            postorder.push_back(node->val);
            if (node->left != NULL)
                st.push(node->left);
            if (node->right != NULL)
                st.push(node->right);

        }
        reverse(postorder.begin(), postorder.end());
        return postorder;
    }
};
```

### O(N) Time and O(N) Space, Iterative (1 stack)

**This is bit tricky.Dry run 2-3 trees to understand**
Watch [this](https://www.youtube.com/watch?v=NzIGLLwZBS8) Video.

```cpp
class Solution{
public:
    vector<int> postorderTraversal(TreeNode *root){
        vector<int> postorder;
        stack<TreeNode *> st;
        TreeNode *curr = root,*temp;

        while(curr!=NULL || !st.empty()){
            if(curr!=NULL){
                st.push(curr);
                curr = curr->left;
            }
            else{
                temp = st.top()->right;
                if(temp==NULL){
                    temp=st.top();
                    st.pop();
                    postorder.push_back(temp->val);
                    while(!st.empty()&&temp==st.top()->right){
                        temp = st.top();
                        st.pop();
                        postorder.push_back(temp->val);
                    }
                }else{
                    curr = temp;
                }
            }
        }

        return postorder;
    }
};
```

### O(N) Time and O(1) Space, Morris traversal

```cpp
class Solution {
public:
    vector<int> postorderTraversal(TreeNode* root) {
        vector<int> nodes;
        TreeNode* dummy = new TreeNode(0);
        dummy -> left = root;
        TreeNode* cur = dummy;
        while (cur) {
            if (cur -> left) {
                TreeNode* pre = cur -> left;
                while (pre -> right && (pre -> right != cur)) {
                    pre = pre -> right;
                }
                if (!(pre -> right)) {
                    pre -> right = cur;
                    cur = cur -> left;
                } else {
                    reverseAddNodes(cur -> left, pre, nodes);
                    pre -> right = NULL;
                    cur = cur -> right;
                }
            } else {
                cur = cur -> right;
            }
        }
        return nodes;
    }
private:
    void reverseNodes(TreeNode* start, TreeNode* end) {
        if (start == end) {
            return;
        }
        TreeNode* x = start;
        TreeNode* y = start -> right;
        TreeNode* z;
        while (x != end) {
            z = y -> right;
            y -> right = x;
            x = y;
            y = z;
        }
    }
    void reverseAddNodes(TreeNode* start, TreeNode* end, vector<int>& nodes) {
        reverseNodes(start, end);
        TreeNode* node = end;
        while (true) {
            nodes.push_back(node -> val);
            if (node == start) {
                break;
            }
            node = node -> right;
        }
        reverseNodes(end, start);
    }
};
```
