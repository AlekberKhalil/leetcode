# Number Complement



Given a positive integer, output its complement number. The complement strategy is to flip the bits of its binary representation.

**Note:**  


1. The given integer is guaranteed to fit within the range of a 32-bit signed integer.
2. You could assume no leading zero bit in the integer’s binary representation.

**Example 1:**  


```text
Input: 5Output: 2Explanation: The binary representation of 5 is 101 (no leading zero bits), and its complement is 010. So you need to output 2.
```

**Example 2:**  


```text
Input: 1Output: 0Explanation: The binary representation of 1 is 1 (no leading zero bits), and its complement is 0. So you need to output 0.
```

分析

1^num = num所有位相反，找到第一个 》num的数-1,都是11111。。。。

```text
class Solution:    def findComplement(self, num: int) -> int:        i = 1        while i <= num:            i<<=1        return num^(i-1)        
```

