[To Index](/index.md)
---
# 面试题16.01 交换数字
难度:Medium

> 编写一个函数，不用临时变量，直接交换numbers = [a, b]中a与b的值。

```
示例：

输入: numbers = [1,2]
输出: [2,1]
提示：

numbers.length == 2
```

直接异或

```
class Solution {
public:
    vector<int> swapNumbers(vector<int>& numbers) {
        numbers[0] ^=  numbers[1];
        numbers[1] ^=numbers[0];
        numbers[0] ^= numbers[1];
        return numbers;
    }
};
```

> 执行用时 :4 ms, 在所有 C++ 提交中击败了48.49%的用户   
内存消耗 :7.2 MB, 在所有 C++ 提交中击败了100.00%的用户
