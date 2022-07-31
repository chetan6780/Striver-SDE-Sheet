# Top View of binary tree

### Solution

-   Simple level order traversal with horizontal distance(distance of node from root).
-   left child have horizontal distance - 1 and right child have horizontal distance + 1.
-   We use map to store which node is at what distance from its root.
-   For each distance we only store first node at that distance.
-   Finally we print the values present for each distance in map.

### Code

```cpp
class Solution {
public:
    vector<int> topView(Node* root)
    {
        vector<int> res;
        if (!root) return res;

        queue<pair<Node*, int>> q;
        map<int, int> mp;
        q.push({ root, 0 });

        while (!q.empty()) {
            auto tp = q.front();
            q.pop();

            Node* node = tp.first;
            int horrDist = tp.second;

            if (mp.count(horrDist) == 0)
                mp[horrDist] = node->data;

            if (node->left) q.push({ node->left, horrDist - 1 });
            if (node->right) q.push({ node->right, horrDist + 1 });
        }

        for (auto x : mp) {
            res.push_back(x.second);
        }

        return res;
    }
};
```
