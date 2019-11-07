# Subarray Sums Divisible by K



Given an array `A` of integers, return the number of \(contiguous, non-empty\) subarrays that have a sum divisible by `K`.

**Example 1:**

```text
Input: A = [4,5,0,-2,-3,1], K = 5Output: 7Explanation: There are 7 subarrays with a sum divisible by K = 5:[4, 5, 0, -2, -3, 1], [5], [5, 0], [5, 0, -2, -3], [0], [0, -2, -3], [-2, -3]
```

**Note:**

1. `1 <= A.length <= 30000`
2. `-10000 <= A[i] <= 10000`
3. `2 <= K <= 10000`



分析

sum\(0,i\)%k = sum\(0,j\)%k, i+1-&gt;j之间可以被K整除。 这里注意先把当前cnt\[cur\] 加入res， 再increase cnt\[cur\] 因为每次当前Index只需要之前的数字，不是更新后数字

```text
class Solution:    def subarraysDivByK(self, A: List[int], K: int) -> int:        n = len(A)        mm = {}        mm[0] = 1        res = prefix = 0        for a in A:            prefix += a            rem = prefix%K            if rem in mm:                res += mm[rem]                mm[rem] +=1            else:                mm[rem] = 1        return res
```

