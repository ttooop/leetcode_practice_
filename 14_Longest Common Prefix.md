>https://leetcode.com/problems/longest-common-prefix/

**expression**

Write a function to find the longest common prefix string amongst an array of strings.

If there is no common prefix, return an empty string "".

**Example 1:**

    Input: ["flower","flow","flight"]
    Output: "fl"

**Example 2:**

    Input: ["dog","racecar","car"]
    Output: ""
    Explanation: There is no common prefix among the input strings.

**Note:**

All given inputs are in lowercase letters a-z.

**comprehension**

当前某个字符和第一个字符串对应位置的字符不相等，说明不会再有更长的共同前缀了，我们直接通过用substr的方法直接取出共同前缀的子字符串。如果遍历结束前没有返回结果的话，说明第一个单词就是公共前缀，返回为结果即可。

```
class Solution {
public:
    string longestCommonPrefix(vector<string>& strs) {
        if(strs.empty())
            return "";
        for(int j=0;j<strs[0].size();++j){
            for(int i=0;i<strs.size();++i){
                if(j>=strs[i].size()||strs[i][j]!=strs[0][j])
                    return strs[i].substr(0,j);
            }
        }
        return strs[0];
    }
};
```
