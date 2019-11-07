# Move Zeroes\(数组）

Given an array`nums`, write a function to move all`0`'s to the end of it while maintaining the relative order of the non-zero elements.

**Example:**

```text
Input:
[0,1,0,3,12]
Output:
[1,3,12,0,0]
```

**Note**:

1. You must do this

   **in-place**

   without making a copy of the array.

2. Minimize the total number of operations.

分析

冒泡排序做 遇到0就往后交换

```text
class Solution:
    def moveZeroes(self, nums):
        """
        :type nums: List[int]
        :rtype: void Do not return anything, modify nums in-place instead.
        """
        end = len(nums)-1
        for i,num in enumerate(nums):
            if not num:
                cur = i
                for j in range(cur,end+1):
                    if nums[j]:
                        nums[cur],nums[j] = nums[j],nums[cur]
                        cur = j
                end = cur
```

solution 2:

loop，把非零都装入nums, **insert**，J++。最后用0填充

```text
class Solution:
    def moveZeroes(self, nums):
        """
        :type nums: List[int]
        :rtype: void Do not return anything, modify nums in-place instead.
        """
        j = 0
        N = len(nums)
        for i in range(N):
            if nums[i]:
                nums[j] = nums[i]
                j+=1
        for i in range(j,N):
            nums[i]=0
```

或者不填充，直接**交换**也行

```text
class Solution:
    def moveZeroes(self, nums):
        """
        :type nums: List[int]
        :rtype: void Do not return anything, modify nums in-place instead.
        """
        j = 0
        N = len(nums)
        for i in range(N):
            if nums[i]:
                nums[j],nums[i] = nums[i],nums[j]
                j+=1
```

