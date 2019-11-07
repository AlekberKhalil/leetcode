# Longest Consecutive Sequence\(math\)

Given an unsorted array of integers, find the length of the longest consecutive elements sequence.

Your algorithm should run in O\(_n_\) complexity.

**Example:**

```text
Input: [100, 4, 200, 1, 3, 2]Output: 4Explanation: The longest consecutive elements sequence is [1, 2, 3, 4]. Therefore its length is 4.
```

分析

if i-1 in set 这样保证只从连续数里最小的开始。

while i+1 in set有连续就一直加 然后max一下

```text
class Solution(object):    def longestConsecutive(self, nums):        """        :type nums: List[int]        :rtype: int        """        ss = set(nums)        mm = 0        for n in ss:            if n-1 not in ss:                ans = 1                cur = n                while cur+1 in ss:                    ans +=1                    cur+=1                mm = max(mm,ans)        return mm
```

