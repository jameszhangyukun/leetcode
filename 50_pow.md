# 代码
```c++
class Solution {
public:
    double myPow(double x, int n) {
        double ans = 1, p = x;
        long long t = abs((long long)(n));
        for (; t; t >>= 1) { // 将 n 进行二进制拆分。
            if (t & 1)
                ans = ans * p; // p 是提前计算好的批量连乘。
            p = p * p; // 每次更新 p，自身平方。
        }
         return n > 0 ? ans : 1 / ans;
    }
};
```