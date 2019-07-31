# Product of Array Except Self\(array\)

Given an array`nums`of_n\_integers where\_n_&gt; 1, return an array`output`such that`output[i]`is equal to the product of all the elements of`nums`except`nums[i]`.

**Example:**

```text
Input:
[1,2,3,4]
Output:
[24,12,8,6]
```

**Note:**Please solve it**without division**and in O\(_n_\).

**Follow up:**  
Could you solve it with constant space complexity? \(The output array**does not**count as extra space for the purpose of space complexity analysis.\)

分析

left 和right需要错位2 left -&gt; 1,a1,a2,a3...an-2 right-&gt;a2,a3,...an-1,1这样 a1=a0\*a2

注意zip 和list里2个for 的区别，前者对齐操作，后者就是2个loop交叉

```text
import itertools


class Solution:
    def productExceptSelf(self, nums):
        """
        :type nums: List[int]
        :rtype: List[int]
        """
        n=len(nums)
        left=list(itertools.accumulate([1]+nums[:n-1],lambda a,b:a*b))
        right = list(itertools.accumulate(reversed(nums[1:]+[1]),lambda a,b:a*b))
        return [a*b for a,b in zip(left,reversed(right))]
```

左边右边同时累积乘，记得不包含当前数

左边相当于切尾，右边相当于切头

```text
import itertools


class Solution:
    def productExceptSelf(self, nums):
        """
        :type nums: List[int]
        :rtype: List[int]
        """
        n = len(nums)
        ret=[1]*n
        left = right=1
        for i in range(n):
            ret[i]*=left
            ret[n-1-i]*=right
            left*=nums[i]
            right*=nums[n-1-i]
        return ret
```

