# N-Queens

The n-queens puzzle is the problem of placing n queens on an n x n chessboard such that no two queens attack each other.

Given an integer n, return all distinct solutions to the n-queens puzzle. You may return the answer in any order.

Each solution contains a distinct board configuration of the n-queens' placement, where 'Q' and '.' both indicate a queen and an empty space, respectively.

### Brute force backtracking (8ms-AC)

-   **Main Algorithm** - we iterate over each row in the board, i.e. once we reach the last row of the board, we should have explored all the possible solutions. - At each iteration (we are located at certain row), we then further iterate over each column of the board, along the current row. At this second iteration, we then can explore the possibility of placing a queen on a particular cell. - Before, we place a queen on the cell with index of `(row, col)`, we need to check if this cell is under the attacking zone of the queens that have been placed on the board before. We can do it with `isSafe()` function. - Once the check passes, we then can proceed to place a queen. Along with the placement, one should also mark out the attacking zone of this newly-placed queen. We achieve this with `placeQueen()` function. - As an important behavior of backtracking, we should be able to abandon our previous decision at the moment we decide to move on to the next candidate. We achieve this with `removeQueen()` function.

-   **The time complexity of `nQueens` problem is dependent of how we implement `isSafe()` function.**

-   **`isSafe()` function**:
    -   We can check if the queen is placed in current row, current column, or the positive diagonal or negative diagonal.
    -   BUT, we don't need to do some redundant checks. like chekiang for the same row, lower column, lower positive and negative diagonal as we haven't traverse them yet.
    -   We just check upper positive and negative diagonal as well as upper column.
    -   We can do it by simple simulation.

### Code

```cpp
class Solution {
private:
    bool isSafe(vector<string>& board, int row, int col)
    {
        int i = row, j = col;
        int n = board.size();
        while (i >= 0 && j >= 0) { // check upper left diagonal
            if (board[i][j] == 'Q')
                return false;
            i--;
            j--;
        }
        i = row;
        j = col;
        while (i >= 0 && j < n) { // check upper right diagonal
            if (board[i][j] == 'Q')
                return false;
            i--;
            j++;
        }
        for (i = 0; i < n; i++) { // check column
            if (board[i][col] == 'Q')
                return false;
        }
        return true;
    }

    void placeQueen(vector<string>& board, int row, int col)
    {
        board[row][col] = 'Q';
    }

    void removeQueen(vector<string>& board, int row, int col)
    {
        board[row][col] = '.';
    }

    void backtrackNQueen(vector<vector<string>>& res, vector<string>& board, int row)
    {
        int n = board.size();
        if (row == n) { // row index is out of bounds, we found the solution
            res.push_back(board);
            return;
        }

        for (int col = 0; col < n; col++) { // traverse every column
            if (isSafe(board, row, col)) {
                placeQueen(board, row, col); // DO
                backtrackNQueen(res, board, row + 1); // RECUR
                removeQueen(board, row, col); // UNDO
            }
        }
    }

public:
    vector<vector<string>> solveNQueens(int n)
    {
        vector<vector<string>> res;
        vector<string> board(n, string(n, '.'));
        backtrackNQueen(res, board, 0);
        return res;
    }
};
```

### 3 vectors optimized backtracking (3ms-AC)

-   All the algorithm is same but we can optimize the `isSafe()` function by using extra space.

-   **`isSafe()` function**:
    -   We can have the `colSet` vector to store the column index of the queens that are placed on the board.
    -   also we can have `posDig` and `negDig` vectors to store the positive and negative diagonal indices of the queens that are placed on the board.
    -   We can get the **positive diagonal index** with **`col + row`**
    -   We can get the **negative diagonal index** with **`col - row + n - 1`**

### Code

```cpp
class Solution {
private:
    bool isSafe(vector<string>& board, vector<int>& colSet, vector<int>& posDig, vector<int>& negDig, int row, int col)
    {
        int n = board.size();
        if (colSet[col] || posDig[col + row] || negDig[col - row + n - 1])
            return false;
        return true;
    }

    void placeQueen(vector<string>& board, vector<int>& colSet, vector<int>& posDig, vector<int>& negDig, int row, int col)
    {
        int n = board.size();
        board[row][col] = 'Q';
        colSet[col] = 1;
        posDig[col + row] = 1;
        negDig[col - row + n - 1] = 1;
    }

    void removeQueen(vector<string>& board, vector<int>& colSet, vector<int>& posDig, vector<int>& negDig, int row, int col)
    {
        int n = board.size();
        board[row][col] = '.';
        colSet[col] = 0;
        posDig[col + row] = 0;
        negDig[col - row + n - 1] = 0;
    }

    void backtrackNQueen(vector<vector<string>>& res, vector<string>& board, vector<int>& colSet, vector<int>& posDig, vector<int>& negDig, int row)
    {
        int n = board.size();
        if (row == n) { // row index is out of bounds, we found the solution
            res.push_back(board);
            return;
        }

        for (int col = 0; col < n; col++) { // traverse every column
            if (isSafe(board, colSet, posDig, negDig, row, col)) {
                placeQueen(board, colSet, posDig, negDig, row, col); // DO
                backtrackNQueen(res, board, colSet, posDig, negDig, row + 1); // RECUR
                removeQueen(board, colSet, posDig, negDig, row, col); // UNDO
            }
        }
    }

public:
    vector<vector<string>> solveNQueens(int n)
    {
        vector<vector<string>> res; // final result
        vector<string> board(n, string(n, '.')); // chess board with "...." strings

        vector<int> colSet(n, 0); // column vector to store column indexes
        vector<int> posDig(2 * n - 1, 0); // positive diagonal vector to store (col+row) indexes
        vector<int> negDig(2 * n - 1, 0); // negative diagonal vector to store (col-row+n-1) indexes

        backtrackNQueen(res, board, colSet, posDig, negDig, 0);

        return res;
    }
};
```

### 1 vector optimized backtracking (7ms-AC)

-   Again same algorithm but we just used **1 vector** instead of **3 vectors**.

-   **`isSafe()` function**:

    -   **`flag[0] to flag[n - 1]`** to indicate if the column had a queen before.
    -   **`flag[n] to flag[3 * n - 2]`** to indicate if the **45° diagonal** had a queen before.
    -   **`flag[3 * n - 1] to flag[5 * n - 3]`** to indicate if the **135° diagonal** had a queen before.
    -   So we will declare **`flag(5 * n - 3)`** vector to store the information of the board.
    -   We can get the **positive diagonal index** with **`n + col + row`**
    -   We can get the **negative diagonal index** with **`4 * n - 2 + col - row`**

### Code

```cpp
class Solution {
private:
    bool isSafe(vector<int>& flag, int n, int row, int col)
    {
        if (flag[col] == 1 || flag[n + col + row] == 1 || flag[4 * n - 2 + col - row] == 1)
            return false;
        return true;
    }
    void placeQueen(vector<string>& board, vector<int>& flag, int n, int row, int col)
    {
        board[row][col] = 'Q';
        flag[col] = 1;
        flag[n + col + row] = 1;
        flag[4 * n - 2 + col - row] = 1;
    }
    void removeQueen(vector<string>& board, vector<int>& flag, int n, int row, int col)
    {
        board[row][col] = '.';
        flag[col] = 0;
        flag[n + col + row] = 0;
        flag[4 * n - 2 + col - row] = 0;
    }
    void backtrackNQueen(vector<vector<string>>& res, vector<string>& board, vector<int>& flag, int row)
    {
        int n = board.size();
        if (row == n) {
            res.push_back(board);
            return;
        }
        for (int col = 0; col < n; col++) {
            if (isSafe(flag, n, row, col)) {
                placeQueen(board, flag, n, row, col);
                backtrackNQueen(res, board, flag, row + 1);
                removeQueen(board, flag, n, row, col);
            }
        }
    }

public:
    vector<vector<string>> solveNQueens(int n)
    {
        vector<vector<string>> res;
        vector<string> board(n, string(n, '.'));
        vector<int> flag(5 * n - 2, 0);
        backtrackNQueen(res, board, flag, 0);
        return res;
    }
};
```

### Codestudio Solution

```cpp
void nQueenHelper(int i, int n, vector<vector<int>>& board, vector<vector<int>>& ans, vector<int>& col, vector<int>& rDig, vector<int>& ldig)
{
    if (i == n) {
        vector<int> temp;
        for (vector<int> k : board) {
            for (int j = 0; j < k.size(); j++)
                temp.push_back(k[j]);
        }
        ans.push_back(temp);
        return;
    }
    for (int j = 0; j < n; j++) {
        if (col[j] == 0 && rDig[i + j] == 0 && ldig[n - 1 + i - j] == 0) {
            board[i][j] = 1;
            col[j] = rDig[i + j] = ldig[n - 1 + i - j] = 1;
            nQueenHelper(i + 1, n, board, ans, col, rDig, ldig);
            board[i][j] = 0;
            col[j] = rDig[i + j] = ldig[n - 1 + i - j] = 0;
        }
    }
}

vector<vector<int>> solveNQueens(int n)
{
    vector<vector<int>> ans;
    vector<vector<int>> board(n, vector<int>(n, 0));
    vector<int> col(n, 0);
    vector<int> rDig(2 * n - 1, 0);
    vector<int> ldig(2 * n - 1, 0);
    nQueenHelper(0, n, board, ans, col, rDig, ldig);
    return ans;
}
```
