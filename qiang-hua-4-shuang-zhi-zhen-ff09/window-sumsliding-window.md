# Window Sum（sliding window\)

## Description

Given an array of n integers, and a moving window\(size k\), move the window at each iteration from the start of the array, find the`sum`of the element inside the window at each moving.

Have you met this question in a real interview?

Yes

Problem Correction

## Example

For array`[1,2,7,8,5]`, moving window size k =`3`.  
1 + 2 + 7 = 10  
2 + 7 + 8 = 17  
7 + 8 + 5 = 20  
return`[10,17,20]`

分析

还是loop len,然后count ++/--

```text
class Solution:    """    @param nums: a list of integers.    @param k: length of window.    @return: the sum of the element inside the window at each moving.    """    def winSum(self, nums, k):        # write your code here        sum  = 0        res = []        cnt = 0        nlen = len(nums)        for i in range(nlen):            sum += nums[i]            cnt += 1            if cnt > k:                sum -= nums[i - k]                cnt -= 1            if cnt == k:                res.append(sum)        return res
```

