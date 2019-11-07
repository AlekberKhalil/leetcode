# Intersection of Two Arrays

Given two arrays, write a function to compute their intersection.

**Example 1:**

```text
Input: nums1 = [1,2,2,1], nums2 = [2,2]Output: [2]
```

**Example 2:**

```text
Input: nums1 = [4,9,5], nums2 = [9,4,9,8,4]Output: [9,4]
```

分析

还是用dictionary counter做，2个for

```text
import collectionsclass Solution:    def intersection(self, nums1, nums2):        """        :type nums1: List[int]        :type nums2: List[int]        :rtype: List[int]        """        if not nums1 or not nums2:            return []        ret =set()        map = collections.defaultdict(int)        for i in nums1:            map[i]+=1        for i in nums2:            if map[i]>0:                ret.add(i)        return list(ret)
```

