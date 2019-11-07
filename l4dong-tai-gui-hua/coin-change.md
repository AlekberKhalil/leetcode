# Coin Change

You are given coins of different denominations and a total amount of moneyamount. Write a function to compute the fewest number of coins that you need to make up that amount. If that amount of money cannot be made up by any combination of the coins, return`-1`.

**Example 1:**

```text
Input: coins = [1, 2, 5], amount = 11Output: 3Explanation: 11 = 5 + 5 + 1
```

**Example 2:**

```text
Input: coins = [2], amount = 3Output: -1
```

**Note**:  
You may assume that you have an infinite number of each kind of coin.

分析

01背包，装满背包。p\[0\] = 0

```text
class Solution(object):    def coinChange(self, coins, amount):        """        :type coins: List[int]        :type amount: int        :rtype: int        """        p = [float('inf')]*(amount+1)        p[0] =0        for i in range(1,amount+1):            for c in coins:                if i - c >=0:                    p[i] = min(p[i],p[i-c]+1)        return p[amount] if p[amount]!=float('inf') else -1
```

