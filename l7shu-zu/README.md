# L7\_数组

**Median of a array**

个数奇数时候取中间那个数

个数偶数取中间两数的平均

**Maximum Subarray I 和 buy and sell stock**

每次loop时_第二行_用来保存前面最小的Price或者最小的_minSum，这样可以省一次loop_

然后当前的price减去min得到的数字max

**Maximum Subarray III**

```text
//1.要不i自成一组，不跟前面，所以用global因为前面i-1是否包含都行//2.要不i跟前面成一组，则i-1必须包含，因为是连续的，所以用local,因为数组连续，要包含i,前面i-1也要包含//3.可以看做local是分j（堆），glabal是分i（数）。前面讨论当前堆含不含i这个数,后面只讨论含不含i这个数。local[i][j] = Math.max(global[i-1][j-1], local[i-1][j]) + nums[i - 1];//1.不取i，所以前面i-1包不包都可以，用global//2.取i,必须包含i,所以用localglobal[i][j] = Math.max(global[i - 1][j], local[i][j]);
```

**比较 Best Time to Buy and Sell Stock IV**

也是维护global和local, 因为sum是连续相加数组，这里价格买入卖出有加减，所以逻辑有差别。k&gt;n/2之后直接退化为贪心算法

```text
//这次卖或者不卖，卖的话所以加global[i][j] = Math.max(global[i - 1][j], prices[i - 1] + localMax);//之前某次买的，所以要减，这次保存了Local就能省一次loop，有loop的话这里就是f[k][j - 1] - prices[k - 1]k次买的localMax = Math.max(f[i][j - 1] - prices[i - 1], localMax);
```

基本上就是i个数j次数，每次不是i-1就是j-1。j-1就是决定当前这次怎么处理：数组里就是决定属于前堆还是当前堆，股票里就是当前卖不卖，要用当前减去之前某次。和Best Time to Buy and Sell Stock III 中`left[i] = Math.max(prices[i] - minPrice, left[i-1]);`不一样stock中价格相减，此处数字叠加。

**股票问题**

Therefore our definition of`T[i][k]`should really be split into two:`T[i][k][0]`and`T[i][k][1]`, where the**former**denotes the maximum profit at the end of the`i-th`day with at most`k`transactions and with`0`stock in our hand AFTER taking the action, while the**latter**denotes the maximum profit at the end of the`i-th`day with at most`k`transactions and with`1`stock in our hand AFTER taking the action. Now the base cases and the recurrence relations can be written as:

```text
Base cases:T[-1][k][0] = 0, T[-1][k][1] = -InfinityT[i][0][0] = 0, T[i][0][1] = -InfinityRecurrence relations:T[i][k][0] = max(T[i-1][k][0], T[i-1][k][1] + prices[i])T[i][k][1] = max(T[i-1][k][1], T[i-1][k-1][0] - prices[i])
```

For the base cases,`T[-1][k][0] = T[i][0][0] = 0`has the same meaning as before while`T[-1][k][1] = T[i][0][1] = -Infinity`emphasizes the fact that it is impossible for us to have`1`stock in hand if there is no stock available or no transactions are allowed.

总结用法：

可以左边遍历再右边遍历 Shortest Distance to a Character\(必须数组因为返回数组\),[Longest Mountain in Array](https://leetcode.com/problems/longest-mountain-in-array)（可以优化数组为数字因为返回最大值）

**矩阵遍历**

如果行数可以直接计算，列数需要用数组，因为遍历的方向性

bomb enemy

