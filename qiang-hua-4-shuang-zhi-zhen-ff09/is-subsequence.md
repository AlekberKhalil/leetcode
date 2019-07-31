# Is Subsequence

Given a string**s**and a string**t**, check if**s**is subsequence of**t**.

You may assume that there is only lower case English letters in both**s**and**t**.**t**is potentially a very long \(length ~= 500,000\) string, and**s**is a short string \(&lt;=100\).

A subsequence of a string is a new string which is formed from the original string by deleting some \(can be none\) of the characters without disturbing the relative positions of the remaining characters. \(ie,`"ace"`is a subsequence of`"abcde"`while`"aec"`is not\).

**Example 1:**  
**s**=`"abc"`,**t**=`"ahbgdc"`

Return`true`.

**Example 2:**  
**s**=`"axc"`,**t**=`"ahbgdc"`

Return`false`.

**Follow up:**  
If there are lots of incoming S, say S1, S2, ... , Sk where k &gt;= 1B, and you want to check one by one to see if T has its subsequence. In this scenario, how would you change your code?

分析

2个指针，一样的时候一起动，否则长动短不动

```text
class Solution:
    def isSubsequence(self, s, t):
        """
        :type s: str
        :type t: str
        :rtype: bool
        """
        p1=p2=0
        n1 = len(s)
        n2 = len(t)
        if n2<n1:
            return False
        while p1 < n1 and p2 < n2:
            if s[p1] == t[p2]:
                p1 +=1
                p2 +=1
            else:
                p2 += 1
        if p1 == n1:
            return True
        return False
```

