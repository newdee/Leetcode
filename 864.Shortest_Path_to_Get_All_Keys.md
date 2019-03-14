[To Index](/index.md)
---
# 864. 获取所有钥匙的最短路径

>给定一个二维网格 grid。 "." 代表一个空房间， "#" 代表一堵墙， "@" 是起点，（"a", "b", ...）代表钥匙，（"A", "B", ...）代表锁。
我们从起点开始出发，一次移动是指向四个基本方向之一行走一个单位空间。我们不能在网格外面行走，也无法穿过一堵墙。如果途经一个钥匙，我们就把它捡起来。除非我们手里有对应的钥匙，否则无法通过锁。
假设 K 为钥匙/锁的个数，且满足 1 <= K <= 6，字母表中的前 K 个字母在网格中都有自己对应的一个小写和一个大写字母。换言之，每个锁有唯一对应的钥匙，每个钥匙也有唯一对应的锁。另外，代表钥匙和锁的字母互为大小写并按字母顺序排列。
返回获取所有钥匙所需要的移动的最少次数。如果无法获取所有钥匙，返回 -1 。

方法：采用BFS方法，并通过将位置坐标和钥匙通过位运算保存到一个数里。
1. 首先获取输入向量的尺寸，并创建一个三维向量，因为6把钥匙共有2^6=64中状态，所以三维向量尺寸为`m*n*64`，表示到达每个位置的状。
2. 获取起始点，获取所有钥匙，设置起始点状态为1，表示已经访问过。
3. 当队列不为空时，去除队列中的元素，并拆分成横纵坐标以及钥匙状态，如此时要是状态和所有钥匙一致，则表示所有钥匙都访问到了，直接返回步数。
4. 四种情况，上下左右访问，如果越界或者碰壁则跳过。
5. 如果是锁，则判断是否已经有钥匙了，没有则跳过。
6. 如果是钥匙，则加入到当前的nkeys中，然后判断该位置nkeys是否访问过，如果访问过表示之前钥匙已经添加过了，跳过循环。
7. 将横纵坐标和钥匙状态压进队列，并将状态置1.
8. 等size--循环结束，将步长加1，继续判断队列是否为空，不为空继续循环。
9. 最后循环结束，没有符合keys和`all_keys`相等的情况，返回-1。
```
class Solution {
public:
    int shortestPathAllKeys(vector<string>& grid) {
        int m=grid.size(), n=grid[0].size();
        queue<int> q;
        vector<vector<vector<int>>> state(m,vector<vector<int>>(n,vector<int>(64,0)));
        int all_keys=0;
        int go[]={-1,0,1,0,-1};
        
        for(int i=0;i<m;i++)
            for(int j=0;j<n;j++){
               auto c=grid[i][j];
                if(c=='@')
                {
                    q.push(i<<16 | j<<8);
                    state[i][j][0]=1;
                }
                if(c>='a' && c<='f')
                    all_keys |= 1 << (c-'a');
            }
        
        int step=0;
        while(!q.empty())
        {
           int  size=q.size();
            while(size--)
            {
                int s=q.front();
                q.pop();
                int x=s>>16;
                int y = s>>8 & 0xFF;
                int keys=s & 0xFF;
                if(keys == all_keys)
                    return step;
                for(int i=0;i<4;i++)
                {
                    int nx= x+ go[i];
                    int ny= y+ go[i+1];
                    
                    if(nx <0 || nx >=m ||ny <0 || ny >=n) continue;
                    auto c = grid[nx][ny];
                    int nkeys=keys;
                    if(c=='#') continue;
                    if(c>='A' && c<='F' && !((1<<(c-'A')) & keys) ) continue;
                    if(c>='a' && c<='f') nkeys |= 1<<(c-'a');
                    if(state[nx][ny][nkeys]) continue;
                    q.push((nx <<16) | (ny <<8) | nkeys);
                    state[nx][ny][nkeys]=1;
                }
            }
            step++;
        }
        
        return -1;
        
    }
};

```
