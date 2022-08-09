# Lowest Common Ancestor of a Binary Tree

### O(N) Time and O(N) Space

-   Find the path from the root node to node n1 and store it in a vector or array.
-   Find the path from the root node to node n2 and store it in another vector or array.
-   Traverse both paths until the values in arrays are same. Return the common element just before the mismatch.

### O(N) Time recursive solution

-   we traverse the tree and find p and q;
-   if one of child node is null return another
-   else both are not null return the root(curr node), that means left and right are p and q.

```cpp
class Solution {
public:
    TreeNode* lowestCommonAncestor(TreeNode* root, TreeNode* p, TreeNode* q) {
        if(root == NULL) return NULL;
        if(root==p || root==q) return root;

        TreeNode* left = lowestCommonAncestor(root->left,p,q);
        TreeNode* right = lowestCommonAncestor(root->right,p,q);

        if(left == NULL) return right;
        else if(right == NULL) return left;
        else return root; // both are not null
    }
};
```
