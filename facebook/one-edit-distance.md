# One Edit Distance

Given two strings S and T, determine if they are both one edit distance apart.

## Example

Given s =`"aDb"`, t =`"adb"`  
return`true`

分析

如果两个字符串长度相差1以上，返回false，选取两个字符串短的那个，一一对应每位比较两个字符串，如果遇到不相等的index位，

则比较两个字符串的a, b的index+1, index+1 位以后是否相等或者 index+1, index 是否相等，或者index, index+1是否相等。

如果前面全都相等，说明只有最后一位不相等，那就返回true

```text
class Solution:
    """
    @param s: a string
    @param t: a string
    @return: true if they are both one edit distance apart or false
    """
    def isOneEditDistance(self, s, t):
        # write your code here
        m = len(s)
        n = len(t)
        if abs(m - n) > 1:
            return False
        if s == t:
            return False
        if m<n:
            s,t,m,n = t,s,n,m #make sure s is always longer one
        i=0
        while i<n:
            if s[i] == t[i]:
                i+=1
            else:
                if s[i+1:]==t[i:] or s[i+1:]==t[i+1:]:#insert or delete or replace
                    return True
                return False
        return True
```

