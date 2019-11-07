# Add Binary\(bit.iter,recur\)

Given two binary strings, return their sum \(also a binary string\).

The input strings are both**non-empty**and contains only characters`1`or `0`.

**Example 1:**

```text
Input: a = "11", b = "1"Output: "100"
```

**Example 2:**

```text
Input: a = "1010", b = "1011"Output: "10101"
```

分析

2个数组倒着相加，while i&gt;=0 or j&gt;=0:

模仿十进制这里，i%2 和i//2

```text
class Solution(object):    def addBinary(self, a, b):        """        :type a: str        :type b: str        :rtype: str        """        i = len(a)-1        j = len(b)-1        c = 0        res=''        while i>=0 or j>=0:                        if i >=0:                c += int(a[i])                i -=1            if j>=0:                c+=int(b[j])                j-=1            res=str(c%2)+res            c = c//2        if c > 0:            res = str(c)+res        return res
```

recursive

```text
class Solution(object):    def addBinary(self, a, b):        """        :type a: str        :type b: str        :rtype: str        """        if not a:return b        if not b:return a        if int(a[-1])+int(b[-1])== 2:            return self.addBinary(self.addBinary(a[:-1],b[:-1]),'1')+'0'        elif int(a[-1])+int(b[-1])==1:            return self.addBinary(a[:-1], b[:-1]) + '1'        else:            return self.addBinary(a[:-1], b[:-1]) + '0'
```

