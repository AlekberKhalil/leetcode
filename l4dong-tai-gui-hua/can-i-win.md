# Can I Win

In the "100 game," two players take turns adding, to a running total, any integer from 1..10. The player who first causes the running total to reach or exceed 100 wins.

What if we change the game so that players cannot re-use integers?

For example, two players might take turns drawing from a common pool of numbers of 1..15 without replacement until they reach a total &gt;= 100.

Given an integer`maxChoosableInteger`and another integer`desiredTotal`, determine if the first player to move can force a win, assuming both players play optimally.

You can always assume that`maxChoosableInteger`will not be larger than 20 and`desiredTotal`will not be larger than 300.

**Example**

```text
Input:

maxChoosableInteger = 10
desiredTotal = 11


Output:

false


Explanation:

No matter which integer the first player choose, the first player will lose.
The first player can choose an integer from 1 up to 10.
If the first player choose 1, the second player can only choose integers from 2 up to 10.
The second player will win by choosing 10 and get a total = 11, which is 
>
= desiredTotal.
Same with other integers chosen by the first player, the second player will always win.
```

分析

用map记录visited，key是现在visited数组（相当棋牌现状），value是bool

胜者是选了该K并且sum &gt;0.对比石头游戏两头取，剩下的sum&gt;1/2total

```text
class Solution:
    def canIWin(self, maxChoosableInteger: int, desiredTotal: int) -> bool:
        if (1+maxChoosableInteger)*maxChoosableInteger/2 < desiredTotal:
            return False
        m = [0]*(1<<20)#只能0-maxChoosableInteger 要不会tle
        def helper(k,sm):
            if sm<=0 or  m[k]:#这里sm是另一个返回的条件，要注意
                return sm >0 and m[k] == 1 
            for i in range(0,maxChoosableInteger):
                if not k&(1<<i) and not helper(k|1<<i,sm-i-1):
                    m[k] = 1
                    return True
            m[k] = -1
            return False
        res = helper(0,desiredTotal)
        return True if res or desiredTotal < 2  else False
```

