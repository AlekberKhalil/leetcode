# Subarrays with K Different Integers

Given an array`A`of positive integers, call a \(contiguous, not necessarily distinct\) subarray of`A`\_good\_if the number of different integers in that subarray is exactly`K`.

\(For example,`[1,2,3,1,2]`has`3`different integers:`1`,`2`, and`3`.\)

Return the number of good subarrays of`A`.

**Example 1:**

```text
Input: A = [1,2,1,2,3], K = 2Output: 7Explanation: Subarrays formed with exactly 2 different integers: [1,2], [2,1], [1,2], [2,3], [1,2,1], [2,1,2], [1,2,1,2].
```

**Example 2:**

```text
Input: A = [1,2,1,3,4], K = 3Output: 3Explanation: Subarrays formed with exactly 3 different integers: [1,2,1,3], [2,1,3], [1,3,4].
```

```text
Note:1 <= A.length <= 200001 <= A[i] <= A.length1 <= K <= A.length
```

分析

1用atmost K做，f\(exactly K\) = f\(atMost K\) - f\(atMost K-1\).

```text
class Solution:    def subarraysWithKDistinct(self, A: List[int], K: int) -> int:                  return self.atMostK(A,K)-self.atMostK(A,K-1)    def atMostK(self, A: List[int], K: int) -> int:            res = cnt = s = e = 0            mm = collections.defaultdict(int)            ll = len(A)            for s in range(ll):                  e = s                mm = collections.defaultdict(int)                while e < ll:                                    if mm[A[e]] == 0:                        cnt += 1                    mm[A[e]] += 1                    e += 1                    while cnt > K:                        if mm[A[s]] == 1:                            cnt -= 1                        mm[A[s]] -= 1                        s += 1                    res += e - s                return res
```

2

```text
If the subarray [j, i] contains K unique numbers, and first prefix numbers also appear in [j + prefix, i] subarray, we have total 1 + prefix good subarrays. For example, there are 3 unique numers in [1, 2, 1, 2, 3]. First two numbers also appear in the remaining subarray [1, 2, 3], so we have 1 + 2 good subarrays: [1, 2, 1, 2, 3], [2, 1, 2, 3] and [1, 2, 3].
```

count = distinct char.

while 让l,r之间始终都是distinct，同时用Pre++表示重复的数字，结果就是pre+1

count &gt;K 时候左边缩一位（k-1）,重置pre=0

```text
class Solution:    def subarraysWithKDistinct(self, A: List[int], K: int) -> int:          res = l = r = cnt = 0        ll = len(A)        mm = collections.defaultdict(int)        pre = 0        while r < ll:            if mm[A[r]] == 0:                cnt += 1            mm[A[r]] +=1            r+=1            if cnt > K:                mm[A[l]] -= 1                l += 1                cnt -= 1                pre = 0            while mm[A[l]] > 1:                pre += 1                mm[A[l]] -= 1                l += 1            if cnt == K:                res += pre + 1        return res
```

