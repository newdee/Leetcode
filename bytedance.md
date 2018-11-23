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
方法：从第一位开始，如果没有重复的元素，就加到字典中。如果碰到存在过的元素，则求出当前无重复元素个数与最大值之间的最大值（初始最大值为0），然后清空字典，从下一位开始继续判断，直到最后一位。如果最后一位循环结束没有重复的，则比较最后一次字典的大小与之前的最大值，返回最大值。 
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

方法：这题相对简单，新建一个字典存放每个子串的相同位置的元素。从第一位开始，如果出现了的次数为子串个数，则该字符是共同前缀。如果遇到不等的，跳出循环，返回前面的字符串为子串。

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

方法：将s1的左右元素转化成字典，然后将s2的长度为s1的子串转化为字典，如果相等，则返回true。如果不等，删除字典中的最开始的元素，并将最后的后面的一个元素添加进来继续比较。如果遍历S2结束没有返回，则返回false。

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

### 字符串相乘

> 给定两个以字符串形式表示的非负整数 num1 和 num2，返回 num1 和 num2 的乘积，它们的乘积也表示为字符串形式。

```
示例 1:
输入: num1 = "2", num2 = "3"
输出: "6"

示例 2:
输入: num1 = "123", num2 = "456"
输出: "56088"
说明：

num1 和 num2 的长度小于110。
num1 和 num2 只包含数字 0-9。
num1 和 num2 均不以零开头，除非是数字 0 本身。
不能使用任何标准库的大数类型（比如 BigInteger）或直接将输入转换为整数来处理。
```
方法： 由于数字长度为一百多个，所以即使能转化成数字相乘，就算是long long也是放不下的。所以只能采取手动相乘，通过乘法原理转化成各位数相乘之和，最后合并即可。
- 创建一个数组，数组长度是两个数字长度之和。（因为m位数和n位数相乘，最大为m+n位数）
- 然后对于结果中第n位的数，结果是所有索引之和为n的两数相乘的和，由于需要将索引为0的位置留给最高位进位，所以整体索引向右偏移一次。
- 然后从末尾开始判断，如果超过10，表示有进位，保留各位数，将进位加到低一位上。
- 最后判断索引为0的位置有没有进位，有的话加进去，没有的话不管。
- 将每个位置的数字转化为字符加到结果字符串中。
```
class Solution {
public:
    string multiply(string num1, string num2) {
        
        if(num1=="0" || num2 =="0") return "0";
        int l1=num1.length();
        int l2=num2.length();
        int l=l1+l2;
        vector<int>result(l,0);
        for(int i=0;i<l1;i++)
            for(int j=0;j<l2;j++)
            {
                result[i+j+1] +=(num1[i]-'0')*(num2[j]-'0');
                
            }
        for(int i=l-1;i>0;i--)
        {
            if(result[i]>9)
            {
                result[i-1] +=result[i]/10;
                result[i] = result[i]%10;
            }
        }
        string res="";
        if(result[0] > 0)
            res += ('0'+result[0]);
        for(int i=1;i<l;i++)
            res += ('0'+result[i]);

        return res;
    }

};
```

### 翻转字符串里的单词

> 给定一个字符串，逐个翻转字符串中的每个单词。

```
示例:  

输入: "the sky is blue",
输出: "blue is sky the".
说明:

无空格字符构成一个单词。
输入字符串可以在前面或者后面包含多余的空格，但是反转后的字符不能包括。
如果两个单词间有多余的空格，将反转后单词间的空格减少到只含一个。
进阶: 请选用C语言的用户尝试使用 O(1) 空间复杂度的原地解法。
```


方法：先将所有字符翻转，然后每遇到一个空格，翻转一次，如果最后一个不是空格，则最后一个单词未翻转，翻转一次。如果翻转结束最后一位是空格，则需要删除末尾的空格。注意erase函数的参数，第一个是索引，第二个是删除字符数量。  

```
class Solution {
public:
    void reverseWords(string &s) {
        if (s == " ") s= "";
        reverse(s.begin(),s.end());
        int st=0;
        for(int i=0;i<s.length();i++)
        {
            if(s[i]==' ')
            {
                if(i!=st)
                {
                reverse(s.begin()+st,s.begin()+i);
                st=i+1;
                }
                else if(i<s.length())
                {
                    s.erase(i,1);
                    i--;
                }

            }
        }
         if(st <s.length())
             reverse(s.begin()+st,s.end());
         if(s[s.length()-1]==' ')  s.erase(s.length()-1,1);
  
        
    }
};
```

###  简化路径

> 给定一个文档 (Unix-style) 的完全路径，请进行路径简化。

```
例如，
path = "/home/", => "/home"
path = "/a/./b/../../c/", => "/c"

边界情况:

你是否考虑了 路径 = "/../" 的情况？
在这种情况下，你需返回 "/" 。
此外，路径中也可能包含多个斜杠 '/' ，如 "/home//foo/" 。
在这种情况下，你可忽略多余的斜杠，返回 "/home/foo" 。
```
方法： 路径可以按“/”来分段处理。首先将字符串中每个以"/"结尾的子串压入到一个向量中。如果最后一个路径后没有加"/"，也压入向量中。然后对每个向量元素进行处理
- 如果有路径名为"./"或者"/"，则直接将该元素赋值为空，如果有路径名为"."（通常是结尾），也是一样的处理。
- 如果有路径名为"../"或者".."（通常这个也是结尾），则往前回溯，如果遇到不为空的元素，将该元素和目前的路径名清空。（只能回溯到索引为1处，根目录不能清空）如果回溯完是根目录，则只清空目前路径名。
- 然后将向量中所有非空元素加到结果字符串中。
- 判断结尾字符是否为"/"，如果是，则删除结尾的“/”。
- 返回结果字符串。

```
class Solution {
public:
    string simplifyPath(string path) {
        vector<string> tmp;
        int st=0;
        for(int i=0;i<path.length();i++)
        {
            if(path[i]=='/') {
                tmp.push_back(path.substr(st,i+1-st));
                st=i+1;
            }
                
        }
        if(st<path.length())
            tmp.push_back(path.substr(st,path.length()-st));
        string result;
        for(int i=1;i<tmp.size();i++)
        {
            if(tmp[i] == "./" || tmp[i] == "."||tmp[i]=="/") tmp[i]="";
            if(tmp[i] == "../" || tmp[i] == "..")
            {
                int k=i-1;
                while(k>0 && tmp[k]=="")
                {
                    k--;
                }
                if(k>0) tmp[k]="";
                tmp[i]="";
            }

        }
        for(int i=0;i<tmp.size();i++)
        {
            if(tmp[i]!="")
                result +=tmp[i];
        }
        while(result[result.length()-1]=='/')
        {
            if(result.length()>1)
            result.erase(result.length()-1,1);
            else return result;
        }
        return result;
    }
};
```

### 复原IP地址
> 给定一个只包含数字的字符串，复原它并返回所有可能的 IP 地址格式。

```
示例:

输入: "25525511135"
输出: ["255.255.11.135", "255.255.111.35"]
```

方法：ip地址每一段范围是0-255，也就是1-3位数字，逐个循环判断。如果是有效IP，则压入向量中。  
- 判断是否有效的函数：首先看，每一段地址长度是否大于1，如果大于1，且开头是0的IP属于无效IP直接返回false。然后将IP转为长整型(最大可能有10位)，然后看每一位范围是否大于255，如果大于直接返回false。循环结束，返回true。
- 标准化输出结果，将IP写为数字加'.'的形式输出。  
```
class Solution {
public:
    vector<string> restoreIpAddresses(string s) {
        vector<string> res;
        vector<string> tmp(4,"");
        int l=s.length();

            for(int i=1;i<4;i++)
            {

                    for(int j=1;j<4;j++)
                    {
                            for(int k=1;k<4;k++)
                            {
                                if(i+j+k<l){
                                tmp[0]=s.substr(0,i);
                                tmp[1]=s.substr(i,j);
                                tmp[2]=s.substr(i+j,k);
                                tmp[3]=s.substr(i+j+k,l-i-j-k);
                                if(isvalid(tmp)) res.push_back(ip(s,i,j,k));
                            }
                            }
                        }
                    }
        return res;

    }
private:
    bool isvalid(vector<string> t)
    {
        for(int i=0;i<4;i++)
            if(t[i].length()>1 && t[i][0]=='0') return false;
        for(int i=0;i<4;i++)
            if(atol(t[i].c_str())>255) return false;
        return true;
    }
    string ip(string s,int i, int j, int k)
    {
        string result;
        result = s.substr(0,i)+'.'+s.substr(i,j)+'.'+s.substr(i+j,k)+'.'+s.substr(i+j+k,s.length()-i-j-k);
        return result;
    }
};
```
