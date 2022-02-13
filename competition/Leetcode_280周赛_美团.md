# 6004. 得到 0 的操作数
```c++
class Solution {
public:
    int countOperations(int num1, int num2) {
        int res = 0;
        while(num1 && num2)
        {
            res ++;
            if(num1 > num2) num1 = num1 - num2;
            else num2 = num2 - num1;
        }
        return res;
    }
};
```
# 6005. 使数组变成交替数组的最少操作数
给你一个下标从 0 开始的数组 nums ，该数组由 n 个正整数组成。

如果满足下述条件，则数组 nums 是一个 交替数组 ：

nums[i - 2] == nums[i] ，其中 2 <= i <= n - 1 。
nums[i - 1] != nums[i] ，其中 1 <= i <= n - 1 。
在一步 操作 中，你可以选择下标 i 并将 nums[i] 更改 为 任一 正整数。

返回使数组变成交替数组的 最少操作数 。

 

示例 1：
```
输入：nums = [3,1,3,2,4,3]
输出：3
解释：
使数组变成交替数组的方法之一是将该数组转换为 [3,1,3,1,3,1] 。
在这种情况下，操作数为 3 。
可以证明，操作数少于 3 的情况下，无法使数组变成交替数组。
```
示例 2：
```
输入：nums = [1,2,2,2,2]
输出：2
解释：
使数组变成交替数组的方法之一是将该数组转换为 [1,2,1,2,1].
在这种情况下，操作数为 2 。
注意，数组不能转换成 [2,2,2,2,2] 。因为在这种情况下，nums[0] == nums[1]，不满足交替数组的条件。
```
## 代码
```c++
class Solution {
public:
    int minimumOperations(vector<int>& nums) {
        int n = nums.size();
        vector<int> odd(100001, 0);
        vector<int> even(100001, 0);
        for(int i = 0;i < nums.size();i ++){
            if(i & 1) odd[nums[i]] ++;
            else even[nums[i]] ++;
        }
        int odd_index = max_element(odd.begin(),odd.end()) - odd.begin();
        int even_index = max_element(even.begin(), even.end()) - even.begin();
        if(odd_index != even_index) return n - odd[odd_index] - even[even_index];
        else{
            int tmp_odd = odd[odd_index];
            int temp_even = even[even_index];
            even[even_index] = 0;
            even_index = max_element(even.begin(),even.end()) - even.begin();

            odd[odd_index] = 0;
            odd_index = max_element(odd.begin(),odd.end()) - odd.begin();
            return n - max(even[even_index] + tmp_odd, temp_even + odd[odd_index]);
        }
        return 0;
    }
};
```
## 思路
1. 统计奇数和偶数出现的次数
2. 查询在奇数数组和偶数数组中出现的最大索引
3. 如果是同一个数，就返回n - 偶数最大数的次数和奇数最大数的次数
4. 如果是不同的数 就返回出现最大数+次大数

# 6006. 拿出最少数目的魔法豆
给你一个 正 整数数组 beans ，其中每个整数表示一个袋子里装的魔法豆的数目。


请你从每个袋子中 拿出 一些豆子（也可以 不拿出），使得剩下的 非空 袋子中（即 至少 还有 一颗 魔法豆的袋子）魔法豆的数目 相等 。一旦魔法豆从袋子中取出，你不能将它放到任何其他的袋子中。

请你返回你需要拿出魔法豆的 最少数目。

 

示例 1：
```
输入：beans = [4,1,6,5]
输出：4
解释：
- 我们从有 1 个魔法豆的袋子中拿出 1 颗魔法豆。
  剩下袋子中魔法豆的数目为：[4,0,6,5]
- 然后我们从有 6 个魔法豆的袋子中拿出 2 个魔法豆。
  剩下袋子中魔法豆的数目为：[4,0,4,5]
- 然后我们从有 5 个魔法豆的袋子中拿出 1 个魔法豆。
  剩下袋子中魔法豆的数目为：[4,0,4,4]
总共拿出了 1 + 2 + 1 = 4 个魔法豆，剩下非空袋子中魔法豆的数目相等。
没有比取出 4 个魔法豆更少的方案。
```
示例 2：
```
输入：beans = [2,10,3,2]
输出：7
解释：
- 我们从有 2 个魔法豆的其中一个袋子中拿出 2 个魔法豆。
  剩下袋子中魔法豆的数目为：[0,10,3,2]
- 然后我们从另一个有 2 个魔法豆的袋子中拿出 2 个魔法豆。
  剩下袋子中魔法豆的数目为：[0,10,3,0]
- 然后我们从有 3 个魔法豆的袋子中拿出 3 个魔法豆。
  剩下袋子中魔法豆的数目为：[0,10,0,0]
总共拿出了 2 + 2 + 3 = 7 个魔法豆，剩下非空袋子中魔法豆的数目相等。
没有比取出 7 个魔法豆更少的方案。
```

## 代码
```c++
class Solution {
public:
    long long minimumRemoval(vector<int>& beans) {
        long long res = LONG_MAX;
        sort(beans.begin(), beans.end());
        long long  n = beans.size();
        long long sum = 0;
        for(int i = 0;i < beans.size();i ++) sum += beans[i];

        for(int i = 0;i < n;i ++)
        {
            res = min(res, sum - (n - i) * beans[i]);
        }
        return res;
    }
};
```
## 思路
排序之后，枚举所有的beans，用总和减去总和就是魔法豆的数量
# 6007. 数组的最大与和
给你一个长度为 n 的整数数组 nums 和一个整数 numSlots ，满足2 * numSlots >= n 。总共有 numSlots 个篮子，编号为 1 到 numSlots 。

你需要把所有 n 个整数分到这些篮子中，且每个篮子 至多 有 2 个整数。一种分配方案的 与和 定义为每个数与它所在篮子编号的 按位与运算 结果之和。

比方说，将数字 [1, 3] 放入篮子 1 中，[4, 6] 放入篮子 2 中，这个方案的与和为 (1 AND 1) + (3 AND 1) + (4 AND 2) + (6 AND 2) = 1 + 1 + 0 + 2 = 4 。
请你返回将 nums 中所有数放入 numSlots 个篮子中的最大与和。

 

示例 1：
```
输入：nums = [1,2,3,4,5,6], numSlots = 3
输出：9
解释：一个可行的方案是 [1, 4] 放入篮子 1 中，[2, 6] 放入篮子 2 中，[3, 5] 放入篮子 3 中。
最大与和为 (1 AND 1) + (4 AND 1) + (2 AND 2) + (6 AND 2) + (3 AND 3) + (5 AND 3) = 1 + 0 + 2 + 2 + 3 + 1 = 9 。
```
示例 2：
```
输入：nums = [1,3,10,4,7,1], numSlots = 9
输出：24
解释：一个可行的方案是 [1, 1] 放入篮子 1 中，[3] 放入篮子 3 中，[4] 放入篮子 4 中，[7] 放入篮子 7 中，[10] 放入篮子 9 中。
最大与和为 (1 AND 1) + (1 AND 1) + (3 AND 3) + (4 AND 4) + (7 AND 7) + (10 AND 9) = 1 + 1 + 3 + 4 + 7 + 8 = 24 。
注意，篮子 2 ，5 ，6 和 8 是空的，这是允许的。
```
## 代码
```c++
const int N = 3e5 + 9;
int n, m, a, b;

class Solution {
public:
    // dp[i][j] 表示可用的数字状态为i，桶的序号为j 等同于可用的桶的数目
    int dp[N][10];
    // S 为二进制，表示可用的数字状态 s表示现在箱子的序号 p表示现在数字的剩余个数
    int dfs(vector<int>& nums,int S ,int s,int p)
    {
        if(dp[S][s] != -1) return dp[S][s];
        int res = 0;
        // 箱子不放的时候
        if((s - 1) * 2 >= p) res = dfs(nums, S, s - 1, p);
        for(int i = 0;i < n;i ++)
        {
            if(S >> i & 1)
            {
                // nums[i] 可以使用
                int o =S ^  (1 << i);
                if((s - 1) * 2 >= (p - 1))
                    res = max(res, dfs(nums, o, s - 1, p -1) + (nums[i]  & s));
                // 枚举放两个数字的情况
                for(int j = i + 1;j < n;j ++)
                {
                    if(S >> j & 1)
                    {
                        res = max(res, dfs(nums, o ^ (1 << j), s - 1, p -2 )+ (nums[i] & s) + (nums[j] & s));
                    }
                }
            }
        }
        dp[S][s] = res;// 记忆化
        return res;
    }
    int maximumANDSum(vector<int>& nums, int s) {
        n = nums.size();
        int o = (1 << n) - 1;
        // 初始化
        for(int i = 1;i <= o;i ++) {
            memset(dp[i],-1,sizeof dp[i]);
        } 
        memset(dp[0],0,sizeof dp[0]);
        return dfs(nums,o,s,n);
    }
};
```