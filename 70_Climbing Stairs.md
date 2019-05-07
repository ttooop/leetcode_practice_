>https://leetcode.com/problems/climbing-stairs/

**expression**

You are climbing a stair case. It takes n steps to reach to the top.

Each time you can either climb 1 or 2 steps. In how many distinct ways can you climb to the top?

**Note:** Given n will be a positive integer.

**example 1**
Input: 2

Output: 2

Explanation: There are two ways to climb to the top.

1. 1 step + 1 step

2. 2 steps

**example 2**

Input: 3

Output: 3

Explanation: There are three ways to climb to the top.

1. 1 step + 1 step + 1 step

2. 1 step + 2 steps

3. 2 steps + 1 step

**comprehension**

*Fibonacci Number*

In the above approach we have used dpdp array where dp[i]=dp[i-1]+dp[i-2]dp[i]=dp[i−1]+dp[i−2]. It can be easily analysed that dp[i]dp[i] is nothing but i^{th}i 
th fibonacci number.

Fib(n)=Fib(n-1)+Fib(n-2) Fib(n)=Fib(n−1)+Fib(n−2)

Now we just have to find n^{th}nth number of the fibonacci series having 11 and 22 their first and second term respectively, i.e. Fib(1)=1Fib(1)=1 and Fib(2)=2Fib(2)=2.


```
class Solution {
public:
    int climbStairs(int n) {
        if(n==1){
            return 1;
        }
        int first=1;
        int second=2;
        for(int i=3;i<=n;i++){
            int third=first+second;
            first=second;
            second=third;
        }
        return second;
    }
};
```
