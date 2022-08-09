# Maximum Width of Binary Tree

Given the root of a binary tree, return the maximum width of the given tree.

The maximum width of a tree is the maximum width among all levels.

The width of one level is defined as the length between the end-nodes (the leftmost and rightmost non-null nodes), where the null nodes between the end-nodes are also counted into the length calculation.

It is guaranteed that the answer will in the range of 32-bit signed integer.

### BFS

-   [Striver Video](https://www.youtube.com/watch?v=ZbybYvcVLks)

### Code

```cpp
class Solution {
public:
    int widthOfBinaryTree(TreeNode* root)
    {
        if (!root) return 0;

        unsigned int ans = 0;
        queue<pair<TreeNode*, int>> q;
        q.push({ root, 0 });

        // bfs ( level order traversal )
        while (!q.empty()) {
            int size = q.size();
            int min = q.front().second;
            unsigned int first, last;

            for (int i = 0; i < size; i++) {
                unsigned int curr = q.front().second - min;
                TreeNode* node = q.front().first;
                q.pop();

                if (i == 0)
                    first = curr;
                if (i == size - 1)
                    last = curr;

                // pushing left child subtree
                if (node->left)
                    q.push({ node->left, 2 * curr + 1 });

                // pushing right child subtree
                if (node->right)
                    q.push({ node->right, 2 * curr + 2 });
            }

            ans = max(ans, last - first + 1);
        }

        return ans;
    }
};
```

### DFS

-   Int will give integer overflow, so we use unsigned int.

### Code

```cpp
class Solution {
private:
    unsigned int dfs(TreeNode* root, unsigned int level, unsigned int order, vector<unsigned int>& start, vector<unsigned int>& end)
    {
        if (root == NULL) {
            return 0;
        }
        int n = start.size();
        if (n == level) {
            start.push_back(order);
            end.push_back(order);
        } else {
            end[level] = order;
        }
        int curr = end[level] - start[level] + 1;
        int left = dfs(root->left, level + 1, 2 * order, start, end);
        int right = dfs(root->right, level + 1, 2 * order + 1, start, end);
        return max({ curr, left, right });
    }

public:
    int widthOfBinaryTree(TreeNode* root)
    {
        vector<unsigned int> start;
        vector<unsigned int> end;
        return int(dfs(root, 0, 1, start, end));
    }
};
```

### Codestudio

-   codestudio problem is simple, just use level order traversal and store max width of level.
