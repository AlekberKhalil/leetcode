# Integer Break

Given a positive integern, break it into the sum of**at least**two positive integers and maximize the product of those integers. Return the maximum product you can get.

**Example 1:**

```text
Input: 
2
Output: 
1
Explanation: 
2 = 1 + 1, 1 × 1 = 1.
```

**Example 2:**

```text
Input: 
10
Output: 
36
Explanation: 
10 = 3 + 3 + 4, 3 × 3 × 4 = 36.
```

**Note**: You may assume thatnis not less than 2 and not larger than 58.

分析

注意这里，可能不拆比拆更好，所以要加入max\(j,p\[j\]\)比较

```text
class Solution:
    def integerBreak(self, n: int) -> int:
        if not n:
            return n
        p = [float('-inf')] * (n+1)


        p[1] =1

        for i in range(2,n+1):
            for j in range(1,i):
                p[i] = max(p[i], max(j,p[j]) * max(p[i-j],(i - j))) #不拆可能比拆得到数更大

        return p[n]
```

