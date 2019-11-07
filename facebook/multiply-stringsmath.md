# Multiply Strings\(math\)

Given two non-negative integers`num1`and`num2`represented as strings, return the product of`num1`and`num2`, also represented as a string.

**Example 1:**

```text
Input:
 num1 = "2", num2 = "3"

Output:
 "6"
```

**Example 2:**

```text
Input:
 num1 = "123", num2 = "456"

Output:
 "56088"
```

**Note:**

```text
The length of both num1 and num2 is < 110.
Both num1 and num2 contain only digits 0-9.
Both num1 and num2 do not contain any leading zero, except the number 0 itself.
You must not use any built-in BigInteger library or convert the inputs to integer directly.
```

分析

也可把num1 num2换成数字后直接相乘

```text
class Solution:
    def multiply(self, num1, num2):
        """
        :type num1: str
        :type num2: str
        :rtype: str
        """
        n1 = len(num1)-1
        n2 = len(num2)-1
        sum = 0
        kk = 0
        for i in range(n1,-1,-1):
            subsum = 0
            k = 0
            for j in range(n2,-1,-1):
                subsum += (int(num1[i])*int(num2[j])) * 10**k
                k+=1
            sum += subsum * 10**kk
            kk+=1
        return str(sum)
```

