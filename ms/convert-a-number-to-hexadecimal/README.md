# Convert a Number to Hexadecimal



Given an integer, write an algorithm to convert it to hexadecimal. For negative integer, [two’s complement](https://en.wikipedia.org/wiki/Two%27s_complement) method is used.

**Note:**

1. All letters in hexadecimal \(`a-f`\) must be in lowercase.
2. The hexadecimal string must not contain extra leading `0`s. If the number is zero, it is represented by a single zero character `'0'`; otherwise, the first character in the hexadecimal string will not be the zero character.
3. The given number is guaranteed to fit within the range of a 32-bit signed integer.
4. You **must not use any method provided by the library** which converts/formats the number to hex directly.

**Example 1:**

```text
Input:
26

Output:
"1a"
```

**Example 2:**

```text
Input:
-1

Output:
"ffffffff"
```

分析

32位的数字，4位4位的来，共8次。每次最后4位 &1111b （&15）

记得结果去掉开头0，因为8位的原因加的

```text
class Solution:
    def toHex(self, num: int) -> str:
        if num == 0:
            return'0'
        elif num < 0:
            num += 2**32
        mp = '0123456789abcdef' 
        res = ''
        for i in range(8):
            n = num & 15
            res = mp[n] + res
            num= num >> 4
            
        return res.lstrip('0')
            
        
```





