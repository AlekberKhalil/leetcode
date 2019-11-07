# Burst Balloons

Given`n`balloons, indexed from`0`to`n-1`. Each balloon is painted with a number on it represented by array`nums`. You are asked to burst all the balloons. If the you burst balloon`i`you will get`nums[left] * nums[i] * nums[right]`coins. Here`left`and`right`are adjacent indices of`i`. After the burst, the`left`and`right`then becomes adjacent.

Find the maximum coins you can collect by bursting the balloons wisely.

**Note:**

* You may imagine

  `nums[-1] = nums[n] = 1`

  . They are not real therefore you can not burst them.

* 0 ≤

  `n`

  ≤ 500, 0 ≤

  `nums[i]`

  ≤ 100

**Example:**

```text
Input:
[3,1,5,8]
Output:
167 

Explanation: 
nums = [3,1,5,8] --
>
 [3,5,8] --
>
   [3,8]   --
>
  [8]  --
>
 []
             coins =  3*1*5      +  3*5*8    +  1*3*8      + 1*8*1   = 167
```

分析

区间内气球全部消掉，所以区间内loop数和区间外头尾\*

数组前后延长1考虑边界

```text
class Solution:
    def maxCoins(self, nums: List[int]) -> int:
        n = len(nums)
        p = [[1]*(n+2) for _ in range(n+2)]#初始化为1
        nums = [1]+nums+[1]#数组延长就不用考虑边界

        def helper(s,e):
            if s > e:
                return 0
            if p[s][e]!=1:
                return p[s][e]
            mx = float('-inf')
            for k in range(s,e+1):                
                val = nums[s-1]*nums[k]*nums[e+1]#s,e区间全部没了，取外面的。
                left = helper(s,k-1)
                right = helper(k+1,e)
                mx = max(mx,left+right+val)

            p[s][e] = mx
            return mx
        return helper(1,n)
```

