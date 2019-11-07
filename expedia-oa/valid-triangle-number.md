# Valid Triangle Number



Given an array consists of non-negative integers, your task is to count the number of triplets chosen from the array that can make triangles if we take them as side lengths of a triangle.

#### Example

**Example 1:**

```text
Input: [2,2,3,4]
Output: 3
Explanation:
Valid combinations are: 
2,3,4 (using the first 2)
2,3,4 (using the second 2)
2,2,3.
```

**Example 2:**

```text
Input: [3,3,3]
Output: 1
Explanation: 
Valid combination is 3,3,3.
```

#### Notice

1. The length of the given array won't exceed `1000`.
2. The integers in the given array are in the range of `[0, 1000]`.

分析

3sum，当前i是最大，left,right在0-i-1之间，只需要判断a+b&gt;c

```text
class Solution:
    """
    @param nums: the given array
    @return:  the number of triplets chosen from the array that can make triangles
    """
    def triangleNumber(self, nums):
        # Write your code here
        n = len(nums)
        res = 0
        nums.sort()
        for i in range(n-1,1,-1):
            l,r =0,i-1
            while l < r:
                if nums[l] + nums[r] > nums[i]:
                    res += r-l
                    r-=1
                else:
                    l+=1
        return res
                    
            
                
                
            

```

