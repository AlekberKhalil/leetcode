# Minimum Size Subarray Sum\(追击指针）

Given an array of**n**positive integers and a positive integer**s**, find the minimal length of a**contiguous**subarray of which the sum ≥**s**. If there isn't one, return 0 instead.

**Example:** 

```text
Input:s = 7, nums = [2,3,1,2,4,3]Output: 2Explanation: the subarray [4,3] has the minimal length under the problem constraint.
```

分析

窗口类前向追击指针，注意这里sum &lt; s要放在while里判断。防止j已经取过了头才退出。先判断再加J

```text
class Solution:    def minSubArrayLen(self, s, nums):        """        :type s: int        :type nums: List[int]        :rtype: int        """        if not nums:            return 0        n = len(nums)        minLen =  n+1        i = j = sum = 0        for i in range(n):            while j < n and sum < s:                sum += nums[j]                j+=1            if sum >= s:                minLen = min(minLen,j-i)            sum-=nums[i]        if minLen == n + 1:            return 0        return minLen
```

