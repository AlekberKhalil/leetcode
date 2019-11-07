# Maximum Size Subarray Sum Equals k

Given an arraynumsand a target valuek, find the maximum length of a subarray that sums tok. If there isn't one, return 0 instead.

**Note:**  
The sum of the entirenumsarray is guaranteed to fit within the 32-bit signed integer range.

**Example 1:**

```text
Input: nums = [1, -1, 5, -2, 3], k = 3Output: 4 Explanation: The subarray [1, -1, 5, -2] sums to 3 and is the longest.
```

**Example 2:**

```text
Input: nums = [-2, -1, 2, 1], k = 1Output: 2 Explanation: The subarray [-1, 2] sums to 1 and is the longest.
```

**Follow Up:**  
Can you do it in O\(n\) time?

分析

不用subsum数组，直接cursum+map，一遍loop,第一次遇到sum加入，后来的就算subsum == k。

注意这里subsum不含头，所以res=j-i就行，不用+1

```text
class Solution:    def maxSubArrayLen(self, nums: List[int], k: int) -> int:        sm = 0         mm = {}        res = 0        for i,v in enumerate(nums):            sm += v            if sm == k:                res = i+1            elif sm - k in mm:                res = max(res,i - mm[sm - k]) #subsum不包含起始的Index，所以这里不用加1            if sm not in mm: mm[sm] = i        return res
```

