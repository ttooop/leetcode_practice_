>https://leetcode.com/problems/wildcard-matching/

**expression**

Given an input string (s) and a pattern (p), implement wildcard pattern matching with support for '?' and '*'.

'?' Matches any single character.
'*' Matches any sequence of characters (including the empty sequence).
The matching should cover the entire input string (not partial).

**Note:**

s could be empty and contains only lowercase letters a-z.
p could be empty and contains only lowercase letters a-z, and characters like ? or *.

**Example 1:**

    Input:
    s = "aa"
    p = "a"
    Output: false
    Explanation: "a" does not match the entire string "aa".

**Example 2:**

    Input:
    s = "aa"
    p = "*"
    Output: true
    Explanation: '*' matches any sequence.

**Example 3:**

    Input:
    s = "cb"
    p = "?a"
    Output: false
    Explanation: '?' matches 'c', but the second letter is 'a', which does not match 'b'.

**Example 4:**

    Input:
    s = "adceb"
    p = "*a*b"
    Output: true
    Explanation: The first '*' matches the empty sequence, while the second '*' matches the substring "dce".

**Example 5:**

    Input:
    s = "acdcb"
    p = "a*c?b"
    Output: false
    
**comprehension**

字符串匹配，'?'可以匹配一个单个字符，'\*'可以匹配0个或任意个字符。该题重点在于'\*'的匹配问题，设变量jstar记录'\*'在p串中的位置，设istar记录'\*'用于匹配到s串中的位置，这两个变量都初始化为-1，开始设p串中没有星号。

循环i小于s的长度
- 若当前两个字符相等或者p中字符是'?'，则i++,j++
- 否则若p当前字符串是'\*'，则记录jstar=j,j++,istar=i;
- 否则若istar大于等于0，i=++istar,j=jstar+1
- 否则返回false

匹配完s的所有字符，还要检查p串，此时没匹配完的p串里只能剩下星号，不能有其他的字符，将连续的星号过滤掉，如果j不等于p的长度则返回false。

```
class Solution {
public:
    bool isMatch(string s, string p) {
        int i = 0, j = 0, jstar = -1, istar = -1;
	    while (i < s.size()) {
		    if (s[i] == p[j] || p[j] == '?') {
			    ++i; ++j;
		    }
		    else if (p[j] == '*') {
		    	istar = i;
		    	jstar = j++;
		    }
		    else if (istar >= 0) {
		    	i = ++istar;
		    	j = jstar + 1;
		    }
		    else
		    	return false;
	    }   
	    while (j < p.size() && p[j] == '*')
	    	++j;
	    return j == p.size();
    }
};
```
