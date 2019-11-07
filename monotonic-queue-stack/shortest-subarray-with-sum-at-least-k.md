# Shortest Subarray with Sum at Least K



Return the **length** of the shortest, non-empty, contiguous subarray of `A` with sum at least `K`.

If there is no non-empty subarray with sum at least `K`, return `-1`.

1. 
**Example 1:**

```text
Input: A = [1], K = 1Output: 1
```

**Example 2:**

```text
Input: A = [1,2], K = 4Output: -1
```

**Example 3:**

```text
Input: A = [2,-1,2], K = 3Output: 3
```

**Note:**

1. `1 <= A.length <= 50000`
2. `-10 ^ 5 <= A[i] <= 10 ^ 5`
3. `1 <= K <= 10 ^ 9`



分析

单调递增栈。 找左边比右边小的，左边i比右边j大的无用，



```text
class Solution:    def shortestSubarray(self, A: List[int], K: int) -> int:        B = [0]        for i in A:            B.append(B[-1]+i)        s = []        res = float('inf')        for i,b in enumerate(B):            if not s:                s.append(i)            else:                while s and B[s[-1]] > b: s.pop() #useless, pop out                while s and B[s[0]] <= b - K:                     res = min(res,i - s[0])                    s.pop(0)                s.append(i)        return res if res!= float('inf') else -1                                                                
```

