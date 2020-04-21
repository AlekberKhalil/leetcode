# Happy number



Write an algorithm to determine if a number `n` is "happy".

A happy number is a number defined by the following process: Starting with any positive integer, replace the number by the sum of the squares of its digits, and repeat the process until the number equals 1 \(where it will stay\), or it **loops endlessly in a cycle** which does not include 1. Those numbers for which this process **ends in 1** are happy numbers.

Return True if `n` is a happy number, and False if not.

**Example:** 

```text
Input: 19
Output: true
Explanation: 
12 + 92 = 82
82 + 22 = 68
62 + 82 = 100
12 + 02 + 02 = 1
```

分析

数字如果重复出现，则不必再计算，可以加入set 或者用快慢指针。

Python 没有do-while 用while true+break来实现快慢指针

```text
class Solution:
    def isHappy(self, n: int) -> bool:    
        def getSum(i):
            res = 0
            while i > 0:
                res+= (i%10)**2
                i //= 10
            return res
        
        slow=fast=n
        
        while True:              
            slow= getSum(slow)
            fast = getSum(fast)
            fast = getSum(fast)
            if fast == 1:
                return True
            if slow == fast:
                break
                       
                        
        return False
         
        
```



