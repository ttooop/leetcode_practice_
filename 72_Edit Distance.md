>https://leetcode.com/problems/edit-distance/

**expression**

Given two words word1 and word2, find the minimum number of operations required to convert word1 to word2.

You have the following 3 operations permitted on a word:

1. Insert a character
2. Delete a character
3. Replace a character

**example 1**

**Input:** word1 = "horse", word2 = "ros"

**Output: **3

**Explanation:**

horse -> rorse (replace 'h' with 'r')

rorse -> rose (remove 'r')

rose -> ros (remove 'e')

**comprehension**

字符串对齐！

动态规划！

```
class Solution {
public:
    int minDistance(string word1, string word2) {
        int m=word1.size(),n=word2.size();
        vector<vector<int>> dp(m+1,vector<int>(n+1));
        for(int i=0;i<=m;++i){
            dp[i][0]=i;
        }
        for(int j=0;j<=n;++j){
            dp[0][j]=j;
        }
        for(int i=1;i<=m;++i){
            for(int j=1;j<=n;++j){
                if(word1[i-1]==word2[j-1]){
                    dp[i][j]=dp[i-1][j-1];
                }
                else{
                    dp[i][j]=min(dp[i-1][j-1],min(dp[i-1][j],dp[i][j-1]))+1;
                }
            }
        }
        return dp[m][n];
    }
};
```
