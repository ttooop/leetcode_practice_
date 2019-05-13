>https://leetcode.com/problems/sqrtx/

**expression**

Implement int sqrt(int x).

Compute and return the square root of x, where x is guaranteed to be a non-negative integer.

Since the return type is an integer, the decimal digits are truncated and only the integer part of the result is returned.

**Example 1:**

    Input: 4
    Output: 2

**Example 2:**

    Input: 8
    Output: 2
    Explanation: The square root of 8 is 2.82842..., and since 
               the decimal part is truncated, 2 is returned.

**comprehension**

牛顿迭代法——用逼近法求方程根。

f(x)=x^2-n

xi+1=xi - (xi2 - n) / (2xi) = xi - xi / 2 + n / (2xi) = xi / 2 + n / 2xi = (xi + n/xi) / 2

```
class Solution {
public:
    int mySqrt(int x) {
        long res=x;
        while(res*res>x){
            res=(res+x/res)/2;
        }
        return res;
    }
};
```
