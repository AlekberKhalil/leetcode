# Predict the Winner

Given an array of scores that are non-negative integers. Player 1 picks one of the numbers from either end of the array followed by the player 2 and then player 1 and so on. Each time a player picks a number, that number will not be available for the next player. This continues until all the scores have been chosen. The player with the maximum score wins.

Given an array of scores, predict whether player 1 is the winner. You can assume each player plays to maximize his score.

**Example 1:**

```text
Input: [1, 5, 2]Output: FalseExplanation: Initially, player 1 can choose between 1 and 2. If he chooses 2 (or 1), then player 2 can choose from 1 (or 2) and 5. If player 2 chooses 5, then player 1 will be left with 1 (or 2). So, final score of player 1 is 1 + 2 = 3, and player 2 is 5. Hence, player 1 will never be the winner and you need to return False.
```

**Example 2:**

```text
Input: [1, 5, 233, 7]Output: TrueExplanation: Player 1 first chooses 1. Then player 2 have to choose between 5 and 7. No matter which number player 2 choose, player 1 can choose 233.Finally, player 1 has more score (234) than player 2 (12), so you need to return True representing player1 can win.
```

**Note:**

1. 1 

   &lt;

   = length of the array 

   &lt;

   = 20.

2. Any scores in the given array are non-negative integers and will not exceed 10,000,000.
3. If the scores of both players are equal, then player 1 is still the winner.

分析

dp存当前i,j范围内，2个player的得分差。

当前得分去掉对手赢的得分差。

len 长度1-n-1 长度0时候就是Nums\[i\]，i \[0，n-1\]

```text
class Solution:    def PredictTheWinner(self, nums: List[int]) -> bool:        n = len(nums)        # sm = [0]*(n+1)        # for i in range(n):        #     sm[i+1] = sm[i]+nums[i]        #dp:diff between players        dp = [[float('-inf')]*(n) for _ in range(n)]        # dp[0][0] = 0        for i in range(n):            dp[i][i] = nums[i]#长度0        for ln in range(1,n):  #长度1->n-1                      for i in range(0,n-ln):                dp[i][i+ln] = max(nums[i] - dp[i+1][i+ln],nums[i+ln]-dp[i][i+ln-1])        return dp[0][n-1] >=0
```

dfs

```text
class Solution:    def PredictTheWinner(self, nums: List[int]) -> bool:        n = len(nums)        dp = [[float('-inf')]*(n) for _ in range(n)]        def dfs(s,e):            if s>e:                return 0            if dp[s][e] != float('-inf'):                return dp[s][e]            if s==e:                return nums[s]            dp[s][e] = max(nums[s]-dfs(s+1,e),nums[e]-dfs(s,e-1))            return dp[s][e]        return dfs(0,n-1)>=0
```

