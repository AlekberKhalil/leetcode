# Maximum Size Subarray Sum Equals k（2sum和Map\)

Given an array`nums`and a target value`k`, find the maximum length of a subarray that sums to k. If there isn't one, return 0 instead.

## Example

Given nums =`[1, -1, 5, -2, 3]`, k =`3`, return`4`.

```text
Explanation:
because the subarray [1, -1, 5, -2] sums to 3 and is the longest.
```

Given nums =`[-2, -1, 2, 1]`, k =`1`, return`2`.

```text
Explanation:
because the subarray [-1, 2] sums to 1 and is the longest.
```

分析

2sum问题，presum存在map里，Map初始值是{0,-1} 因为presum相减之后，前数剪没了不含，所以坐标前补一位

比如presum 5-3其实只包含4，5 正好和长度一样。5-3长度是2

```text
class Solution:
    """
    @param nums: an array
    @param k: a target value
    @return: the maximum length of a subarray that sums to k
    """
    def maxSubArrayLen(self, nums, k):
        # Write your code here
        presum = 0
        dict = {0:-1}
        ret = 0
        for i, num in enumerate(nums):
            presum += num
            if presum not in dict:
                dict[presum] = i
            if presum - k in dict:
                ret = max(i - dict[presum - k],ret)


        return ret
```

