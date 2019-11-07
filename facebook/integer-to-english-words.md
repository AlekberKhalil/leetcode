# Integer to English Words

Convert a non-negative integer to its english words representation. Given input is guaranteed to be less than 231- 1.

**Example 1:**

```text
Input:
 123

Output:
 "One Hundred Twenty Three"
```

**Example 2:**

```text
Input:
 12345

Output:
 "Twelve Thousand Three Hundred Forty Five"
```

**Example 3:**

```text
Input:
 1234567

Output:
 "One Million Two Hundred Thirty Four Thousand Five Hundred Sixty Seven"
```

**Example 4:**

```text
Input:
 1234567891

Output:
 "One Billion Two Hundred Thirty Four Million Five Hundred Sixty Seven Thousand Eight Hundred Ninety One"
```

分析

2段递归，forloop找到合适数以后，递归//和% ，中间+str\[\]。

注意前半段要IM\[100\]&gt;=100 只有这样的数才有 One hundred ,one million这样。

```text
self.helper(num // self.IM[i], index + 1) + [self.SM[i]] + self.helper(num%self.IM[i],index+1)
```

```text
class Solution:
    IM = [1000000000, 1000000, 1000, 100, 90, 80, 70, 60, 50, 40, 30, 20, 19, 18, 17, 16, 15, 14, 13, 12, 11, 10, 9, 8,
          7, 6, 5, 4, 3, 2, 1]
    SM = ["Billion", "Million", "Thousand", "Hundred", "Ninety", "Eighty", "Seventy", "Sixty", "Fifty", "Forty",
          "Thirty", "Twenty", "Nineteen", "Eighteen", "Seventeen", "Sixteen", "Fifteen", "Fourteen", "Thirteen",
          "Twelve", "Eleven", "Ten", "Nine", "Eight", "Seven", "Six", "Five", "Four", "Three", "Two", "One",""]

    def numberToWords(self, num):
        """
        :type num: int
        :rtype: str
        """

        if num == 0:
            return "Zero"

        return " ".join(self.helper(num,0))

    def helper(self,num,index):
        ret = []
        n = len(self.IM)

        for i in range(index,n):
            if num >= self.IM[i]:
                if self.IM[i] >= 100:
                    ret = self.helper(num // self.IM[i], index + 1) 
                ret += [self.SM[i]]+self.helper(num%self.IM[i],index+1)
                break
        return ret
```

