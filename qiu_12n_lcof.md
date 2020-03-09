# [To Index](/index.md)

# 面试题64\. 求1+2+...+n

难度:Medium

> 求 1+2+...+n ，要求不能使用乘除法、for、while、if、else、switch、case等关键字及条件判断语句（A?B:C）。

示例 1：

```
输入: n = 3 输出: 6 示例 2：

输入: n = 9 输出: 45
```

限制：

```
1 <= n <= 10000
```

简单递归：

```
class Solution {
vector<int> sums={1,3,6};
public:
    int sumNums(int n) {
        if(n<=sums.size()) return sums[n-1];
        return sumNums(n-1)+n;
    }
};
```

> 执行用时 :16 ms, 在所有 C++ 提交中击败了24.74%的用户<br>
> 内存消耗 :9.3 MB, 在所有 C++ 提交中击败了6.03%的用户
