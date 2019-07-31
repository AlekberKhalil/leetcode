# Increasing Triplet Subsequence\(二分得递增子序列）

Given an unsorted array return whether an increasing subsequence of length 3 exists or not in the array.

Formally the function should:

> Return true if there exists i, j, k such that arr\[i\] &lt; arr\[j\] &lt; arr\[k\] given 0 ≤ i &lt; j &lt; k ≤ n -1 else return false.

**Note:**Your algorithm should run in O\(n\) time complexity and O\(1\) space complexity.

**Example 1:**

```text
Input: 
[1,2,3,4,5]
Output: 
true
```

**Example 2:**

```text
Input: 
[5,4,3,2,1]
Output: 
false
```

分析：

注意这种方法，二分得到原数组的递增子序列

```text
class Solution(object):
    def increasingTriplet(self, nums):
        """
        :type nums: List[int]
        :rtype: bool
        """
        res = []
        for n in nums:
            index = bisect.bisect_left(res,n)  
            if index ==len(res):
                res.append(n)
            else: res[index] = n
            if index == 2:
                return True
        return False
```

