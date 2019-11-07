# Pow\(x, n\)\(recursive, iterative\)

Implement[pow\(_x_,_n_\)](http://www.cplusplus.com/reference/valarray/pow/), which calculates _x\_raised to the power\_n_\(xn\).

**Example 1:**

```text
Input: 2.00000, 10Output: 1024.00000
```

**Example 2:**

```text
Input: 2.10000, 3Output: 9.26100
```

**Example 3:**

```text
Input: 2.00000, -2Output: 0.25000Explanation: 2-2 = 1/22 = 1/4 = 0.25
```

分析

iterative

N = 9 = 2^3 + 2^0 = 1001 in binary. Then:

x^9 = x^\(2^3\) \* x^\(2^0\)

We can see that every time we encounter a 1 in the binary representation of N, we need to multiply the answer with x^\(2^i\) where**i**is the**ith**bit of the exponent. Thus, we can keep a running total of repeatedly squaring x - \(x, x^2, x^4, x^8, etc\) and multiply it by the answer when we see a 1.

```text
class Solution:    def myPow(self, x, n):        """        :type x: float        :type n: int        :rtype: float        """        # if n == 0:        #     return 1        if n < 0:            x = 1 / x        ans = 1        m = abs(n)        while m > 0:            if m&1 == 1:                ans *= x            m>>=1            x*=x        return ans
```

recursive

```text
class Solution:    def myPow(self, x, n):        """        :type x: float        :type n: int        :rtype: float        """        if n < 0:            return 1/self.myPow(x,-n)        if n == 0:            return 1        res = self.myPow(x,n//2)        if n%2 == 0:            return res*res        return res*res*x
```

