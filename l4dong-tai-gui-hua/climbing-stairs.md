# Climbing Stairs

You are climbing a stair case. It takesnsteps to reach to the top.

Each time you can either climb 1 or 2 steps. In how many distinct ways can you climb to the top?

**Note:**Givennwill be a positive integer.

分析

DP, n+1的数组，f\[0\] 和f\[1\]都是1 ，计算f\[1\]，f\[2\]推出来的

```text
class Solution {
    public int climbStairs(int n) {
        if(n < 1)
            return n;
        int[] ret = new int[n + 1];
        ret[0] = 1;
        ret[1] = 1;
        for(int i = 2; i <= n ; i ++){
            ret[i] = ret[i - 2] + ret[i - 1]; 
        }
        return ret[n];
    }
}
```

不用数组

```text
class Solution:
    def climbStairs(self, n):
        """
        :type n: int
        :rtype: int
        """
        if n <= 1:
            return 1
        p = 2
        pp = 1
        cur = p # cur = 0 

        for i in range(2,n):
            cur = p+pp
            pp,p = p,cur
        return cur #p
```

