# Divide Two Integers\(math\)

The integer division should truncate toward zero.

**Example 1:**

```text
Input: dividend = 10, divisor = 3Output: 3
```

**Example 2:**

```text
Input: dividend = 7, divisor = -3Output: -2
```

**Note:**

```text
Both dividend and divisor will be 32-bit signed integers.The divisor will never be 0.Assume we are dealing with an environment which could only store integers within the 32-bit signed integer range: [−231,  231 − 1]. For the purpose of this problem, assume that your function returns 231 − 1 when the division result overflows.
```

分析

**先都abs,注意 Map**： p,q,i,ans =map\(abs,\(dividend, divisor,0,0\)\)

divident = divisor\*\(1+2+4+6+8.....\)

注意其实&lt;&lt; &gt;&gt;就是 \*2和//2。 ans = 1+2+4+6+8.....

```text
Algorithm for integer division of p/q, where p and q are positive:i, result = 0, 0 # Initialize stuff.while q << i <= p: i += 1 # Phase 1: Figure out how far left you should go.for j in reversed(range(i)): # Phase 2: Divide like a 7-year-old.    if q << j <= p:        p -= q << j        result += 1 << j
```

Time: O\(log\(answer\)\) = O\(log\(dividend // divisor\)\) = O\(log\(dividend\) - log\(divisor\)\)

Space: O\(1\)

**注意这里判断2个异号的方法 ：**

`(dividend<0)!=(divisor<0)`

```text
negative = (dividend < 0) ^ (divisor < 0)if negative:            r = ~r + 1
```

**还有就是int的取值**

```text
[-1<<31, 1<<31-1]
```

```text
class Solution:    def divide(self, dividend, divisor):        """        :type dividend: int        :type divisor: int        :rtype: int        """        p,q,i,ans =map(abs,(dividend, divisor,0,0))        while q<<i <= p:            i+=1        for j in reversed(range(i)):            if q<<j <= p:                p -= q<<j                ans+=1<<j        if (dividend<0)!=(divisor<0) or ans < -1<<31:            ans = -ans        return min(ans,(1<<31)-1)
```

