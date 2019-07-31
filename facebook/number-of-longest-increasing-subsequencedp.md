# Number of Longest Increasing Subsequence\(dp\)

Given an unsorted array of integers, find the number of longest increasing subsequence.

**Example 1:**

```text
Input:
 [1,3,5,4,7]

Output:
 2

Explanation:
 The two longest increasing subsequence are [1, 3, 4, 7] and [1, 3, 5, 7].
```

**Example 2:**

```text
Input:
 [2,2,2,2,2]

Output:
 5

Explanation:
 The length of longest continuous increasing subsequence is 1, and there are 5 subsequences' length is 1, so output 5.
```

**Note:**Length of the given array will be not exceed 2000 and the answer is guaranteed to be fit in 32-bit signed int.

分析

2个dp， 一个length的dp， 一个count的dp

```text
length[i]=max(length[j]+1,length[i])
```

cnt\[i\]以i为底长度为x的所有cnt都相加`if len[i] = len[j] + 1: cnt[i] += cnt[j]`除非将来有长度更长的len覆盖，否则cnt\[i\]得到所有该长度的cnt

```text
class Solution:
    def findNumberOfLIS(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        if not nums:
            return 0
        n = len(nums)
        dp, cnt = [1] * n, [1] * n
        for i in range(1,n):
            for j in range(i):
                if nums[i] > nums[j]:
                    if dp[i] == dp[j]:
                        dp[i] =dp[j] + 1
                        cnt[i] = cnt[j]
                    elif dp[i] == dp[j] + 1:
                        cnt[i] += cnt[j]
        maxLen = max(dp)           
        return sum(cnt[i] for i in range(n) if dp[i] == maxLen)
```

