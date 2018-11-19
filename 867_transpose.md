[To Index](/index.md)
---
# 867.转置矩阵
这题题目不难，首先是获取向量A的行列，然后行列转置新建向量，并交换行列赋值即可。


```
class Solution {
public:
    vector<vector<int>> transpose(vector<vector<int>>& A) {

        int r,c;
        r= A.size();
        c= A[0].size();
        vector<vector<int>> trans(c,vector<int>(r,0));
        for(int i=0;i<c;i++)
        {

            for (int j=0;j<r;j++)
            {
                trans[i][j]=A[j][i];
            }

    }
        return trans;
    }
};
```
