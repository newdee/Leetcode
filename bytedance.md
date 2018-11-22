[To Index](/index.md)
---

# 字节跳动推荐

### 挑战字符串
###   无重复字符的最长子串

> 给定一个字符串，请你找出其中不含有重复字符的 最长子串 的长度。

```
示例 1:

输入: "abcabcbb"
输出: 3
解释: 因为无重复字符的最长子串是 "abc"，所以其长度为 3。
示例 2:

输入: "bbbbb"
输出: 1
解释: 因为无重复字符的最长子串是 "b"，所以其长度为 1。
示例 3:

输入: "pwwkew"
输出: 3
解释: 因为无重复字符的最长子串是 "wke"，所以其长度为 3。
     请注意，你的答案必须是 子串 的长度，"pwke" 是一个子序列，不是子串。
```

```
class Solution {
public:
    int lengthOfLongestSubstring(string s) {
        if(s.length() ==0) return 0;
        if(s.length() == 1) return 1;
        int st=0;
        int m=0;
        unordered_map<char,int> tmp;
        for(int i=0;i<s.length();i++)
        {
            if(tmp[s[i]] == 0)
                tmp[s[i]]++;
            else
            {
                m = max(i-st,m);
                i=st++;
                tmp.clear();
            }
            
        }
        st =s.length()-st;
        m=max(m , st);
        return m;
        
    }
};
```

### 无重复字符的最长子串


> 编写一个函数来查找字符串数组中的最长公共前缀。
如果不存在公共前缀，返回空字符串 ""。

```
示例 1:

输入: ["flower","flow","flight"]
输出: "fl"
示例 2:

输入: ["dog","racecar","car"]
输出: ""
解释: 输入不存在公共前缀。
说明:

所有输入只包含小写字母 a-z 。
```

```
class Solution {
public:
    string longestCommonPrefix(vector<string>& strs) {
        if(strs.size()==0) return "";
        if(strs.size() ==1) return strs[0];
        unordered_map<char,int>tmp;
        int i;
        for(i=0;i<strs[0].length();i++)
        {
            for(int j=0;j<strs.size();j++)
            {
                tmp[strs[j][i]]++;
            }
            if(tmp[strs[0][i]] < strs.size())
                break;
            else
                tmp.clear();
        }
        if(i==0) return "";
        else
            return strs[0].substr(0,i);


    }
};
```

### 字符串的排列

> 给定两个字符串 s1 和 s2，写一个函数来判断 s2 是否包含 s1 的排列。
换句话说，第一个字符串的排列之一是第二个字符串的子串。

```
示例1:

输入: s1 = "ab" s2 = "eidbaooo"
输出: True
解释: s2 包含 s1 的排列之一 ("ba").


示例2:

输入: s1= "ab" s2 = "eidboaoo"
输出: False


注意：

输入的字符串只包含小写字母
两个字符串的长度都在 [1, 10,000] 之间
```

方法：
```
class Solution {
public:
    bool checkInclusion(string s1, string s2) {
        if(s1.length()>s2.length()) return false;
        int l1=s1.length();
        int l2=s2.length();
        unordered_map<char,int>tmp1,tmp2;

        for(int i=0;i<l1;i++)
        {
            tmp1[s1[i]]++;
            tmp2[s2[i]]++;
        }
        if(tmp1 == tmp2) return true;
        for(int j=1;l1<l2;j++,l1++)
        {

            if(tmp2[s2[j-1]] == 1)
                tmp2.erase(s2[j-1]);
            else
                tmp2[s2[j-1]]--;
            tmp2[s2[l1]]++;
            if(tmp2 == tmp1) return true;

        }
        return false;
    }

};
```
