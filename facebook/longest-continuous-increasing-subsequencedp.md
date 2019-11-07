# Longest Continuous Increasing Subsequence\(dp\)

```text
Input:
```

```text
 [1,3,5,4,7]

Output:
 3

Explanation:
 The longest continuous increasing subsequence is [1,3,5], its length is 3. 
Even though [1,3,5,7] is also an increasing subsequence, it's not a continuous one where 5 and 7 are separated by 4.
```

**Example 2:**

```text
Input:
 [2,2,2,2,2]

Output:
 1

Explanation:
 The longest continuous increasing subsequence is [2], its length is 1.
```

**Note:**Length of the array will not exceed 10,000.

分析

dp\[\]或者直接dp，dp\[i\] = nums\[i-1\]&lt;nums\[i\]? dp\[i-1\] + 1: 1

注意python : if not nums

```text
class Solution:
    def findLengthOfLCIS(self, nums):
        """
        :type nums: List[int]
        :rtype: int

        """
        if not nums:
            return 0
        n = len(nums)

        dp = maxp = 1
        for i in range(1, n):
            dp = dp+1 if nums[i] > nums[i-1] else 1
            maxp = max(maxp,dp)

        return maxp
```

