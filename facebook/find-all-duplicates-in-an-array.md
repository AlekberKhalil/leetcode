# Find All Duplicates in an Array

Given an array of integers, 1 ≤ a\[i\] ≤n\(n= size of array\), some elements appear**twice**and others appear**once**.

Find all the elements that appear**twice**in this array.

Could you do it without extra space and in O\(n\) runtime?

**Example:**

```text
Input:[4,3,2,7,8,2,3,1]Output:[2,3]
```

分析

有a\[i\]，把index=a\[i\]-1那个位置的数置为1

```text
class Solution:    def findDuplicates(self, nums):        """        :type nums: List[int]        :rtype: List[int]        """        ret = []        n = len(nums)        if n<=1:            return ret        for i in range(n):            index =  abs(nums[i])-1            if nums[index]<0:                ret.append(index+1)            nums[index] = -nums[index]        return ret
```

当前数换到val-1的位置上，所以数是1-&gt;n 位置是0-&gt;n-1

```text
class Solution:    def findDuplicates(self, nums):        """        :type nums: List[int]        :rtype: List[int]        """        ret = []        n = len(nums)        if n<=1:            return ret        i = 0        while i<n:        #换到i这个位置的新数字位置很可能也不对，需要继续换到i这个位置数到应有的位置为止            while nums[nums[i]-1] != nums[i]:                nums[nums[i]-1],nums[i] = nums[i],nums[nums[i]-1]                       i+=1         #数不在自己该有的位置，占了别人的位置，多余了。           for j in range(n):            if j+1!=nums[j]:                ret.append(nums[j])        return ret
```

