# Vertical order traversal

### Solution

-   Similar to top/bottom view of a binary tree, we store horizontal distance of each node in a map.
-   for every horizontal distance we print all the nodes at that horizontal distance.
-   For more explanation see [this video](https://www.youtube.com/watch?v=h7xALnzllec)

### Code

```cpp
class Solution
{
    public:
    //Function to find the vertical order traversal of Binary Tree.
    vector<int> verticalOrder(Node *root)
    {
        vector<int> ans;
        if(root==NULL)
            return ans;
        map<int,vector<int>> mp;
        queue<pair<Node*,int>> q;
        // node, horizontal distance
        q.push({root,0});
        while(!q.empty())
        {
            pair<Node*,int> tp=q.front();
            q.pop();
            mp[tp.second].push_back(tp.first->data);
            if(tp.first->left)
                q.push({tp.first->left,tp.second-1});
            if(tp.first->right)
                q.push({tp.first->right,tp.second+1});
        }
        for(auto it : mp)
        {
            for(auto it1 : it.second)
                ans.push_back(it1);
        }
        return ans;
    }
};
```
