# 3Sum Smaller

Given an array of n integers nums and a target, find the number of index triplets `i, j, k` with `0 <= i < j < k < n` that satisfy the condition `nums[i] + nums[j] + nums[k] < target`.

**Example:**

```text
Input: nums = [-2,0,1,3], and target = 2
Output: 2 
Explanation: Because there are two triplets which sums are less than 2:
             [-2,0,1]
             [-2,0,3]
```

分析

这里没有去重

符合条件的时候，直接count += end-start 而不是 count += 1

```text
class Solution:
    def threeSumSmaller(self, nums: List[int], target: int) -> int:
        res = 0
        l = len(nums)
        nums.sort()
        for i in range(l-2):
            #if i == 0 or nums[i] != nums[i-1]:
            tt,start,end = target - nums[i],i+1,l-1
            while start < end:
                if nums[start]+nums[end] < tt:
                    res += end-start
                    start += 1
                else:
                    end -= 1


        return res
```

