# Partition Equal Subset Sum

Given a**non-empty**array containing**only positive integers**, find if the array can be partitioned into two subsets such that the sum of elements in both subsets is equal.

**Note:**

1. Each of the array element will not exceed 100.
2. The array size will not exceed 200.

**Example 1:**

```text
Input: [1, 5, 11, 5]

Output: true

Explanation: The array can be partitioned as [1, 5, 5] and [11].
```

**Example 2:**

```text
Input: [1, 2, 3, 5]

Output: false

Explanation: The array cannot be partitioned into equal sum subsets.
```

分析

01背包需要倒序

```text
class Solution:
    def canPartition(self, nums: List[int]) -> bool:
        sm = sum(nums)
        if sm%2!=0:
            return False
        t = sm//2
        n = len(nums)
        p = [False]*(t+1)
        p[0] = True


        for i in range(n):
            for j in range(t,0,-1):#01背包，需要倒着，因为需要i-1的值。
                if j - nums[i] >= 0 and p[j - nums[i]]:
                    p[j] = True#没有break，否则之后的J都不再计算了。


        return p[t]
```

