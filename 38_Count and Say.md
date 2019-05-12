>https://leetcode.com/problems/count-and-say/

**expression**

The count-and-say sequence is the sequence of integers with the first five terms as following:

    1.     1
    2.     11
    3.     21
    4.     1211
    5.     111221
1 is read off as "one 1" or 11.

11 is read off as "two 1s" or 21.

21 is read off as "one 2, then one 1" or 1211.

Given an integer n where 1 ≤ n ≤ 30, generate the nth term of the count-and-say sequence.

Note: Each term of the sequence of integers will be represented as a string.

**Example 1:**

    Input: 1
    Output: "1"

**Example 2:**

    Input: 4
    Output: "1211"
    
**comprehension**

表示前一个数的元素和个数，比如第一个数是1，那么第二个数来描述前一个数，一个一也就是11，同样的，第三个数来描述第二个数，也就是两个1，即21，以此类推

```
class Solution {
public:
    string countAndSay(int n) {
        if (n <= 0)
		    return "";
	    string res = "1";
	    while (--n) {
		    string cur = "";
		    for (int i = 0; i < res.size(); ++i) {
			    int cnt = 1;
			    while (i + 1 < res.size() && res[i] == res[i + 1]) {
				    cnt++;
				    i++;
			    }
			    cur += to_string(cnt) + res[i];
		    }
		    res = cur;
	    }
	    return res;
    }
};
```
