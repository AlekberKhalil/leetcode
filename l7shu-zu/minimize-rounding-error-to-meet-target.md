# Minimize Rounding Error to Meet Target

Given an array of prices`[p1,p2...,pn]`and a`target`, round each price`pi`to`Roundi(pi)`so that the rounded array`[Round1(p1),Round2(p2)...,Roundn(pn)]`sums to the given`target`. Each operation`Roundi(pi)`could be either`Floor(pi)`or`Ceil(pi)`.

Return the string`"-1"`if the rounded array is impossible to sum to`target`. Otherwise, return the smallest rounding error, which is defined as Σ \|Roundi\(pi\) - \(pi\)\| forifrom 1 ton, as a string with three places after the decimal.

**Example 1:**

```text
Input: prices = ["0.700","2.800","4.900"], target = 8Output: "1.000"Explanation: Use Floor, Ceil and Ceil operations to get (0.7 - 0) + (3 - 2.8) + (5 - 4.9) = 0.7 + 0.2 + 0.1 = 1.0 .
```

**Example 2:**

```text
Input: prices = ["1.500","2.500","3.500"], target = 10Output: "-1"Explanation: It is impossible to meet the target.
```

**Note:**

1. `1`

   `<`

   `= prices.length`

   `<`

   `= 500`

   .

2. Each string of prices

   `prices[i]`

   represents a real number which is between 0 and 1000 and has exactly 3 decimal places.

3. `target`

   is between 0 and 1000000.

分析

int和floor差不多，也是切头，3 = 3.000 True

这里算出max和min，中间差的就是floor或者ceil。 max-target就是多出来的，需要floor的数字。

记住map和filter都要变List

format用法：**"{:.3f}".format\(res\)**

```text
from math import ceil,floorclass Solution:    def minimizeError(self, prices: List[str], target: int) -> str:        prices = list(map(float,prices))        lg,sm = int(sum(map(ceil,prices))),sum(map(int,prices))        if not sm<=target<=lg:            return "-1"        m = lg-target        prices = list(filter(lambda x: x!=int(x),prices))        prices.sort(key = lambda x: (x-int(x)))        res = sum(x-int(x) for x in prices[:m]) + sum(ceil(x)-x for x in prices[m:])        return "{:.3f}".format(res)
```

