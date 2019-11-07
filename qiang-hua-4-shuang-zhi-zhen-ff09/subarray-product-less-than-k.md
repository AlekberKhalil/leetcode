# Subarray Product Less Than K

Your are given an array of positive integers`nums`.

Count and print the number of \(contiguous\) subarrays where the product of all the elements in the subarray is less than`k`.

**Example 1:**

```text
Input:
 nums = [10, 5, 2, 6], k = 100

Output:
 8

Explanation:
 The 8 subarrays that have product less than 100 are: [10], [5], [2], [6], [10, 5], [5, 2], [2, 6], [5, 2, 6].
Note that [10, 5, 2] is not included as the product of 100 is not strictly less than k.
```

**Note:**

```text
0 < nums.length <= 50000.
0 < nums[i] < 1000.
0 <= k < 10^6.
```

分析

每次right加入新数字，若&gt;=k，则while缩小Left直到valid

每次右边加入新数字，就会多出来x个new subarray，x = e-s window size

```text
for window (5, 2), when 6 is introduced, it add 3 new subarray: (5, (2, (6)))
        (6)
     (2, 6)
  (5, 2, 6)
```

```text
class Solution:
    def numSubarrayProductLessThanK(self, nums: List[int], k: int) -> int:
        s,e,l,p,res = 0,0,len(nums),1,0
        while e < l:
            p *= nums[e]
            e += 1
            while p >= k and s < e:                                
                p /= nums[s]
                s += 1
            res += e-s
        return res
```

