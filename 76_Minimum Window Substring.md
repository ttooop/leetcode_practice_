>https://leetcode.com/problems/minimum-window-substring/

**expression**

Given a string S and a string T, find the minimum window in S which will contain all the characters in T in complexity O(n).

**Example:**

    Input: S = "ADOBECODEBANC", T = "ABC"
    Output: "BANC"
**Note:**

If there is no such window in S that covers all characters in T, return the empty string "".
If there is such window, you are guaranteed that there will always be only one unique minimum window in S.

**comprehension**

给定原字符串s和字符串t，求s的含有t中所有字符的最小子串。

使用hashmap：：因为不仅要看t中含有哪个字母，还需要统计t中字母的个数，cnt计数器，当cnt和t串字母个数相等时，说明当前窗口已经包含t串中所有字母。minlen记录出现过包含t串所有字母的最短子串的长度，res存的是该最短子串

- 首先遍历一遍t串，将对应字母和出现次数存到hashmap中
- 然后遍历s，把遍历到的字母在对应的hashmap中将其value减一，若减1后仍大于等于0，cnt自增1
- 如果cnt等于t串长度时，开始循环，记录一个子串并更新最小子串的值，然后将子窗口的左边界右移，如果某个移除掉的字母是t串中不可缺少的字母，那么cnt自减1

```
class Solution {
public:
    string minWindow(string s, string t) {
        string res="";
        unordered_map<char,int> lettercnt;
        int left=0,cnt=0,minlen=INT_MAX;
        for(char c:t)
            ++lettercnt[c];
        for(int i=0;i<s.size();++i){
            if(--lettercnt[s[i]]>=0)
                cnt++;
            while(cnt==t.size()){
                if(minlen>i-left+1){
                    minlen=i-left+1;
                    res=s.substr(left,minlen);
                }
                if(++lettercnt[s[left]]>0)
                    --cnt;
                ++left;
            }
        }
        return res;
    }
};
```
