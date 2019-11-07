# Palindromic Substrings

Given a string, your task is to count how many palindromic substrings in this string.  
The substrings with different start indexes or end indexes are counted as different substrings even they consist of same characters.

#### Example

**Example1**

```text
Input: "abc"Output: 3Explanation:3 palindromic strings: "a", "b", "c".
```

**Example2**

```text
Input: "aba"Output: 4Explanation:4 palindromic strings: "a", "b", "a", "aba".
```

#### Notice

The input string length won't exceed 1000

分析

以中间2位向两边扩展，注意判断left, right 是在范围内

```text
class Solution:    """    @param str: s string    @return: return an integer, denote the number of the palindromic substrings    """    def countPalindromicSubstrings(self, str):        # write your code here        n = len(str)        def expand(i,j):            cnt = 0            while 0 <= i and j < n:                if str[i] != str[j]:                    break                i -= 1                 j += 1                cnt += 1            return cnt                    res = 0        for i in range(n):            res += expand(i,i)            res += expand(i,i+1)        return res
```

