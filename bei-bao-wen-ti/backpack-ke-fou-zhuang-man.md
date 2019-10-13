# Backpack\(可否装满）

Given _n_ items with size Ai, an integer _m_ denotes the size of a backpack. How full you can fill this backpack?

#### Example

```text
Example 1:
	Input:  [3,4,8,5], backpack size=10
	Output:  9

Example 2:
	Input:  [2,3,5,7], backpack size=12
	Output:  12
	
```

#### Challenge

O\(n x m\) time and O\(m\) memory.

O\(n x m\) memory is also acceptable if you do not know how to optimize memory.

#### Notice

You can not divide any item into small pieces.

分析

当前解是否可以从前面得到

```text
class Solution:
    """
    @param m: An integer m denotes the size of a backpack
    @param A: Given n items with size A[i]
    @return: The maximum size
    """
    def backPack(self, m, A):
        # write your code here
        n = len(A)
        dp = [False]*(m+1)
        dp[0] = True
        res = 0
        for i in range(n):
            for v in range(m,A[i]-1,-1):
                if dp[v-A[i]]:
                    dp[v] = True
                    res = max(res,v)
        return res

```

