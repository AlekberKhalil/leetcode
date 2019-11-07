# Hamming Distance

The[Hamming distance](https://en.wikipedia.org/wiki/Hamming_distance)between two integers is the number of positions at which the corresponding bits are different.

Given two integers`x`and`y`, calculate the Hamming distance.

**Note:**  
0 ≤`x`,`y`&lt; 231.

**Example:**

```text
Input: x = 1, y = 4Output: 2Explanation:1   (0 0 0 1)4   (0 1 0 0)       ↑   ↑The above arrows point to positions where the corresponding bits are different.
```

分析

就是每次x,y位移然后 &1 ,然后2个^

也可以设置个m=1移动 像total hamming distance一样

```text
class Solution:    def hammingDistance(self, x, y):        """        :type x: int        :type y: int        :rtype: int        """        m = 1        maxx = max(x,y)        cnt = 0        while m <= maxx:            if (x&m) ^(y&m):                cnt += 1            m<<=1        return cntclass Solution:    def hammingDistance(self, x, y):        """        :type x: int        :type y: int        :rtype: int        """        cnt = 0        while x or y:            if (x&1) ^(y&1):                cnt +=1            x>>=1            y>>=1        return cnt
```

用Bin

```text
class Solution:    def hammingDistance(self, x, y):        """        :type x: int        :type y: int        :rtype: int        """        return (bin(x^y)).count('1')
```

