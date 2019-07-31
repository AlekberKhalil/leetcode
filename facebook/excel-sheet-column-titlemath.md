# Excel Sheet Column Title（math\)

Given a positive integer, return its corresponding column title as appear in an Excel sheet.

For example:

```text
  1 -> A
    2 -> B
    3 -> C
    ...
    26 -> Z
    27 -> AA
    28 -> AB 
    ...
```

**Example 1:**

```text
Input:
 1

Output:
 "A"
```

**Example 2:**

```text
Input:
 28

Output:
 "AB"
```

**Example 3:**

```text
Input:
 701

Output:
 "ZY"
```

分析

就是模拟十进制数，个位数%，十位数/，注意这里是n-1，不是N

python ord 和 chr

```text
class Solution(object):
    def convertToTitle(self, n):
        """
        :type n: int
        :rtype: str
        """
        s = ''
        while n>0:
            rem = (n-1)%26
            s=chr(ord('A')+rem)+s #想象 A+25 =Z 所以要n-1
            n=(n-1)/26
        return s
```

分治

每次递归结果+最低位的char

```text
class Solution(object):
    def convertToTitle(self, n):
        """
        :type n: int
        :rtype: str
        """
        return "" if n==0 else self.convertToTitle((n-1)/26)+chr((n-1)%26+ord('A'))
```

