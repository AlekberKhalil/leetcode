# Wiggle Subsequence

A sequence of numbers is called a**wiggle sequence**if the differences between successive numbers strictly alternate between positive and negative. The first difference \(if one exists\) may be either positive or negative. A sequence with fewer than two elements is trivially a wiggle sequence.

For example,`[1,7,4,9,2,5]`is a wiggle sequence because the differences`(6,-3,5,-7,3)`are alternately positive and negative. In contrast,`[1,4,7,2,5]`and`[1,7,4,5,5]`are not wiggle sequences, the first because its first two differences are positive and the second because its last difference is zero.

Given a sequence of integers, return the length of the **longest subsequence** that is a wiggle sequence. A subsequence is obtained by deleting some number of elements \(eventually, also zero\) from the original sequence, leaving the remaining elements in their original order.

**Example 1:**

```text
Input: [1,7,4,9,2,5]Output: 6Explanation:The entire sequence is a wiggle sequence.
```

**Example 2:**

```text
Input: [1,17,5,10,13,15,10,5,16,8]Output: 7Explanation: There are several subsequences that achieve this length. One is [1,17,10,13,10,16,8].
```

**Example 3:**

```text
Input: [1,2,3,4,5,6,7,8,9]Output: 2
```

**Follow up:**  
Can you do it in O\(n\) time?

分析

这个是求subarray :[https://app.gitbook.com/@nataliekung/s/ladder\_code/~/drafts/-LjvQZ\_jy6w0cY-GRkBq/primary/l4dong-tai-gui-hua/longest-turbulent-subarray](https://app.gitbook.com/@nataliekung/s/ladder_code/~/drafts/-LjvQZ_jy6w0cY-GRkBq/primary/l4dong-tai-gui-hua/longest-turbulent-subarray)

subarray时候 每次都要reset up / down/up&down\(==\)

2个状态升降 up and down，交替由对方得来

```text
if (nums[i] > nums[i-1]) u = b + 1;else if (nums[i] < nums[i-1]) b = u + 1;else 不变
```

```text
class Solution:    def wiggleMaxLength(self, nums: List[int]) -> int:        n = len(nums)        if n==0:            return n        up=down=1        for i in range(1,n):            if nums[i]>nums[i-1]:                up=down+1            elif nums[i]<nums[i-1]:                down= up+1        return max(up,down)
```

错位相减得到diff，然后diff错位相乘，计算&lt;0的总数

注意这里float\('nan'\)占位，zip2个数组可以长度不一。

```text
class Solution:    def wiggleMaxLength(self, nums: List[int]) -> int:        c = float('nan')        diffs = [a-b for a,b in zip([c]+nums,nums+[c]) if a-b]        return sum(not a*b>=0 for a,b in zip(diffs,diffs[1:]))
```

