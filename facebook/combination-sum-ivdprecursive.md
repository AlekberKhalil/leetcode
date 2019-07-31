# Combination Sum IV\(dp,recursive\)

Given an integer array with all positive numbers and no duplicates, find the number of possible combinations that add up to a positive integer target.

**Example:**

```text
nums
 = [1, 2, 3]

target
 = 4

The possible combination ways are:
(1, 1, 1, 1)
(1, 1, 2)
(1, 2, 1)
(1, 3)
(2, 1, 1)
(2, 2)
(3, 1)

Note that different sequences are counted as different combinations.

Therefore the output is 
7
.
```

**Follow up:**  
What if negative numbers are allowed in the given array?  
How does it change the problem?  
What limitation we need to add to the question to allow negative numbers?

分析

背包问题，不懂为什么不是多重背包而是分组

```text
class Solution:
    def combinationSum4(self, nums, target):
        """
        :type nums: List[int]
        :type target: int
        :rtype: int
        """
        n = len(nums)
        f = [0]*(target + 1)
        f[0]=1

        for j in range(1,target+1):
            for num in nums:
                if j >= num:
                    f[j] += f[j-num]
        return f[target]
```

recursive 有for loop!!!!!!!

因为是可以重复，所以for loop从0开始

```text
class Solution:

    def combinationSum4(self, nums, target):
        """
        :type nums: List[int]
        :type target: int
        :rtype: int
        """
        cache = {}
        return self.helper(nums,target,cache)


    def helper(self,nums,target,cache): 
        if target in cache:
            return cache.get(target)
        if target == 0:
            return 1 
        elif target < 0:
            return 0

        cnt = 0
        for num in nums:
            cnt += self.helper(nums,target - num,cache)
        cache[target] = cnt
        return cnt
```

