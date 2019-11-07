# Paint House II\(DP\)

There are a row of`n`houses, each house can be painted with one of the`k`colors. The cost of painting each house with a certain color is different. You have to paint all the houses such that no two adjacent houses have the same color.

The cost of painting each house with a certain color is represented by a`n`x`k`cost matrix. For example,`costs[0][0]`is the cost of painting house`0`with color`0`;`costs[1][2]`is the cost of painting house`1`with color`2`, and so on... Find the minimum cost to paint all houses.

## Example

Given`n`= 3,`k`= 3,`costs`=`[[14,2,11],[11,14,5],[14,3,10]]`return`10`

house 0 is color 2, house 1 is color 3, house 2 is color 2,`2 + 5 + 3 = 10`

## Challenge

Could you solve it in O\(nk\)?

分析

f\[n\]\[k\]是以k颜色为最后颜色的最小 值。

最大trick是这里当前f\[n\]需要从**完整的**f\[n-1\]层获取最小的和次小的，所以不能一维数组同时做，否则n-1被覆盖被改变。

所以有old\_cost\[:\] = new\_cost\[:\]。记得此处赋值，不能直接赋引用。

因为限制不能和前面一层同色，所以除了n-1层的Min，还需要第二Min来做当前层和千层取同色情况

f\[n\]\[k\] = f\[n-1\]\[min\]+cost 这里 min= min1 if k!= min else min2

```text
class Solution:    """    @param costs: n x k cost matrix    @return: an integer, the minimum cost to paint all houses    """    def minCostII(self, costs):        # write your code here        if not costs or not len(costs):            return 0        n = len(costs)        k = len(costs[0])        old_cost = [0]*k        new_cost = [0] * k        min1 = min2 = -1        for i in range(n):            m1 = m2 = float('inf')            for s, v in enumerate(old_cost):                if v < m2:                    if v<m1:                        m1, m2 = v, m1                        min1, min2 = s, min1                    else:                        m2 = v                        min2 = s            for j in range(k):                if j != min1:                    new_cost[j] = old_cost[min1] + costs[i][j]                else:                    new_cost[j] = old_cost[min2] + costs[i][j]            old_cost[:] = new_cost[:]        return min(new_cost)
```

