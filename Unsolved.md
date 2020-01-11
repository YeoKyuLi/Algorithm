# Difficult Algorithms

1. Valid Sudoku - Medium

   [site](https://leetcode.com/problems/valid-sudoku/)

Determine if a 9x9 Sudoku board is valid. Only the filled cells need to be validated **according to the following rules**:

1. Each row must contain the digits `1-9` without repetition.
2. Each column must contain the digits `1-9` without repetition.
3. Each of the 9 `3x3` sub-boxes of the grid must contain the digits `1-9` without repetition.

![img](https://upload.wikimedia.org/wikipedia/commons/thumb/f/ff/Sudoku-by-L2G-20050714.svg/250px-Sudoku-by-L2G-20050714.svg.png)
A partially filled sudoku which is valid.

The Sudoku board could be partially filled, where empty cells are filled with the character `'.'`.

**Example 1:**

```
Input:
[
  ["5","3",".",".","7",".",".",".","."],
  ["6",".",".","1","9","5",".",".","."],
  [".","9","8",".",".",".",".","6","."],
  ["8",".",".",".","6",".",".",".","3"],
  ["4",".",".","8",".","3",".",".","1"],
  ["7",".",".",".","2",".",".",".","6"],
  [".","6",".",".",".",".","2","8","."],
  [".",".",".","4","1","9",".",".","5"],
  [".",".",".",".","8",".",".","7","9"]
]
Output: true
```

**Example 2:**

```
Input:
[
  ["8","3",".",".","7",".",".",".","."],
  ["6",".",".","1","9","5",".",".","."],
  [".","9","8",".",".",".",".","6","."],
  ["8",".",".",".","6",".",".",".","3"],
  ["4",".",".","8",".","3",".",".","1"],
  ["7",".",".",".","2",".",".",".","6"],
  [".","6",".",".",".",".","2","8","."],
  [".",".",".","4","1","9",".",".","5"],
  [".",".",".",".","8",".",".","7","9"]
]
Output: false
Explanation: Same as Example 1, except with the 5 in the top left corner being 
    modified to 8. Since there are two 8's in the top left 3x3 sub-box, it is invalid.
```

**Note:**

- A Sudoku board (partially filled) could be valid but is not necessarily solvable.

- Only the filled cells need to be validated according to the mentioned rules.

- The given board contain only digits `1-9` and the character `'.'`.

- The given board size is always `9x9`.

- ```c++
  class Solution {
  public:
      bool isValidSudoku(vector<vector<char>>& board) {
          // cout << board[0][0] - '0';
          int row[9][9] = {0}, col[9][9] = {0}, sub[9][9] = {0};
          for(int i = 0 ; i < board.size(); i++)
          {
              for(int j = 0 ; j < board[i].size(); j++)
              {
                  if(board[i][j] != '.')
                  {
                      int num =  board[i][j] - '0' -1;
                      int box = i / 3 * 3 + j / 3;
                      cout << board[i][j] << " " << i << "," << num << " " << j << "," << num << " " << box << "," << num << " " << endl;
                      if(row[i][num] || col[j][num] || sub[box][num])
                          return false;
                      row[i][num] = col[j][num] = sub[box][num] = true;
                  }
              }
              cout << endl;
          }
          
          return true;
      }
  };
  
  
  // class Solution
  // {
  // public:
  //     bool isValidSudoku(vector<vector<char> > &board)
  //     {
  //         int used1[9][9] = {0}, used2[9][9] = {0}, used3[9][9] = {0};
          
  //         for(int i = 0; i < board.size(); ++ i)
  //             for(int j = 0; j < board[i].size(); ++ j)
  //                 if(board[i][j] != '.')
  //                 {
  //                     int num = board[i][j] - '0' - 1, k = i / 3 * 3 + j / 3;
  //                     if(used1[i][num] || used2[j][num] || used3[k][num])
  //                         return false;
  //                     used1[i][num] = used2[j][num] = used3[k][num] = 1;
  //                 }
          
  //         return true;
  //     }
  // };
  
  ```

  