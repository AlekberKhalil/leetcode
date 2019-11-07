# Binary Subarrays With Sum

n an array`A`of`0`s and`1`s, how many**non-empty**subarrays have sum`S`?

**Example 1:**

```text
Input: A = [1,0,1,0,1], S = 2Output: 4Explanation: The 4 subarrays are bolded below:[1,0,1,0,1][1,0,1,0,1][1,0,1,0,1][1,0,1,0,1]
```

**Note:**

```text
A.length <= 300000 <= S <= A.lengthA[i] is either 0 or 1.
```

分析

用presum,一个map存sum:count, 每次+= map（cursum-target）

map初始0:1 因为要考虑sum=target的情况

2指针没做出来

```text
class Solution:    def numSubarraysWithSum(self, A: List[int], S: int) -> int:        mm = {0:1}#要包含正好相等的情况        res = ss = 0        for i in A:            ss += i            if ss-S in mm:                res += mm[ss-S]            mm[ss] = mm[ss] + 1 if ss in mm else 1        return res#         res = count = s = e =0#         ll = len(A)#         while e < ll:#             if A[e] == 1:#                 count += 1#             e+= 1#             while count == S and s < e:#                 res += 1#                 if A[s] == 1:#                     count -= 1#                 s += 1#         return res
```

