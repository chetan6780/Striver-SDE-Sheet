# Is Height Balanced Binary Tree

### O(N^2) solution

-   calculate left and right height of node.
-   If their difference is greater than 1, return false.
-   if left or right subtree is not balanced, return false.else return true.

```cpp
int heightOfBT(BinaryTreeNode<int>* root){
    if(root == NULL) return 0;
    return max(heightOfBT(root->left), heightOfBT(root->right)) + 1;
}
bool isBalancedBT(BinaryTreeNode<int>* root) {
    if(root == NULL) return true;

    int leftHeight = heightOfBT(root->left);
    int rightHeight = heightOfBT(root->right);

    if(abs(leftHeight - rightHeight) > 1) return false;

    return isBalancedBT(root->left) && isBalancedBT(root->right);
}
```

### O(N) optimization

-   Modification of height of binary tree

```cpp
int heightOfBt(BinaryTreeNode<int>* root)
{
    if (!root) return 0;

    int lh = heightOfBt(root->left);
    if (lh == -1) return -1;

    int rh = heightOfBt(root->right);
    if (rh == -1) return -1;

    if (abs(lh - rh) > 1) return -1;

    return 1 + max(lh, rh);
}

bool isBalancedBT(BinaryTreeNode<int>* root)
{
    if (!root) return true;
    return heightOfBt(root) != -1;
}
```
