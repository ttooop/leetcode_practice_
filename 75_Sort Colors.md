>https://leetcode.com/problems/sort-colors/

**expression**

Given an array with n objects colored red, white or blue, sort them in-place so that objects of the same color are adjacent, with the colors in the order red, white and blue.

Here, we will use the integers 0, 1, and 2 to represent the color red, white, and blue respectively.

**Note:** You are not suppose to use the library's sort function for this problem.

**example**

Input: [2,0,2,1,1,0]

Output: [0,0,1,1,2,2]

**Follow up:**

A rather straight forward solution is a two-pass algorithm using counting sort.
First, iterate the array counting number of 0's, 1's, and 2's, then overwrite array with total number of 0's, then 1's and followed by 2's.
Could you come up with a one-pass algorithm using only constant space?

**comprehension**

排序题

**方法一**

遍历两边数组的方法：记录每种颜色的个数，更新数组

```
class Solution {
public:
    void sortColors(vector<int>& nums) {
        vector<int> colors(3);
	//数组colors三个下标0，1，2，分别存的是三种颜色的个数
	for (int num : nums) {
		++colors[num];
	}
	//存入个数
	for (int i = 0, cur = 0; i < 3; ++i) {
		for (int j = 0; j < colors[i]; ++j) {
			nums[cur++] = i;
			//cur是更新后指向的位置
		}
	}
    }
};
```

**方法二**

只遍历一次数组来求解，需要用到双指针来做，分别从原数组的首尾向中心移动

- 定义red指针指向开头位置，blue指针指向末尾位置

- 从头开始遍历原数组，如果遇到0，则交换该值和red指针指向的值，并将red指针后移一位。如果遇到2，则交换该值和blue指针指向的值，并将blue指针前移以为，如果遇到1，则继续遍历

```
class Solution {
public:
    void sortColors(vector<int>& nums) {
        int red = 0, blue = (int)nums.size() - 1;
	for (int i = 0; i <= blue ; ++i) {
		if (nums[i] == 0) {
			swap(nums[i], nums[red++]);
		}
		else if (nums[i] == 2) {
			swap(nums[i--], nums[blue--]);
		}
	}
    }
};
```
