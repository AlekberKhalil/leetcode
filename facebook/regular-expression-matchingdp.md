# Regular Expression Matching（DP）

Given an input string \(`s`\) and a pattern \(`p`\), implement regular expression matching with support for`'.'`and`'*'`.

```text
'.' Matches any single character.'*' Matches zero or more of the preceding element.
```

The matching should cover the**entire**input string \(not partial\).

**Note:**

* `s`

   could be empty and contains only lowercase letters

  `a-z`

  .

* `p`

  could be empty and contains only lowercase letters

  `a-z`

  , and characters like 

  `.`

   or 

  `*`

  .

**Example 1:**

```text
Input:s = "aa"p = "a"Output: falseExplanation: "a" does not match the entire string "aa".
```

**Example 2:**

```text
Input:s = "aa"p = "a*"Output: trueExplanation: '*' means zero or more of the precedeng element, 'a'. Therefore, by repeating 'a' once, it becomes "aa".
```

**Example 3:**

```text
Input:s = "ab"p = ".*"Output: trueExplanation: ".*" means "zero or more (*) of any character (.)".
```

**Example 4:**

```text
Input:s = "aab"p = "c*a*b"Output: trueExplanation: c can be repeated 0 times, a can be repeated 1 time. Therefore it matches "aab".
```

**Example 5:**

```text
Input:s = "mississippi"p = "mis*is*p*."Output: false
```

分析

1可以顺序等得话 f\[i\]\[j\] = f\[i-1\]\[j-1\]

2不能的话需要\*

a.把a\*当做空串：f\[0\]\[j\] = f\[0\]\[j-2\]

b. 让s最后的字符有保障之后：if s\[i-1\] == p\[j-2\] or p\[j-2\] == '.' 让P匹配好s前面所有的：f\[i\]\[j\] = f\[i-1\]\[j\]

dp

```text
class Solution:    def isMatch(self, s, p):        """        :type s: str        :type p: str        :rtype: bool        """        sl = len(s)        pl = len(p)        f = [[False]*(pl+1) for _ in range(sl+1)]        f[0][0] = True        for j in range(1,pl+1):            if p[j-1] == '*':                f[0][j] = f[0][j-2]        for i in range(1,sl+1):            for j in range(1,pl+1):                if s[i-1] == p[j-1] or p[j-1] == '.':                    f[i][j] = f[i-1][j-1]                elif p[j-1] == '*':                    if f[i][j-2]:                        f[i][j] = True                    elif s[i-1] == p[j-2] or p[j-2] == '.':                        f[i][j] = f[i-1][j]        return f[sl][pl]
```

recursive

```text
class Solution:    def isMatch(self, s, p):        """        :type s: str        :type p: str        :rtype: bool        """        if not s and not p:            return True        return self.helper(s,p,len(s)-1, len(p)-1) #倒着来    def helper(self,s,p,i,j):        if i==-1 and j==-1: #相当于i==pos            return True        if j<0:#这里有查j所以下面只要查i            return i<0        if p[j] == '*':            return i>=0 and (s[i]==p[j-1] or p[j-1]=='.') and self.helper(s,p,i-1,j) or self.helper(s,p,i,j-2) #前面i-1所以要查i，后面直接I所以不用        else:            return i >= 0 and (s[i] == p[j] or p[j] == '.') and self.helper(s, p, i - 1, j-1)#前面i-1所以要查i
```

