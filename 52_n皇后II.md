# 代码
```c++
class Solution {
public:
    vector<bool> dg, udg, col;
    int n;
    int res = 0;
    int totalNQueens(int _n) {
        n = _n;
        dg = udg = vector<bool>(2 * n);
        col = vector<bool>(n);
        dfs(0);
        return res;
    }
    void dfs(int u)
    {
        if(u == n)
        {
            res ++;
            return;
        }
        for(int i =0;i < n;i ++)
        {
            if(!col[i] && !dg[u - i + n] && !udg[u + i])
            {
                col[i] = dg[u - i + n]  = udg[u + i] = true;
                dfs(u + 1);
                col[i] = dg[u - i + n]  = udg[u + i] = false;
            }
        }
    }
};
```