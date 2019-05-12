>https://leetcode.com/problems/valid-sudoku/

**expression**

Determine if a 9x9 Sudoku board is valid. Only the filled cells need to be validated according to the following rules:

1. Each row must contain the digits 1-9 without repetition.
2. Each column must contain the digits 1-9 without repetition.
3. Each of the 9 3x3 sub-boxes of the grid must contain the digits 1-9 without repetition.

The Sudoku board could be partially filled, where empty cells are filled with the character '.'.

**comprehension**

验证一个方阵是否为数独矩阵。需要三个标志矩阵，分别记录各行各列，各小方阵，是否出现某个数字。行和列的标志下标直接对应，小方阵的下标需要转换

```
class Solution {
public:
    bool isValidSudoku(vector<vector<char>>& board) {
      if (board.empty() || board[0].empty())
		return false;
	int m = board.size(), n = board[0].size();
	vector<vector<bool>> rowflag(m, vector<bool>(n, false));
	vector<vector<bool>> colflag(m, vector<bool>(n, false));
	vector<vector<bool>> cellflag(m, vector<bool>(n, false));
	for (int i = 0; i < m; ++i) {
		for (int j = 0; j < n; ++j) {
			if (board[i][j] >= '1'&&board[i][j] <= '9') {
				int c = board[i][j] - '1';
				if (rowflag[i][c] || colflag[c][j] || cellflag[3 * (i / 3) + j / 3][c])
					return false;
				rowflag[i][c] = true;
				colflag[c][j] = true;
				cellflag[3 * (i / 3) + j / 3][c] = true;
			}
		}
	}
	return true;  
    }
};
```
