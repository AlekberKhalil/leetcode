# String Compression



#### Description



Implement a method to perform basic string compression using the counts of repeated characters. For example, the string `aabcccccaaa` would become `a2b1c5a3`.

If the "compressed" string would not become smaller than the original string, your method should return the original string.

You can assume the string has only upper and lower case letters \(a-z\).Have you met this question in a real interview?  YesProblem Correction

#### Example

**Example 1:**

```text
Input: str = "aabcccccaaa"Output: "a2b1c5a3"
```

**Example 2:**

```text
Input: str = "aabbcc"Output: "aabbcc"
```

分析

遇到cur不同就压入list cur+str\(cnt\)。 最后比较结果和原数组哪个长

```text
class Solution:    """    @param originalString: a string    @return: a compressed string    """    def compress(self, originalString):        # write your code here        if not originalString:            return originalString        e = 1        cnt = 1        cur = originalString[0]        n = len(originalString)        res = []        for e in range(1,n):            if originalString[e] == cur:                cnt += 1            else:                res+=[cur,str(cnt)]                cur = originalString[e]                cnt = 1                                    res+=[cur,str(cnt)]        res = ''.join(res)        return res if len(res) < len(originalString) else originalString                        
```

