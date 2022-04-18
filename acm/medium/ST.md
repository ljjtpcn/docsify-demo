**ST表**（Sparse Table，稀疏表）是一种简单的数据结构，主要用来解决**RMQ**（Range Maximum/Minimum Query，区间最大/最小值查询）问题。它主要应用倍增的思想，可以实现$O(nlogn)$预处理， $O(1)$查询。
```cpp
int st_min[N][21], st_max[N][21], LOG[N];
for (int i = 1; i <= n; i++)
        cin >> a[i], st_max[i][0] = st_min[i][0] = a[i];

    auto init = [&]() {
        for (int i = 1; i <= 20; i++) { // // 第二维的大小根据数据范围决定，不小于log2(N)
            for (int j = 1; j + (1 << i) - 1 <= n; j++) {
                st_min[j][i] =
                    min(st_min[j][i - 1], st_min[j + (1 << (i - 1))][i - 1]);
                st_max[j][i] =
                    max(st_max[j][i - 1], st_max[j + (1 << (i - 1))][i - 1]);
            }
        }

        for (int i = 2; i <= n; ++i) LOG[i] = LOG[i / 2] + 1;
    };
    init();

    auto getMax = [&](int l, int r) {
        int s = LOG[r - l + 1];
        return max(st_max[l][s], st_max[r - (1 << s) + 1][s]);
    };
    auto getMin = [&](int l, int r) {
        int s = LOG[r - l + 1];
        return min(st_min[l][s], st_min[r - (1 << s) + 1][s]);
    };
```

> [限于篇幅原因，如需理解原理请点击此处跳转知乎文章](https://zhuanlan.zhihu.com/p/105439034)