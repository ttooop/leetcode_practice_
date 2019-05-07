>https://leetcode.com/problems/subsets/

**expression**

Given a set of **distinct** integers, *nums*, return all possible subsets (the power set).

**Note:** The solution set must not contain duplicate subsets.

**Example:**

**Input:** nums = [1,2,3]

**Output:**

[

  [3],
  
  [1],
  
  [2],
  
  [1,2,3],
  
  [1,3],
  
  [2,3],
  
  [1,2],
  
  []
  
]

**comprehension**

求子集合的问题：

非递归解法：要求子集合中数字是非降序排列的，所以先进行预处理：先给输入数组排序

一位一位的往上叠加，比如对于题目中给的例子[1,2,3]来说，最开始是空集，那么我们现在要处理1，就在空集上加1，为[1]，现在我们有两个自己[]和[1]，下面我们来处理2，我们在之前的子集基础上，每个都加个2，可以分别得到[2]，[1, 2]，那么现在所有的子集合为[], [1], [2], [1, 2]，同理处理3的情况可得[3], [1, 3], [2, 3], [1, 2, 3], 再加上之前的子集就是所有的子集合了

```
class Solution {
public:
    vector<vector<int>> subsets(vector<int>& nums) {
        vector<vector<int>> res(1);
	sort(nums.begin(), nums.end());
	for (int i = 0; i < nums.size(); ++i) {
		int size = res.size();
		for (int j = 0; j < size; ++j) {
			res.push_back(res[j]);
			res.back().push_back(nums[i]);
		}
	}
	return res;
    }
};
```
