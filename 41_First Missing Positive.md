>https://leetcode.com/problems/first-missing-positive/

**expression**

Given an unsorted integer array, find the smallest missing positive integer.

**Example 1:**

    Input: [1,2,0]
    Output: 3

**Example 2:**

    Input: [3,4,-1,1]
    Output: 2

**Example 3:**

    Input: [7,8,9,11,12]
    Output: 1
**Note:**

Your algorithm should run in O(n) time and uses constant extra space.

**comprehension**

使用hashset，先找到最大值，然后从1挨个遍历查看是否存在，并记录在哈希集合中，同时记录nums中最大的数，以便后续循环。最后返回第一个缺失的值

```
class Solution {
public:
    int firstMissingPositive(vector<int>& nums) {
        int mx = 0;
	    unordered_set<int> s;
	    for (int num : nums) {
		    if (num <= 0)
		    	continue;
		    s.insert(num);
		    mx = max(mx, num);
	    }
	    for (int i = 1; i <= mx; ++i) {
	    	if (!s.count(i))
	    		return i;
	    }
	    return mx + 1;
    }
};
```
