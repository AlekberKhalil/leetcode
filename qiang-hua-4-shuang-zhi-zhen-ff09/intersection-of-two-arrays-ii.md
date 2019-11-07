# Intersection of Two Arrays II

Given two arrays, write a function to compute their intersection.

**Example 1:**

```text
Input: 
nums1 = 
[1,2,2,1]
, nums2 = 
[2,2]
Output: 
[2,2]
```

**Example 2:**

```text
Input: 
nums1 = 
[4,9,5]
, nums2 = 
[9,4,9,8,4]
Output: 
[4,9]
```

**Note:**

* Each element in the result should appear as many times as it shows in both arrays.
* The result can be in any order.

分析

用counter intersection 或者双指针

```text
class Solution:
    def intersect(self, nums1: List[int], nums2: List[int]) -> List[int]:
        # a,b = map(collections.Counter,(nums1,nums2))
        # return list((a&b).elements())
        mm = collections.Counter(nums1)
        res = []
        for i in nums2:
            if i in mm and mm[i]>0:#记得这里光是In不够
                res.append(i)
                mm[i] -= 1
        return res
```

