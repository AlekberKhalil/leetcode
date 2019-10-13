# Balanced Sales Array



Given has an array of sales numbers, what is the index of the smallest index element for which the sums of all elements to the left and to the right are equal. The array may not be reordered.  
For example, given the array sales = \[1, 2, 3, 4, 6\],we see that 1+2+3=6，Using zero based indexing,sales\[3\] = 4 is the value sought.The index is 3.

#### Example

```text
Example:
Input : [1, 2, 3, 4, 6]
Output : 3
```

#### Notice

* 3 &lt;= n &lt;= 10^5
* 1 &lt;= sales\[i\] &lt;= 2\*10^4,where 0 &lt;= i&lt;n
* It is guaranteed that a solution always exists

分析

左右presum，然后loop 比较左右sum。 right要reverse 2次，算的时候和用的时候

```text
class Solution:
    """
    @param sales: a integer array
    @return: return a Integer
    """
    import itertools
    def BalancedSalesArray(self, sales):
        # write your code here
        left,right = [],[]
        leftsum = rightsum = 0
        n = len(sales)
        for i in range(n):
            leftsum += sales[i] 
            left.append(leftsum)
            rightsum += sales[n-1-i]
            right.append(rightsum)
            

        n = len(sales)
        for i in range(n):
            if left[i] == right[n-1-i]:
                return i 
        return -1
        
        
    
```

