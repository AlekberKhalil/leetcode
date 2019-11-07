# Merge Sorted Array

Given two sorted integer arrays_nums1\_and\_nums2_, merge\_nums2\_into\_nums1\_as one sorted array.

**Note:**

* The number of elements initialized in

  _nums1_

  and

  _nums2_

  are

  _m_

  and

  _n_

  respectively.

* You may assume that

  _nums1_

  has enough space \(size that is greater or equal to

  _m_

  +

  _n_

  \) to hold additional elements from

  _nums2_

  .

**Example:**

```text
Input:nums1 = [1,2,3,0,0,0], m = 3nums2 = [2,5,6],       n = 3Output: [1,2,2,3,5,6]
```

分析

尾部开始填充

3个while,开始while i&gt;=0 and j&gt;=0: 然后while i&gt;=0:和while j&gt;=0：

```text
class Solution:    def merge(self, nums1, m, nums2, n):        """        :type nums1: List[int]        :type m: int        :type nums2: List[int]        :type n: int        :rtype: void Do not return anything, modify nums1 in-place instead.        """        if not n:            return        i = m-1        j=n-1        k=m+n-1        while i>=0 and j>=0:            if nums1[i]<nums2[j]:                nums1[k] = nums2[j]                k-=1                j-=1            else:                nums1[k] = nums1[i]                k-=1                i-=1        while i>=0:            nums1[k] = nums1[i]            k -= 1            i -= 1        while j>=0:            nums1[k] = nums2[j]            k -= 1            j -= 1
```

