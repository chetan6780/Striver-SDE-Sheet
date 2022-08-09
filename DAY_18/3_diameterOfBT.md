# Diameter of binary tree

### O(N^2) solution

-   diameter for the tree is max({currDiameter,leftDiameter,rightDiameter});
-   currDiameter = max(leftHeight+rightHeight+1);
-   **TC: O(N^2)**

### Code

```cpp
class Solution {
private:
    int height(TreeNode* root)
    {
        if (root == NULL) return 0;
        return 1 + max(height(root->left), height(root->right));
    }
    int diameter(TreeNode* root)
    {
        if (root == NULL) return 0;

        int leftHeight = height(root->left);
        int rightHeight = height(root->right);

        int leftDig = diameter(root->left);
        int rightDig = diameter(root->right);

        return max(1 + leftHeight + rightHeight, max(leftDig, rightDig));
    }

public:
    int diameterOfBinaryTree(TreeNode* root)
    {
        if (root == NULL) return 0;
        return diameter(root)-1;
    }
};
```

### O(N) optimization.

-   modification in height function.

### Code

```cpp
class Solution {
private:
    int height(TreeNode* root, int& ans)
    {
        if (root == NULL) return 0;
        int leftHeight = height(root->left, ans);
        int rightHeight = height(root->right, ans);
        ans = max(ans, leftHeight + rightHeight);
        return max(leftHeight, rightHeight) + 1;
    }

public:
    int diameterOfBinaryTree(TreeNode* root)
    {
        int ans = 0;
        height(root, ans);
        return ans;
    }
};
```
