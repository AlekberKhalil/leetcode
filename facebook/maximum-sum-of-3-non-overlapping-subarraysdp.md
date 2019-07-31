# Maximum Sum of 3 Non-Overlapping Subarrays\(dp\)

In a given array`nums`of positive integers, find three non-overlapping subarrays with maximum sum.

Each subarray will be of size`k`, and we want to maximize the sum of all`3*k`entries.

Return the result as a list of indices representing the starting position of each interval \(0-indexed\). If there are multiple answers, return the lexicographically smallest one.

**Example:**

```text
Input: [1,2,1,2,6,7,5,1], 2
Output: [0, 3, 5]
Explanation: Subarrays [1, 2], [2, 6], [7, 5] correspond to the starting indices [0, 3, 5].
We could have also taken [2, 1], but an answer of [1, 3, 5] would be lexicographically larger.
```

**Note:**

```text
nums.length will be between 1 and 20000.
nums[i] will be between 1 and 65535.
k will be between 1 and floor(nums.length / 3).
```

分析

dp\[3个group\]\[以哪个数字为底\]

```text
class Solution:
    def maxSumOfThreeSubarrays(self, nums, k):
        """
        :type nums: List[int]
        :type k: int
        :rtype: List[int]
        """
        n, m = len(nums), 3
        dp = [[0] * (n + 1) for _ in range(m + 1)]
        path = [[0] * (n + 1) for _ in range(m + 1)]
        preSum = [0] * (n + 1)

        s = 0
        for i in range(1, n + 1):
            s += nums[i - 1]
            preSum[i] = s


        for i in range(1, m+1):
            for j in range(k, n+1):
                include = dp[i - 1][j - k] + preSum[j] - preSum[j - k] if j - k >= 0 else prefixSum[j]
                exclude = dp[i][j - 1]

                if include > exclude:
                    dp[i][j] = include
                    path[i][j] = j - k //这里j已经是index+1了 所以不是j-k+1
                else:
                    dp[i][j] = exclude
                    path[i][j] = path[i][j - 1]


        ret = [None] * 3
        ret[2] = path[3][-1] #3group以n结尾的
        ret[1] = path[2][ret[2]] #2个group以ret[2]结尾，ret[2] 就是第三个group起始位置，2group到那里已经终结
        ret[0] = path[1][ret[1]]#1个group 以ret[1]结尾

        return ret
```

