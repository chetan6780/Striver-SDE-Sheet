# Root to node path

### Solution

-   We use recursion to solve this problem.
-   For every node we visit store it in the path.
-   if node is null return false.
-   if any one of the child returns true then return true.
-   else pop last element and return false.
-   [Striver Video](https://www.youtube.com/watch?v=fmflMqVOC7k)

### Code

```cpp
bool getPath(vector<int>& res, TreeNode<int>* root, int x)
{
    if (!root)
        return false;
    res.push_back(root->data);
    if (root->data == x)
        return true;
    if (getPath(res, root->left, x) || getPath(res, root->right, x))
        return true;
    res.pop_back();
    return false;
}

vector<int> pathInATree(TreeNode<int>* root, int x)
{
    vector<int> res;
    if (!root)
        return res;
    getPath(res, root, x);
    return res;
}
```
