# Decode Ways II\(dp\)

A message containing letters from`A-Z`is being encoded to numbers using the following mapping way:

```text
'A' -> 1'B' -> 2...'Z' -> 26
```

Beyond that, now the encoded string can also contain the character '\*', which can be treated as one of the numbers from 1 to 9.

Given the encoded message containing digits and the character '\*', return the total number of ways to decode it.

Also, since the answer may be very large, you should return the output mod 109+ 7.

**Example 1:**

```text
Input: "*"Output: 9Explanation: The encoded message can be decoded to the string: "A", "B", "C", "D", "E", "F", "G", "H", "I".
```

**Example 2:**

```text
Input: "1*"Output: 9 + 9 = 18
```

**Note:**

1. The length of the input string will fit in range \[1, 10

   5

   \].

2. The input string will only contain the character '\*' and digits '0' - '9'.

分析

dp，前面一步（一个字母）来或者前面2步（2个字母合并）来。

数字判断\*和digit判断

```text
class Solution:    def decodeWay(self, s1, s2):        ret = 0        if s1 == '-':            if s2.isdigit() and 1 <=int(s2) <=9:                ret = 1            elif s2 == '*':                ret = 9        elif s1.isdigit() and 0 < int(s1) <= 2:            if s2.isdigit() and int(s1+s2) <= 26:                ret = 1            elif s2 == '*':                ret = 9 if int(s1) == 1 else 6        elif s1 == '*':            if s2.isdigit():               ret = 2 if  0<= int(s2) <=6 else 1            elif s2 == '*':                ret = 15        return ret    def numDecodings(self, s):        """        :type s: str        :rtype: int        """        if not s or len(s) == 0:            return 0        dp1 = dp2 = 1        MOD = 10 ** 9 + 7        lc = '-'        ret = 0        for i,c in enumerate(s):            if i == 0:                ret = self.decodeWay('-', c)            else:                ret = (self.decodeWay('-', c)*dp1 + dp2*self.decodeWay(lc,c))% MOD            lc = c            dp1, dp2 = ret,dp1        return ret
```

dp

```text
class Solution:    def numDecodings(self, s):        """        :type s: str        :rtype: int        """        if not s or s[0] == '0':            return 0        n = len(s)        p = 9 if s[0] == '*' else 1#0 if s[0]=='0' else 1        pp = 1        cur = 0        M = 10**9 + 7        for i in range(1,n):            if s[i] == '*':                cur = p*9# 因为不用数组用cur，所以每次赋新值，不是cur+=                if s[i-1] == '*':                    cur = (cur+pp*15)%M                else:                    num = int(s[i-1])                    if num <=2 and num >0:                       cur =(cur+pp * 9)%M if num == 1 else (cur+pp * 6)%M            else:                num1 = int(s[i])                cur = p if num1 > 0 else 0#每次cur一定要先赋值                if s[i-1] == '*':                    cur= (cur+pp*2)%M if num1 <=6 else (cur+pp)%M                else:                    num2 = int(s[i-1:i+1])                    if num2 < 27 and num2 >9:                       cur = (cur+pp)%M            p,pp = cur,p        return p#p=cur，用cur n=1不行
```

