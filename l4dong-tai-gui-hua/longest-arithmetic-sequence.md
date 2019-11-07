# Longest Arithmetic Sequence

Given an array`A`of integers, return the**length**of the longest arithmetic subsequence in`A`.

Recall that a\_subsequence\_of`A`is a list`A[i_1], A[i_2], ..., A[i_k]`with`0 <= i_1 < i_2 < ... < i_k <= A.length - 1`, and that a sequence`B` is\_arithmetic\_if`B[i+1] - B[i]`are all the same value \(for`0 <= i < B.length - 1`\).

**Example 1:**

```text
Input: 
[3,6,9,12]
Output: 
4
Explanation: 

The whole array is an arithmetic sequence with steps of length = 3.
```

**Example 2:**

```text
Input: 
[9,4,7,2,10]
Output: 
3
Explanation: 

The longest arithmetic subsequence is [4,7,10].
```

**Example 3:**

```text
Input: 
[20,1,15,3,10,5,8]
Output: 
4
Explanation: 

The longest arithmetic subsequence is [20,15,10,5].
```

**Note:**

```text
2 <= A.length <= 2000
0 <= A[i] <= 10000
```

分析

对比Length of Longest Fibonacci Subsequence，本题input&gt;1000， 双循环超时。

用dict的dp, 记载当前Index为尾数，该diff的最长长度，dp\[index\]\[diff\] = dp\[prev\]\[diff\]+1

本题dict用法， get\(\)可以返回默认值，不同于dict\[\]没Key会报错

dict的Key可以不用tuple, 直接Index,diff

```text
class Solution:

    def longestArithSeqLength(self, A: List[int]) -> int:
        n = len(A)
        res=1

        dp = {}
        for i in range(n):           
            for j in range(i+1,n):
                diff = A[j]-A[i]
                dp[j,diff] = dp.get((i,diff),1) + 1
                res = max(dp[j,diff],res)
        return res
```

