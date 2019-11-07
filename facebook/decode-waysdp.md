# Decode Ways\(dp\)

A message containing letters from`A-Z`is being encoded to numbers using the following mapping:

```text
'A' -> 1'B' -> 2...'Z' -> 26
```

Given a**non-empty**string containing only digits, determine the total number of ways to decode it.

**Example 1:**

```text
Input: "12"Output: 2Explanation: It could be decoded as "AB" (1 2) or "L" (12).
```

**Example 2:**

```text
Input: "226"Output: 3Explanation: It could be decoded as "BZ" (2 26), "VF" (22 6), or "BBF" (2 2 6).
```

分析

从i-1或者i-2到达当前I

记得判断&gt;0 和&gt;9 and &lt;=26 还有01的情况

[https://leetcode.com/problems/decode-ways/discuss/187032/Java-DP%3A-memoization-top-down-and-bottom-up](https://leetcode.com/problems/decode-ways/discuss/187032/Java-DP%3A-memoization-top-down-and-bottom-up)

和2 的区别：当前dp\[i-1\]到dp\[i\] 1 就一个str，等于是 dp\[i-1\]\*1

对于2 中间好几种str，所以是dp\[i-1\]\*count\(str\)

```text
class Solution(object):    def numDecodings(self, s):        """        :type s: str        :rtype: int        """        n = len(s)        f = [0]*(n+1)        f[0] = 1        f[1] = 1 if int(s[0])> 0 else 0        for i in range(2,n+1):            if int(s[i-1])> 0:                f[i] = f[i-1]            x = int(s[i-2:i])            if s[i-2]!='0' and x >=10 and x<=26:                f[i]+=f[i-2]        return f[n]
```

```text
class Solution:    def numDecodings(self, s):        """        :type s: str        :rtype: int        """        if not s or s[0]=='0':#处理'0’的情况            return 0        n = len(s)        f = [0]*n        f[0]=1        for i in range(1,n):            num1 = int(s[i])            num2 = int(s[i-1:i+1])            if num1 > 0:                f[i]+=f[i-1]            if num2>9 and num2<27:                f[i]+=f[i-2] if i-2>=0 else 1# 第一个数的时候        return f[n-1]
```

