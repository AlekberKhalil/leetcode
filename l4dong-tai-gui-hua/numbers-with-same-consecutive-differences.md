# Numbers With Same Consecutive Differences

Return all**non-negative**integers of length`N`such that the absolute difference between every two consecutive digits is`K`.

Note that**every**number in the answer**must not**have leading zeros**except**for the number`0`itself. For example,`01`has one leading zero and is invalid, but`0`is valid.

You may return the answer in any order.

**Example 1:**

```text
Input: N = 3, K = 7Output: [181,292,707,818,929]Explanation: Note that 070 is not a valid number, because it has leading zeroes.
```

**Example 2:**

```text
Input: N = 2, K = 1Output: [10,12,21,23,32,34,43,45,54,56,65,67,76,78,87,89,98]
```

```text
Note:1 <= N <= 90 <= K <= 9
```

分析

最后一个digit， lastdigit+k&lt;10 and lastdigit-k&gt;=0.不是用abs这里

```text
class Solution:    def numsSameConsecDiff(self, N, K):        """        :type N: int        :type K: int        :rtype: List[int]        """        cur = {i for i in range(10)}        for i in range(1,N):            temp = set()            for j in cur:                                lastdigit = j%10                                                    if j > 0 and lastdigit +K<10:                    temp.add(j*10+lastdigit +K)                 if j > 0 and lastdigit -K>=0:                    temp.add(j*10+lastdigit -K)                cur = temp        return list(cur)
```

简化版

```text
        cur = range(10)        for i in range(1,N):            cur = {i*10+y for i in cur for y in [i%10+K,i%10-K] if i and 0<=y<10}        return list(cur)
```

