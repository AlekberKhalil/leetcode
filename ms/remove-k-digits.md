# Remove K Digits



Given a non-negative integer num represented as a string, remove k digits from the number so that the new number is the smallest possible.

**Note:**  


* The length of num is less than 10002 and will be ≥ k.
* The given num does not contain any leading zero.

**Example 1:**

```text
Input: num = "1432219", k = 3
Output: "1219"
Explanation: Remove the three digits 4, 3, and 2 to form the new number 1219 which is the smallest.
```

**Example 2:**

```text
Input: num = "10200", k = 1
Output: "200"
Explanation: Remove the leading 1 and the number is 200. Note that the output must not contain leading zeroes.
```

**Example 3:**

```text
Input: num = "10", k = 2
Output: "0"
Explanation: Remove all the digits from the number and it is left with nothing which is 0.
```

分析

去掉峰值，for loop num，内loop while每次和栈顶元素比较，栈顶元素大就弹掉。

最后考虑1 k》0                s\[:-k or None\]

2 trim leading 0                       lstrip\('0'\) 

3 空str

```text
class Solution:
    def removeKdigits(self, num: str, k: int) -> str:
        s = []
        for d in num:
            while k and s and int(s[-1]) > int(d):
                k-=1
                s.pop()
            s.append(d)
            
        return ''.join(s[:-k or None]).lstrip('0') or '0'
            
                
            
        
```



