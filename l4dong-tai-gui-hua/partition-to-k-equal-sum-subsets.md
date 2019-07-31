# Partition to K Equal Sum Subsets

Given an array of integers`nums`and a positive integer`k`, find whether it's possible to divide this array into`k`non-empty subsets whose sums are all equal.

**Example 1:**

```text
Input:
 nums = [4, 3, 2, 3, 5, 2, 1], k = 4

Output:
 True

Explanation:
 It's possible to divide it into 4 subsets (5), (1, 4), (2,3), (2,3) with equal sums.
```

**Note:**

```text
1 <= k <= len(nums) <= 16.
0 < nums[i] < 10000.
```

分析

此题DP不能做，只能DFS

DP:用01背包，尝试失败。

```text
class Solution:
    def canPartitionKSubsets(self, nums: List[int], k: int) -> bool:
        sm = sum(nums)
        if sm % k !=0:
            return False
        t = sm//4
        n = len(nums)
        f = [[False]*(t+1) for _ in range(k)]       

        for i in range(n):
            for kk in range(k):
                f[kk][0] = True  
                for v in range(t,nums[i]-1,-1):
                        f[kk][v] |= f[kk][v-nums[i]]
        res = False
        for i in range(k):
            res |= f[i][t]
        return res
```

dfs

和combination sum一样，只是target满了就移到下一组。

记住下一组nums从头起，要不nums有值跳过没取到。有seen不会重复

```text
class Solution:
    def canPartitionKSubsets(self, nums: List[int], k: int) -> bool:
        sm = sum(nums)
        if sm % k !=0:
            return False
        target = sm//k
        n = len(nums)
        seen =set()
        #分成K组，每组还是combination sum
        def dfs(cursum,ni,gi):
            if gi == 1:
                return True
            if cursum == target:
                return dfs(0,0,gi-1)#nums从0开始，有seen不怕重复
            for i in range(ni,n):
                if i not in seen:
                    seen.add(i)
                    if dfs(cursum+nums[i],i+1,gi):
                        return True                    
                    seen.remove(i)
            return False

        return dfs(0,0,k)
```

