# Max Path Sum

### Solution

-   Modification of width of binary tree problem.
-   [Strive Video](https://youtu.be/WszrfSwMz58)

### code

```cpp
#include <bits/stdc++.h>
#define ll long long
int maxPath(TreeNode<int>* node, ll &mx)
{
    if (node == NULL) return 0;
    ll left = max(0, maxPath(node->left, mx));
    ll right = max(0, maxPath(node->right, mx));
    mx = max(mx, left + right + node->val);
    return max(left, right) + node->val;
}

long long int findMaxSumPath(TreeNode<int>* root)
{
    if(!root) return -1;
    // condition to check for only one leaf node
    if(root->left == NULL || root->right == NULL) return -1;
    ll mx = INT_MIN;
    maxPath(root, mx);
    return mx;
}
```
