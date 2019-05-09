>https://leetcode.com/problems/single-number/

**expression**

Given a non-empty array of integers, every element appears twice except for one. Find that single one.

**Note:**

Your algorithm should have a linear runtime complexity. Could you implement it without using extra memory?

**Example 1:**

    Input: [2,2,1]
    Output: 1
    
**Example 2:**

    Input: [4,1,2,1,2]
    Output: 4
    
**comprehension**

本题要求找出数组中只出现一次的数，其他数都只出现一次。但是要求，时间复杂度O(n)，并且空间复杂度O(1)，因此，不能用排序方法，也不能用map数据结构。

因此使用位操作来解此题——逻辑异或

```
class Solution {
public:
    int singleNumber(vector<int>& nums) {
        int res = 0;
	    for (auto num : nums) {
		    res ^= num;
	    }
	    return res;
    }
};
```
