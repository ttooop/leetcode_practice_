>https://leetcode.com/problems/minimum-path-sum/

**expression:**

Given a m x n grid filled with non-negative numbers, find a path from top left to bottom right which minimizes the sum of all numbers along its path.

**Note:** You can only move either down or right at any point in time.

**example**

Input:
[
  [1,3,1],
  [1,5,1],
  [4,2,1]
]

Output: 7

Explanation: Because the path 1→3→1→1→1 minimizes the sum

**comprehension**

求最小路径和：使用动态规划来做，维护一个二维dp数组，其中dp[i][j]表示当前位置的最小路径和，
递推式为：dp[i][j]=grid[i][j]+min(dp[i-1][j],dp[i][j])

```
class Solution {
public:
    int minPathSum(vector<vector<int>>& grid) {
        int m=grid.size(),n=grid[0].size();
        int dp[m][n];
        dp[0][0] = grid[0][0];
	for (int i = 1; i < m; i++)
		dp[i][0] = grid[i][0] + dp[i - 1][0];
	for (int i = 1; i < n; i++)
		dp[0][i] = grid[0][i] + dp[0][i - 1];
	for (int i = 1; i < m; ++i) {
		for (int j = 1; j < n; ++j) {
			dp[i][j] = grid[i][j] + min(dp[i - 1][j], dp[i][j - 1]);
		}
	}
	return dp[m - 1][n - 1];
    }
};
```
