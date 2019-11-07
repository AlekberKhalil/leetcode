# Find All Duplicates in an Array

Given an array of integers, 1 ≤ a\[i\] ≤ n \(n = size of array\), some elements appear twice and others appear once.

Find all the elements that appear twice in this array.

#### Example

**Example1**

```text
Input:[4,3,2,7,8,2,3,1]Output:[2,3]
```

**Example2**

```text
Input:[10,2,5,10,9,1,1,4,3,7]Output:[1,10]
```

#### Challenge

Could you do it without extra space and in O\(n\) runtime?

分析

把当前数abs\(x\)-1作为Index, nums\[index\]  flop. 如果当前数字已经是负数，说明index+1已经出现过

```text
class Solution:    """    @param nums: a list of integers    @return: return a list of integers    """    def findDuplicates(self, nums):        # write your code here        res = []        for x in nums:            idx = abs(x)-1            if nums[idx]< 0:                res.append(idx + 1)            else:                nums[idx] *= -1        return res                        
```

