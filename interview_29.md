[To Index](/index.md)
---
# 面试题29. 顺时针打印矩阵
难度:Easy

> 输入一个矩阵，按照从外向里以顺时针的顺序依次打印出每一个数字。

 
```

示例 1：

输入：matrix = [[1,2,3],[4,5,6],[7,8,9]]
输出：[1,2,3,6,9,8,7,4,5]
示例 2：

输入：matrix = [[1,2,3,4],[5,6,7,8],[9,10,11,12]]
输出：[1,2,3,4,8,12,11,10,9,5,6,7]
 

限制：

0 <= matrix.length <= 100
0 <= matrix[i].length <= 100
```
Code:

```
class Solution {
public:
    vector<int> spiralOrder(vector<vector<int>>& matrix) {
        vector<int>res;
        if(matrix.empty() || matrix[0].empty()) return res;
        int rstart=0;
        int rend=matrix.size()-1;
        int cstart=0;
        int cend=matrix[0].size()-1;

        while( !(rstart> rend || cstart>cend) )
        {
            if(rstart== rend && cstart == cend)
            {
                res.push_back(matrix[rstart][cstart]);
                return res;
            }
            else if(rstart == rend)
            {
                for(int i=cstart;i<=cend;i++)
                res.push_back(matrix[rstart][i]);
                return res;
            }
            else if(cstart == cend)
            {
                for(int i=rstart;i<=rend;i++)
                res.push_back(matrix[i][cstart]);
                return res;
            }
            else
            {
                for(int j=cstart;j<cend;j++)
                {
                    res.push_back(matrix[rstart][j]);

                }
                for(int i=rstart;i<=rend;i++)
                {
                    res.push_back(matrix[i][cend]);

                }

                for(int j=cend-1;j>=cstart;j--)
                {
                    res.push_back(matrix[rend][j]);

                }
                for(int i=rend-1;i>rstart;i--)
                {
                    res.push_back(matrix[i][cstart]);
                }
                rstart++;
                cstart++;
                rend--;
                cend--;
            }

    }
    return res;
    }
};
```

> 执行用时 :16 ms, 在所有 C++ 提交中击败了81.08%的用户   
内存消耗 :10MB, 在所有 C++ 提交中击败了100.00%的用户
