# Construct Binary Tree from Inorder and Preorder

### Solution

-   [Striver Video](https://youtu.be/aZNaLrVebKQ)

### Solution

```cpp

class Solution {
    TreeNode* buildTreeHelp(vector<int>& preorder, int preStart, int preEnd, vector<int>& inorder, int inStart, int inEnd, map<int, int>& inorderMap)
    {
        if (preStart > preEnd || inStart > inEnd) {
            return NULL;
        }
        TreeNode* root = new TreeNode(preorder[preStart]);

        int inorderIndex = inorderMap[preorder[preStart]];
        int leftSize = inorderIndex - inStart;

        root->left = buildTreeHelp(preorder, preStart + 1, preStart + leftSize, inorder, inStart, inorderIndex - 1, inorderMap);
        root->right = buildTreeHelp(preorder, preStart + leftSize + 1, preEnd, inorder, inorderIndex + 1, inEnd, inorderMap);

        return root;
    }

public:
    TreeNode* buildTree(vector<int>& preorder, vector<int>& inorder)
    {
        map<int, int> inMap;
        for (int i = 0; i < inorder.size(); i++) {
            inMap[inorder[i]] = i;
        }
        int preStart = 0, preEnd = preorder.size() - 1;
        int inStart = 0, inEnd = inorder.size() - 1;
        TreeNode* root = buildTreeHelp(preorder, preStart, preEnd, inorder, inStart, inEnd, inMap);
        return root;
    }
};
```
