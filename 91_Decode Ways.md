>https://leetcode.com/problems/decode-ways/

**EXPRESSION**

A message containing letters from A-Z is being encoded to numbers using the following mapping:

    'A' -> 1
    'B' -> 2
    ...
    'Z' -> 26
Given a non-empty string containing only digits, determine the total number of ways to decode it.

**Example 1:**

    Input: "12"
    Output: 2
    Explanation: It could be decoded as "AB" (1 2) or "L" (12).

**Example 2:**

    Input: "226"
    Output: 3
    Explanation: It could be decoded as "BZ" (2 26), "VF" (22 6), or "BBF" (2 2 6).

**COMPREHENSION**

求解码方法，限制条件：
- 一位数时不能为0
- 两位数不能大于26，其十位数上也不能为0

动态规划求解，建立一位dp数组，长度比输入长度多2，全部初始化为1，对每个数首先判断是否为0，如果是则将改为dp赋值为0 ，如果不是，附赋上一个dp值，此时相当于加上了dp[i-1],然后看数组前一位是否存在，若存在且满足前一位不是0，且和当前为一起组成的两位数不大于26，则当前dp值加上dp[i-2]。

```
class Solution {
public:
    int numDecodings(string s) {
        if(s.empty()||(s.size()>1&&s[0]=='0'))
            return 0;
        vector<int> dp(s.size()+1,0);
        dp[0]=1;
        for(int i=1;i<dp.size();++i){
            dp[i]=(s[i-1]=='0')?0:dp[i-1];
            if(i>1&&(s[i-2]=='1'||(s[i-2]=='2'&&s[i-1]<='6'))){
                dp[i]+=dp[i-2];
            }
        }
        return dp.back();
    }
};
```
