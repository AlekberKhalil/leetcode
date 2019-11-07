# Coin Change 2



You are given coins of different denominations and a total amount of money. Write a function to compute the number of combinations that make up that amount. You may assume that you have infinite number of each kind of coin.

* 
**Example 1:**

```text
Input: amount = 5, coins = [1, 2, 5]Output: 4Explanation: there are four ways to make up the amount:5=55=2+2+15=2+1+1+15=1+1+1+1+1
```

**Example 2:**

```text
Input: amount = 3, coins = [2]Output: 0Explanation: the amount of 3 cannot be made up just with coins of 2.
```

**Example 3:**

```text
Input: amount = 10, coins = [10] Output: 1
```

**Note:**

You can assume that

* 0 &lt;= amount &lt;= 5000
* 1 &lt;= coin &lt;= 5000
* the number of coins is less than 500
* the answer is guaranteed to fit into signed 32-bit integer

分析

完全背包

这里注意coin外层，amount内层，是为了防止221 he 212这样重复出现

[https://leetcode.com/problems/coin-change-2/discuss/141076/Logical-Thinking-with-Clear-Java-Code](https://leetcode.com/problems/coin-change-2/discuss/141076/Logical-Thinking-with-Clear-Java-Code)

```text
class Solution:    def change(self, amount: int, coins: List[int]) -> int:                dp = [0] * (amount+1)        dp [0] = 1        for c in coins:            for i in range(c,amount+1):                                            dp[i] += dp[i-c]        return dp[amount]        
```

