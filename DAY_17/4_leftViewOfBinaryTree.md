# Left View of binary tree

### Recursive Solution

-   Simple DFS.
-   if our level is same as result vector's size, then we push the value in the result vector.

### Code

```cpp
void leftView(vector<int>&res, TreeNode<int>* root, int level)
{
    if(root == NULL) return;

    if(level == res.size()) res.push_back(root->data);

    leftView(res, root->left, level + 1);
    leftView(res, root->right, level + 1);
}

vector<int> getLeftView(TreeNode<int>* root)
{
    vector<int> res;
    leftView(res,root,0);
    return res;
}
```

### Iterative Solution

-   We push first element of queue in the result to get right side view.

### Code

```cpp
class Solution {
public:
    vector<int> leftSideView(TreeNode* root)
    {
        vector<int> res;
        if (root == NULL)
            return res;

        queue<TreeNode*> q;
        q.push(root);

        while (!q.empty()) {
            int sz = q.size();
            for (int i = 0; i < sz; i++) {
                TreeNode* node = q.front(); q.pop();

                if (i == 0) res.push_back(node->val);

                if (node->left != NULL) q.push(node->left);
                if (node->right != NULL) q.push(node->right);
            }
        }
        return res;
    }
};

```
