>https://leetcode.com/problems/majority-element/

**expression**

Given an array of size n, find the majority element. The majority element is the element that appears more than ⌊ n/2 ⌋ times.

You may assume that the array is non-empty and the majority element always exist in the array.

**Example 1:**

    Input: [3,2,3]
    Output: 3
    Example 2:

**Example 2:**

    Input: [2,2,1,1,1,2,2]
    Output: 2
    
**comprehension**

摩尔投票法**Moore Voting**，需要O(n)的时间和O(1)的空间。这种投票法的算法思想：

前提：：数组中一定有过半数的存在才可以使用。先将第一个数字假设为过半数，然后把计数器设为1，比较下一个数和此数是否相等，若相等则计数器加一，若不等则减一。然后看此时计数器的值，若为零，则将下一个值设为候选过半数，，以此类推直到遍历整个数组，当前候选过半数为该数组的过半数。

先假设候选者，然后再进行验证的算法。我们现将数组中的第一个数假设为过半数，然后进行统计其出现的次数，如果遇到同样的数，则计数器自增1，否则计数器自减1，如果计数器减到了0，则更换下一个数字为候选者。
这是一个很巧妙的设定，也是本算法的精髓所在，为啥遇到不同的要计数器减1呢，为啥减到0了又要更换候选者呢？首先是有那个强大的前提存在，一定会有一个出现超过半数的数字存在，那么如果计数器减到0了话，说明目前不是候选者数字的个数已经跟候选者的出现个数相同了，那么这个候选者已经很weak，不一定能出现超过半数，我们选择更换当前的候选者。那有可能你会有疑问，那万一后面又大量的出现了之前的候选者怎么办，不需要担心，如果之前的候选者在后面大量出现的话，其又会重新变为候选者，直到最终验证成为正确的过半数。

```
class Solution {
public:
    int majorityElement(vector<int>& nums) {
        int res=0,cnt=0;
        for(int num:nums){
            if(cnt==0){
                res=num;
                cnt++;
            }
            else
                (num==res)?++cnt:--cnt;
        }
        return res;
    }
};
```
