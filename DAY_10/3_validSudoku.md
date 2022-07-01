# Valid Sudoku

Determine if a 9 x 9 Sudoku board is valid. Only the filled cells need to be validated according to the following rules:

1. Each row must contain the digits 1-9 without repetition.
2. Each column must contain the digits 1-9 without repetition.
3. Each of the nine 3 x 3 sub-boxes of the grid must contain the digits 1-9 without repetition.

**_Note:_**

-   A Sudoku board (partially filled) could be valid but is not necessarily solvable.
-   Only the filled cells need to be validated according to the mentioned rules.

### Implementation

### Code

```cpp
class Solution{
public:
    bool isValidSudoku(vector<vector<char>> &board){
        vector<set<int>> rows(9), cols(9), blocks(9);

        for (int i = 0; i < 9; i++){
            for (int j = 0; j < 9; j++){
                if (board[i][j] != '.'){
                    int curr = board[i][j] - '0'; // get the current number on board
                    // Check if the number is already in the row, column or block
                    if (rows[i].count(curr) || cols[j].count(curr) || blocks[(i / 3) * 3 + j / 3].count(curr))
                        return false;

                    // Insert the number into the corresponding row, column and block
                    rows[i].insert(curr);
                    cols[j].insert(curr);
                    blocks[(i / 3) * 3 + j / 3].insert(curr);
                }
            }
        }
        return true;
    }
};
```

---

**_Q. `(i/3)*3+j/3` , how did you count this , means how did you think of this no , how it came in your mind ??_**

The problem is to come up with an equation to map (n\*n) coordinates to (n) numbers so we can use it as an index into the blocks array.

Our board would look like this:

```
(0,0) (0,1) (0,2) (0,3) (0,4) (0,5) (0,6) (0,7) (0,8)
(1,0) (1,1) (1,2) (1,3) (1,4) (1,5) (1,6) (1,7) (1,8)
(2,0) (2,1) (2,2) (2,3) (2,4) (2,5) (2,6) (2,7) (2,8)
(3,0) (3,1) (3,2) (3,3) (3,4) (3,5) (3,6) (3,7) (3,8)
(4,0) (4,1) (4,2) (4,3) (4,4) (4,5) (4,6) (4,7) (4,8)
(5,0) (5,1) (5,2) (5,3) (5,4) (5,5) (5,6) (5,7) (5,8)
(6,0) (6,1) (6,2) (6,3) (6,4) (6,5) (6,6) (6,7) (6,8)
(7,0) (7,1) (7,2) (7,3) (7,4) (7,5) (7,6) (7,7) (7,8)
(8,0) (8,1) (8,2) (8,3) (8,4) (8,5) (8,6) (8,7) (8,8)
```

Let's divide this into 3x3 boxes, and label the boxes like this:

```
0 1 2
3 4 5
6 7 8
```

Thus

```
(0,0) (0,1) (0, 2)
(1,0) (1,1) (1, 2)
(2,0) (2,1) (2, 2)
```

will map to box 0.

And

```
(0,3) (0,4) (0,5)
(1,3) (1,4) (1,5)
(2,3) (2,4) (2,5)
```

will map to box 1.

And so on.

We can see that for any coordinate (r, c), the column index (c), which ranges from 0-8 should contribute either (0, 1, or 2) to the boxIndex. So we can write this as c/3.
This is because of integer division:

```
{0, 1, 2} / 3 = 0
{3, 4, 5} / 3 = 1
{6, 7, 8} / 3 = 2
```

Also, for any coordinate (r, c), if the column already contributes (0, 1, or 2) to the boxIndex (which has a maximum of 8), then the row index (r) needs to contribute either (0, 3, or 6) to the boxIndex, since this gives all possible numbers from 0 - 8.

```
e.g.
0 + {0, 1, 2} = {0, 1, 2}
3 + {0, 1, 2} = {3, 4, 5}
6 + {0, 1, 2} = {6, 7, 8}
```

Well how do we map {0,1,2,3,4,5,6,7,8} to {0,3,6} ?
We can use integer division again, but multiply the result by 3

```
({0, 1, 2} / 3) * 3 = (0) * 3 = 0
({3, 4, 5} / 3) * 3 = (1) * 3 = 3
({6, 7, 8} / 3) * 3 = (2) * 3 = 6
```

So we have `boxIndex = c/3 + r/3*3`

### Codestudio

```cpp
bool isValid(int matrix[9][9], int row, int col, int n)
{
    for (int c = 0; c < 9; c++) {
        if (matrix[row][c] == n)
            return false;
    }

    for (int r = 0; r < 9; r++) {
        if (matrix[r][col] == n)
            return false;
    }

    int x = 3 * (row / 3);
    int y = 3 * (col / 3);
    for (int r = x; r < x + 3; r++) {
        for (int c = y; c < y + 3; c++) {
            if (matrix[r][c] == n)
                return false;
        }
    }

    return true;
}
bool solver(int matrix[9][9], int row, int col)
{
    if (col == 9) {
        row++;
        col = 0;
    }

    if (row == 9)
        return true;

    bool flag = false;
    if (matrix[row][col] == 0) {
        for (int n = 1; n <= 9; n++) {
            if (isValid(matrix, row, col, n)) {
                matrix[row][col] = n;
                flag = flag || solver(matrix, row, col + 1);
                matrix[row][col] = 0;
            }
        }
    } else
        flag = flag || solver(matrix, row, col + 1);

    return flag;
}

bool isItSudoku(int matrix[9][9])
{
    return solver(matrix, 0, 0);
}
```
