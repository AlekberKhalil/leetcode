# Backpack X\(多重背包）

You have a total of`n`yuan. Merchant has three merchandises and their prices are 150 yuan, 250 yuan and 350 yuan. And the number of these merchandises can be considered as infinite. After the purchase of goods need to be the remaining money to the businessman as a tip, finding`the minimum tip`for the merchant.

## Example

```text
Given: n = 900Return: 0
```

多重背包p2

```text
class Solution:    """    @param n: the money you have    @return: the minimum money you have to give    """    def backPackX(self, n):        # write your code here        f = [0]*(n+1)        values = [150,250,350]        for i in range(3):            for j in range(values[i], n+1):                f[j] = max(f[j],f[j-values[i]]+values[i])        return n - f[-1]
```

