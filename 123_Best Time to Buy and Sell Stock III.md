>https://leetcode.com/problems/best-time-to-buy-and-sell-stock-iii/

**EXPRESSION**

Say you have an array for which the ith element is the price of a given stock on day i.

Design an algorithm to find the maximum profit. You may complete at most two transactions.

Note: You may not engage in multiple transactions at the same time (i.e., you must sell the stock before you buy again).

**Example 1:**

    Input: [3,3,5,0,0,3,1,4]
    Output: 6
    Explanation: Buy on day 4 (price = 0) and sell on day 6 (price = 3), profit = 3-0 = 3.
                 Then buy on day 7 (price = 1) and sell on day 8 (price = 4), profit = 4-1 = 3.

**Example 2:**

    Input: [1,2,3,4,5]
    Output: 4
    Explanation: Buy on day 1 (price = 1) and sell on day 5 (price = 5), profit = 5-1 = 4.
                 Note that you cannot buy on day 1, buy on day 2 and sell them later, as you are
                 engaging multiple transactions at the same time. You must sell before buying again.

**Example 3:**

    Input: [7,6,4,3,1]
    Output: 0
    Explanation: In this case, no transaction is done, i.e. max profit = 0.

**COMPREHENSION**

122. Best Time to Buy and Sell Stock II  之前的题比较简单，给定股票序列，要求可以做多次的购入和卖出操作（但是要求必须买一次再卖出去才能再购买），找到最大利润。代码如下：

```
class Solution {
public:
    int maxProfit(vector<int>& prices) {
        if(prices.empty())
            return 0;
        int res=0;
        for(int i=0;i<prices.size()-1;++i){
            if(prices[i]<prices[i+1]){
                res+=prices[i+1]-prices[i];
            }
        }
        return res;
    }
};
```
但是再该题中，限制购入和卖出的次数最多为两次，找到最大利润。用动态规划来解，需要两个递推公式分别更新变量local和global。我们可以求至少k次交易的最大利润，找到通解后可以设定k=2，即为本体的解答。我们定义local[i][j]为在到达第i天时最多可以进行j次交易并且最后一次交易在最好一天卖出的最大利润，此为局部最优。然后我们定义global[i][j]为在到达第i天时最多可进行j次交易的最大利润，此为全局最优。

递推公式：local[i][j]=max(global[i-1][j-1]+max(diff,0),local[i-1][j]+diff)

global[i][j]=max(local[i][j],global[i-1][j])

```
class Solution {
public:
    int maxProfit(vector<int>& prices) {
        if(prices.empty())
            return 0;
        int n=prices.size(),g[n][3]={0},l[n][3]={0};
        for(int i=1;i<prices.size();++i){
            int diff=prices[i]-prices[i-1];
            for(int j=1;j<=2;++j){
                l[i][j]=max(g[i-1][j-1]+max(diff,0),l[i-1][j]+diff);
                g[i][j]=max(l[i][j],g[i-1][j]);
            }
        }
        return g[n-1][2];
    }
};
```


