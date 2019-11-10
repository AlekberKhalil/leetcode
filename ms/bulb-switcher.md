# Bulb Switcher



There are n bulbs that are initially off. You first turn on all the bulbs. Then, you turn off every second bulb. On the third round, you toggle every third bulb \(turning on if it's off or turning off if it's on\). For the i-th round, you toggle every i bulb. For the n-th round, you only toggle the last bulb. Find how many bulbs are on after n rounds.

**Example:**

```text
Input: 3
Output: 1 
Explanation: 
At first, the three bulbs are [off, off, off].
After first round, the three bulbs are [on, on, on].
After second round, the three bulbs are [on, off, on].
After third round, the three bulbs are [on, off, off]. 

So you should return 1, because there is only one bulb is on.
```

分析

对于每个数，只有divisor个数是奇数才能是开。

每个数divisor都是成对出现，比如12： 2\*6，2个数字。 除了有平方根的数比如36： 6\*6。所以只要返回n的平方根。

```text
class Solution:
    def bulbSwitch(self, n: int) -> int:
        return int(math.sqrt(n))
            
        
                
        
                
                
        
```



