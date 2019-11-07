# Decode Ways

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

二刷看注释

for 1：n

```text
class Solution:    def numDecodings(self, s):        """        :type s: str        :rtype: int        """        if not s or s[0] == '0':#是判断s[0]不是整个s，防止了'01'的情况            return 0        n = len(s)        f = [0] * n        f[0] = 1        for i in range(1,n):            if s[i] != '0':                f[i] += f[i - 1]            num = int(s[i-1:i+1])            if num > 9 and num < 27: #是>9不是>0啊，也是防止'01'                f[i] += f[i - 2] if i-2>=0 else 1 #i-2要判断，越界就+1        return f[n - 1]
```

