# Count Numbers with Unique Digits

Given a**non-negative**integer n, count all numbers with unique digits, x, where 0 ≤ x &lt; 10n.

**Example:**

```text
Input: 2Output: 91 Explanation: The answer should be the total numbers in the range of 0 ≤ x <100, excluding 11,22,33,44,55,66,77,88,99
```

分析

就是从高位起loop每个位，每个往后的数，可选数字都只能少一个，排列组合思想

```text
class Solution:    def countNumbersWithUniqueDigits(self, n: int) -> int:        if n == 0:            return 1        res = 10        avail = uniq = 9        for i in range(2,n+1):            uniq = avail*uniq            res+= uniq            avail -=1        return res
```

