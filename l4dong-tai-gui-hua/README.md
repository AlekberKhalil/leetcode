# L4\_动态规划

**背包问题**

如果是第一种问法，要求恰好装满背包，那么在初始化时除了f\[0\]为0其它f\[1..V\]均设为-∞，这样就可以保证最终得到的f\[N\]是一种恰好装满背包的最优解。

如果并没有要求必须把背包装满，而是只希望价格尽量大，初始化时应该将f\[0..V\]全部设为0。

状态表示前i件物品放入一个容量为ω的背包可以获得的最大价值。

用value或weight做第二个Index，分拿和不拿状态，选个Max.value和weight那个小选哪个做Index

重复和非重复唯一区别就是拿时候从i+1个状态里选还是i个状态里选。重复的话可以包含当前i+1，不重复不能包含i+1

可重复：拿时候从前i+1个选

```text
dp[i + 1][j] = max{dp[i][j], dp[i + 1][j - w[i]] + v[j]}
```

不重复：拿时候从前i个选

```text
dp[i + 1][j] = max{dp[i][j], dp[i][j - w[i]] + v[j]}
```

01背包问题：

V倒序才能拿到f\[i-1\]\[v\]的 否则就是f\[i\]\[v\]

```text
for i=1..N    for v=V..0        f[v]=max{f[v],f[v-c[i]]+w[i]};
```

Palindrome Partitioning II

i,j关系。j相当于i-1。i: 1-&gt;n j: 0-&gt;i\(不含i）

数组分组问题

maximum subarray

split array largest sum

从palindrome I II和word break I II可知 sequence dp

```text
dp：n+1i: [1,n]j: [0,i)f[i]=f[j] && [j,i) #注意这里f[j]和s[j] 因为f[j]不含s[j]，index错位，f[j]包含的是s[j-1]的情况f[0]要初始化 i range 从1开始
```

```text
dp: ni:[0,n-1]j:[0,i]#包含if[i] = f[j-1] && [j,i] #这里s[j]和f[j-1] 因为f[j-1]含s[j-1] 所以s[i]对应当前要求的f[i]要单独判断j=0的情况，因为有f[j-1]
```

DP问题：[https://zhengyang2015.gitbooks.io/lintcode/house\_robber\_392.html](https://zhengyang2015.gitbooks.io/lintcode/house_robber_392.html)

总结

1需要返回List的结果，dp不明显，考虑一个dp和一个辅助Parent list来求解

2 记忆化搜索**从大到小**的dp，无法从小开始，直接从总结果最大开始。2个loop区间\[i.j\]然后一个loopk拆分区间\[i.j\]。分治思想：stone game,burst balloon

3 排列组合的公式可以用，当需要计算总选择数：Paint Fence，Count Numbers with Unique Digits

4 有环时候去头或者尾，做完再比较哪个大：House Robber II

5 设置2个状态，2个状态交替由对方得到。Wiggle Subsequence

6 区间循环

```text
for ln in range(1,n+1):                        for start in range(1,n+1-ln):
```

7 字串长度 = unique substring数: Unique Substrings in Wraparound String

8 前两天得到第三天的，python可以同时赋值：Delete and Earn，house robber

9 状态类dp，一个人可以有多个选择，can I win, Campus Bikes II. 用bit数组来表示每个人的状态。dp\[i\]\[bit status\] \(bit status = 1&lt;&lt; j\]

```text
bitwise notenum | (1<<k): set num's k-th bit as 1num & (1<<k): get num's k-th bitint prev = s ^ (1 << j);
```

10 博弈类问题

一头取就一维dp，2头取就二维DP\(predict the winner\)，任意取就bit表示状态。 最后决定输赢看sum&gt;0

11 只和前面某个词有关的，和LIS，如果是和前面几个数有关的，比如fibonacii,等比数列，或者山峰最长长度。以2个数取出来，然后往后顺次找序列。

或者2个数出来，根据diff去后面list找第三个数字是否存在。

12 做不出来的时候考虑top down，dfs的分治法，对比dp的bottom up

