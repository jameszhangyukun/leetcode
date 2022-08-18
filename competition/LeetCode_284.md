## 6031. 找出数组中的所有 K 近邻下标

给你一个下标从 0 开始的整数数组 nums 和两个整数 key 和 k 。K 近邻下标 是 nums 中的一个下标 i ，并满足至少存在一个下标 j 使得 |i - j| <= k 且 nums[j] == key 。

以列表形式返回按 递增顺序 排序的所有 K 近邻下标。


示例 1：

输入：
```
nums = [3,4,9,1,3,9,5], key = 9, k = 1
```
输出：

```
[1,2,3,4,5,6]
```
解释：因此，nums[2] == key 且 nums[5] == key 。
- 对下标 0 ，|0 - 2| > k 且 |0 - 5| > k ，所以不存在 j 使得 |0 - j| <= k 且 nums[j] == key 。所以 0 不是一个 K 近邻下标。
- 对下标 1 ，|1 - 2| <= k 且 nums[2] == key ，所以 1 是一个 K 近邻下标。
- 对下标 2 ，|2 - 2| <= k 且 nums[2] == key ，所以 2 是一个 K 近邻下标。
- 对下标 3 ，|3 - 2| <= k 且 nums[2] == key ，所以 3 是一个 K 近邻下标。
- 对下标 4 ，|4 - 5| <= k 且 nums[5] == key ，所以 4 是一个 K 近邻下标。
- 对下标 5 ，|5 - 5| <= k 且 nums[5] == key ，所以 5 是一个 K 近邻下标。
- 对下标 6 ，|6 - 5| <= k 且 nums[5] == key ，所以 6 是一个 K 近邻下标。
  因此，按递增顺序返回 [1,2,3,4,5,6] 。
  示例 2：


输入：
```
nums = [2,2,2,2,2], key = 2, k = 2
```
输出：
```
[0,1,2,3,4]
```
解释：对 nums 的所有下标 i ，总存在某个下标 j 使得 |i - j| <= k 且 nums[j] == key ，所以每个下标都是一个 K 近邻下标。
因此，返回 [0,1,2,3,4] 。
### 思路 
暴力枚举所有的可能，对于每一个数枚举距离k内的所有j，如果存在和key相等的数，则保存下标并排序
### 代码
```c++
class Solution {
public:
    vector<int> findKDistantIndices(vector<int>& nums, int key, int k) {
        vector<int> res;
        for(int i = 0;i < nums.size();i ++)
        {
            for(int j = i - k;j <= i + k;j ++)
            {
                if(j && j < nums.size() && nums[j] == key)
                {
                    res.push_back(i);
                }
            }
        }
        sort(res.begin(),res.end());
        return res;
    }
};
```
## 5203. 统计可以提取的工件

存在一个 n x n 大小、下标从 0 开始的网格，网格中埋着一些工件。给你一个整数 n 和一个下标从 0 开始的二维整数数组 artifacts ，artifacts 描述了矩形工件的位置，其中 artifacts[i] = [r1i, c1i, r2i, c2i] 表示第 i 个工件在子网格中的填埋情况：
(r1i, c1i) 是第 i 个工件 左上 单元格的坐标，且
(r2i, c2i) 是第 i 个工件 右下 单元格的坐标。

你将会挖掘网格中的一些单元格，并清除其中的填埋物。如果单元格中埋着工件的一部分，那么该工件这一部分将会裸露出来。如果一个工件的所有部分都都裸露出来，你就可以提取该工件。
给你一个下标从 0 开始的二维整数数组 dig ，其中 dig[i] = [ri, ci] 表示你将会挖掘单元格 (ri, ci) ，返回你可以提取的工件数目。


生成的测试用例满足：
不存在重叠的两个工件。
每个工件最多只覆盖 4 个单元格。
dig 中的元素互不相同。


示例 1：

```
输入：n = 2, artifacts = [[0,0,0,0],[0,1,1,1]], dig = [[0,0],[0,1]]
输出：1
解释：
不同颜色表示不同的工件。挖掘的单元格用 'D' 在网格中进行标记。
有 1 个工件可以提取，即红色工件。
蓝色工件在单元格 (1,1) 的部分尚未裸露出来，所以无法提取该工件。
因此，返回 1 。
```
示例 2：

```
输入：n = 2, artifacts = [[0,0,0,0],[0,1,1,1]], dig = [[0,0],[0,1],[1,1]]
输出：2
解释：红色工件和蓝色工件的所有部分都裸露出来（用 'D' 标记），都可以提取。因此，返回 2 。 
```
### 思路
首先统计dig能覆盖的区域，然后判断每一个工件的所有位置，是否都被覆盖，如果都被覆盖，则记为被覆盖的工件
### 代码
```c++
class Solution {
public:
    int digArtifacts(int n, vector<vector<int>>& artifacts, vector<vector<int>>& dig) {
        vector<bool> f(n * n);
        for(auto d : dig) {
            int index = n * d[0] + d[1];
            f[index] = true;
        }
        int ans = 0;
        for(auto art : artifacts){
            bool flag = true;
            for(int i = art[0];i <= art[2] && flag;i ++)
            {
                for(int j = art[1];j <= art[3] && flag;j ++)
                {
                    flag = f[i * n + j];
                    if(!flag) break;
                }
            }
            if(flag) ans ++; 
        }
        return ans;
    }
};
```
## 2202. K 次操作后最大化顶端元素
给你一个下标从 0 开始的整数数组 nums ，它表示一个 栈 ，其中 nums[0] 是栈顶的元素。

每一次操作中，你可以执行以下操作 之一 ：

如果栈非空，那么 删除 栈顶端的元素。
如果存在 1 个或者多个被删除的元素，你可以从它们中选择任何一个，添加 回栈顶，这个元素成为新的栈顶元素。
同时给你一个整数 k ，它表示你总共需要执行操作的次数。

请你返回 恰好 执行 k 次操作以后，栈顶元素的 最大值 。如果执行完 k 次操作以后，栈一定为空，请你返回 -1 。



示例 1：
```
输入：
nums = [5,2,2,4,0,6], k = 4
输出：5
解释：
4 次操作后，栈顶元素为 5 的方法之一为：
- 第 1 次操作：删除栈顶元素 5 ，栈变为 [2,2,4,0,6] 。
- 第 2 次操作：删除栈顶元素 2 ，栈变为 [2,4,0,6] 。
- 第 3 次操作：删除栈顶元素 2 ，栈变为 [4,0,6] 。
- 第 4 次操作：将 5 添加回栈顶，栈变为 [5,4,0,6] 。
  注意，这不是最后栈顶元素为 5 的唯一方式。但可以证明，4 次操作以后 5 是能得到的最大栈顶元素。
```  
  
示例 2：
```
输入：nums = [2], k = 1
输出：-1
解释：
第 1 次操作中，我们唯一的选择是将栈顶元素弹出栈。
由于 1 次操作后无法得到一个非空的栈，所以我们返回 -1 。
```

### 思路
每次只能进行从剩余元素中选择最大值，或者删除当前栈顶元素，考虑三种情况
1. 如果k > nums.size() 此时我们把所有元素出栈之后，还有多余的次数必定能从出栈的所有的元素中选择最大值
2. 如果k == num.size() 我们能去的最大元素就是前k-1个元素中的最大值
3. 如果k < nums.size() 此时能得到的值就是前k-1个元素和当前栈顶元素的最大值
### 实现代码
```c++
class Solution {
public:
    int maximumTop(vector<int>& nums, int k) {
        if(nums.size() == 1 && k % 2 == 1) return -1;
        int maxv = -1;
        for(int i = 0;i < nums.size() - 1;i ++) maxv = max(maxv, nums[i]);

        if(k > nums.size()) return max(maxv, nums[nums.size() - 1]);
        else if(k == nums.size()) return maxv;

        maxv = - 1;
        for(int i = 0;i < k - 1;i ++) maxv = max(maxv, nums[i]);
        return max(maxv, nums[k]);

    }
};

```
## 2203. 得到要求路径的最小带权子图
给你一个整数 n ，它表示一个 带权有向 图的节点数，节点编号为 0 到 n - 1 。

同时给你一个二维整数数组 edges ，其中 edges[i] = [fromi, toi, weighti] ，表示从 fromi 到 toi 有一条边权为 weighti 的 有向 边。

最后，给你三个 互不相同 的整数 src1 ，src2 和 dest ，表示图中三个不同的点。

请你从图中选出一个 边权和最小 的子图，使得从 src1 和 src2 出发，在这个子图中，都 可以 到达 dest 。如果这样的子图不存在，请返回 -1 。

子图 中的点和边都应该属于原图的一部分。子图的边权和定义为它所包含的所有边的权值之和。



示例 1：

```
输入：n = 6, edges = [[0,2,2],[0,5,6],[1,0,3],[1,4,5],[2,1,1],[2,3,3],[2,3,4],[3,4,2],[4,5,1]], src1 = 0, src2 = 1, dest = 5
输出：9
解释：
上图为输入的图。
蓝色边为最优子图之一。
注意，子图 [[1,0,3],[0,5,6]] 也能得到最优解，但无法在满足所有限制的前提下，得到更优解。

```


示例 2：
```
输入：n = 3, edges = [[0,1,1],[2,1,1]], src1 = 0, src2 = 1, dest = 2
输出：-1
解释：
上图为输入的图。
可以看到，不存在从节点 1 到节点 2 的路径，所以不存在任何子图满足所有限制。
```
### 思路
从src1和src2都能到达dest的子图，一定是从src1->mid，src2->mid，然后从mid2->dest的形式。
所以只需要枚举中间点mid，然后计算src->mid + src->mid + mid->dest之和的最小值就一定是最小权图

### 代码
```c++
class Solution {
public:
    long long minimumWeight(int n, vector<vector<int>>& edges, int src1, int src2, int dest) {
        vector<pair<int,int>> g[n], vg[n];
        for(auto e : edges)
        {
            g[e[0]].push_back({e[1], e[2]});
            vg[e[1]].push_back({e[0],e[2]});
        }
        vector<long long> dist1(n, 1e15), dist2(n, 1e15), dist3(n, 1e15);

        auto f = [&](int s, vector<pair<int,int>> nes[],vector<long long> & dist){
            priority_queue<pair<long long, int>, vector<pair<long long,int>>,greater<pair<long long, int>>> q;
            dist[s] = 0;
            q.push({0, s});
            while(q.size()) {
                auto [cost, node] = q.top();
                q.pop();

                if(cost > dist[node]) continue;
                for(auto [ne, w] : nes[node]){
                    if(cost + w < dist[ne]) {
                        dist[ne] = cost + w;
                        q.push({cost + w, ne});
                    }
                }
            }
        };
        f(src1, g, dist1);
        f(src2, g, dist2);
        f(dest, vg, dist3);
        long long res = 1e15;

        for(int i = 0;i < n;i ++)
        {
            res = min(res, dist1[i] + dist2[i] + dist3[i]);
        }
        if(res > 1e12) return -1;
        return res;
    }
};
```