# Stone Game

Alex and Lee play a game with piles of stones. There are an even number of piles**arranged in a row**, and each pile has a positive integer number of stones`piles[i]`.

The objective of the game is to end with the most stones. The total number of stones is odd, so there are no ties.

Alex and Lee take turns, with Alex starting first. Each turn, a player takes the entire pile of stones from either the beginning or the end of the row. This continues until there are no more piles left, at which point the person with the most stones wins.

Assuming Alex and Lee play optimally, return`True` if and only if Alex wins the game.

**Example 1:**

```text
Input: [5,3,4,5]Output: trueExplanation: Alex starts first, and can only take the first 5 or the last 5.Say he takes the first 5, so that the row becomes [3, 4, 5].If Lee takes 3, then the board is [4, 5], and Alex takes 5 to win with 10 points.If Lee takes the last 5, then the board is [3, 4], and Alex takes 4 to win with 9 points.This demonstrated that taking the first 5 was a winning move for Alex, so we return true.
```

**Note:**

```text
2 <= piles.length <= 500piles.length is even.1 <= piles[i] <= 500sum(piles) is odd.
```

分析

因为是两头都能取，所以需要i,j记录，所以只能一个头的话，就一维数组

dp\[i\]\[j\] = sum\[i\]\[j\] - min\(dp\[i+1\]\[j\],dp\[i\]\[j-1\]\)

```text
class Solution:    def stoneGame(self, piles: List[int]) -> bool:        n = len(piles)        dp = [[float('-inf')] * (n+1) for _ in range(n+1)]        dp[0][0] = 0        presums = [0]*(n+1)        for i,v in enumerate(piles):            presums[i+1] = v + presums[i]        for i in range(n):            for j in range(i,n+1):                # if i == j:                #     dp[i][j] = piles[i-1]                # else:                    dp[i][j] = presums[j] - presums[i-1] - min(dp[i+1][j],dp[i][j-1])        return presums[-1]/2 - dp[n][n] > 0
```

