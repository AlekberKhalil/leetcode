# Continuous Subarray Sum（2 sum）

Given a list of**non-negative**numbers and a target**integer**k, write a function to check if the array has a continuous subarray of size at least 2 that sums up to the multiple of**k**, that is, sums up to n\*k where n is also an**integer**.

**Example 1:**

```text
Input: [23, 2, 4, 6, 7],  k=6Output: TrueExplanation: Because [2, 4] is a continuous subarray of size 2 and sums up to 6.
```

**Example 2:**

```text
Input: [23, 2, 6, 4, 7],  k=6Output: TrueExplanation: Because [23, 2, 6, 4, 7] is an continuous subarray of size 5 and sums up to 42.
```

**Note:**

1. The length of the array won't exceed 10,000.
2. You may assume the sum of all the numbers is in the range of a signed 32-bit integer.

分析

2个loop做法：这里presum\[j\] - presum\[i\] 包括j 不包括i,根据题意这里j-i&gt;=2才行。 所以Presum计算的时候坐标后移一位。

一个loop：其实这里还是2 sum问题。x = presum % k，如果X再次出现，直接隔得就是multiple of k。corner是k=0

还是Index直接相减，留尾去头。i-j&gt;=2

自己版本：2个loop

```text
class Solution:    def checkSubarraySum(self, nums, k):        """        :type nums: List[int]        :type k: int        :rtype: bool        """        preSum = list(itertools.accumulate(nums))        n = len(nums)        if n< 2: return False        if n == 2: return preSum[1] == k or (k != 0 and preSum[1] % k == 0)        if k != 0 and preSum[-1] %k == 0:            return True        for i in range(n):            for j in range(n)[i:]:                subSum = preSum[j] - preSum[i]                if j - i >= 2 and (subSum == k or (k != 0 and subSum % k == 0)):                    return True        return False
```

2个loop：map的坐标后移一位。补充{0:0} 这样d\[2\]-d\[0\]就是2个数至少

```text
class Solution:    def checkSubarraySum(self, nums, k):        """        :type nums: List[int]        :type k: int        :rtype: bool        """        sum,d = 0,{0:0}        for i,e in enumerate(nums):            sum += e            d[i+1] = sum        n = len(nums)        for i in range(0,n-1):            for j in range(i+2,n+1):                subsum = d[j]-d[i]                if subsum == k or (k != 0 and subsum % k == 0):                    return True        return False
```

1个loop

```text
class Solution:    def checkSubarraySum(self, nums, k):        n= len(nums)        if k == 0:            return n >= 2 and sum(nums) == 0        summ, d = 0, {0: -1}        for i, v in enumerate(nums):            summ = (summ + v) % k            if summ in d:                if i - d[summ] >= 2:                    return True            else:                d[summ] = i        return False
```

