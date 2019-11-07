# Contiguous Array\(2 sum\)

Given a binary array, find the maximum length of a contiguous subarray with equal number of 0 and 1.

**Example 1:**

```text
Input: [0,1]Output: 2Explanation: [0, 1] is the longest contiguous subarray with equal number of 0 and 1.
```

**Example 2:**

```text
Input: [0,1,0]Output: 2Explanation: [0, 1] (or [1, 0]) is a longest contiguous subarray with equal number of 0 and 1.
```

**Note:**The length of the given binary array will not exceed 50,000.

分析

two sum的变种

count ++ if 1 count--if 0. count 0，1. map存 count: index，初始{0，-1} 此处-1是Index，为了后面计算正确。可用{0，1}验证

这里ret直接index j-i, 比如{1，0，1} 。因为一样sum又出现，说明中间的array accumulated sum=0 此时尾含头不含，正好j-i。

```text
class Solution(object):    def findMaxLength(self, nums):        """        :type nums: List[int]        :rtype: int        """        ret, sum2idx, count = 0, {0: -1}, 0        for i, v in enumerate(nums):            count += -1 if v == 0 else 1            if count in sum2idx:                ret = max(ret, i - sum2idx[count])            else:                sum2idx[count] = i        return ret
```

