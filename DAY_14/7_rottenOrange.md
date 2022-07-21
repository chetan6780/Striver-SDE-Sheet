# Rotting Oranges

You are given an m x n grid where each cell can have one of three values:

- 0 representing an empty cell,
- 1 representing a fresh orange, or
- 2 representing a rotten orange.

Every minute, any fresh orange that is 4-directionally adjacent to a rotten orange becomes rotten.

Return the minimum number of minutes that must elapse until no cell has a fresh orange. If this is impossible, return -1.

### BFS solution

- simple application of bfs.
- Watch [striver's short video](https://www.youtube.com/watch?v=pUAPcVlHLKA) for better explanation.
- **Time complexity: O(M\*N)**

### Code

```cpp
class Solution{
public:
    int orangesRotting(vector<vector<int>> &grid){
        if (grid.empty()) return 0;
        int r = grid.size(), c = grid[0].size(), days = 0, oranges = 0, cnt = 0;

        queue<pair<int, int>> rotten;
        for (int i = 0; i < r; i++){
            for (int j = 0; j < c; j++){
                if (grid[i][j] != 0) oranges++;
                if (grid[i][j] == 2) rotten.push({i, j});
            }
        }

        int dirs[5] = {0, 1, 0, -1, 0};

        while (!rotten.empty()){
            int k = rotten.size();
            cnt += k;
            while (k--){
                auto [x, y] = rotten.front();
                rotten.pop();

                for (int i = 0; i < 4; i++){
                    int nr = x + dirs[i], nc = y + dirs[i + 1];
                    if (nr < 0 || nc < 0 || nr >= r || nc >= c || grid[nr][nc] != 1) continue;
                    grid[nr][nc] = 2;
                    rotten.push({nr, nc});
                }
            }
            if (!rotten.empty()) days++;
        }

        return oranges == cnt ? days : -1;
    }
};
```
