>https://leetcode.com/problems/powx-n/

**expression**

Implement pow(x, n), which calculates x raised to the power n (xn).

**Example 1:**

    Input: 2.00000, 10
    Output: 1024.00000

**Example 2:**

    Input: 2.10000, 3
    Output: 9.26100

**Example 3:**

    Input: 2.00000, -2
    Output: 0.25000
    Explanation: 2-2 = 1/22 = 1/4 = 0.25

**Note:**

-100.0 < x < 100.0
n is a 32-bit signed integer, within the range [−231, 231 − 1]

**comprehension**

快速幂算法：：：时间复杂度为O(logN)：：：i初始化为n，若i为奇数，则res乘x，若为偶数，x自己乘自己，循环至0为止。

```
class Solution {
public:
    double myPow(double x, int n) {
        double res=1.0;
        for(int i=n;i!=0;i/=2){
            if(i%2!=0)
                res*=x;
            x*=x;
        }
        return n<0?1/res:res;
    }
};
```
