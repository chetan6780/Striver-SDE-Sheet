# Preorder inorder postorder in a single traversal

### Code

```cpp
vector<vector<int>> getTreeTraversal(BinaryTreeNode<int>* root)
{
    vector<vector<int>> result(3, vector<int>());
    if (root == NULL)
        return result;

    stack<pair<BinaryTreeNode<int>*, int>> st;
    st.push({ root, 0 });

    while (!st.empty()) {
        auto x = st.top();
        st.pop();

        if (x.second == 0) {
            result[1].push_back({ x.first->data });
            x.second++;
            st.push(x);
            if (x.first->left != NULL) {
                st.push({ x.first->left, 0 });
            }
        } else if (x.second == 1) {
            result[0].push_back({ x.first->data });
            x.second++;
            st.push(x);
            if (x.first->right != NULL) {
                st.push({ x.first->right, 0 });
            }
        } else {
            result[2].push_back({ x.first->data });
        }
    }
}
```
