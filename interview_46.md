[To Index](/index.md)
---
#面试题46. 把数字翻译成字符串
难度:Medium
> 给定一个数字，我们按照如下规则把它翻译为字符串：0 翻译成 “a” ，1 翻译成 “b”，……，11 翻译成 “l”，……，25 翻译成 “z”。一个数字可能有多个翻译。请编程实现一个函数，用来计算一个数字有多少种不同的翻译方法。

 

```
示例 1:

输入: 12258
输出: 5
解释: 12258有5种不同的翻译，分别是"bccfi", "bwfi", "bczi", "mcfi"和"mzi"
 

提示：

0 <= num < 231
```


从末尾开始拆分，一位数必然是可行的，所以需要判断是否两位数是一个合法的翻译。

```
class Solution {
public:
    int translateNum(int num) {
        if(num<10) return 1;
        int k=num%100;
        if(k>9 && k<26) return translateNum(num/100)+translateNum(num/10);
        else return translateNum(num/10);

    }
};
```

> 执行用时 :0 ms, 在所有 C++ 提交中击败了100.00%的用户   
内存消耗 :6 MB, 在所有 C++ 提交中击败了100.00%的用户
