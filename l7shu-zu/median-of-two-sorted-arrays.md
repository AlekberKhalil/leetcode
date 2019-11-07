# Median of Two Sorted Arrays

There are two sorted arrays**nums1**and**nums2**of size m and n respectively.

Find the median of the two sorted arrays. The overall run time complexity should be O\(log \(m+n\)\).

**Example 1:**

```text
nums1 = [1, 3]nums2 = [2]The median is 2.0
```

**Example 2:**

```text
nums1 = [1, 2]nums2 = [3, 4]The median is (2 + 3)/2 = 2.5
```

分析

本质是利用二分法，中间的数字比较，然后丢一半。

比较a\[k/2\] b\[k/2\] 哪个小就不要前半段，把该数组的start移动，同时k-k/2

特殊情况：

* a没数了， b没数了， 取剩下的数
* ab里只剩一个数了，取小的
* 数组不足k/2，设置为max。这样可以取另一个数组里的数。

medium所以K存在，否则K判断k是否比俩加起来都大

递归里的参数都在变，有极端情况

```text
class Solution {    public double findMedianSortedArrays(int[] nums1, int[] nums2) {        int m = nums1.length;        int n = nums2.length;        int total = m + n;        //取中位数，记住判断奇偶        if(total % 2 == 0){            return (findMedian(nums1, nums2, 0, 0, total/2) + findMedian(nums1, nums2, 0, 0, total/2 + 1)) / 2;        }else{            return findMedian(nums1, nums2, 0, 0, total/2 + 1);        }    }    public double findMedian(int[] nums1, int[] nums2, int s1, int s2, int k){        //a或者b没数了，取剩下的数。        if(s1 >= nums1.length)            return nums2[s2 + k - 1];        if(s2 >= nums2.length)            return nums1[s1 + k - 1];        //ab里只剩一个数了，取小的        if(k == 1)            return Math.min(nums1[s1], nums2[s2]);        //要判断a[k/2] b[k/2] k/2是否过界，过界就用Max代替！！！！！！！        //数组不足k/2，设置为max。这样可以取另一个数组里的数。下一轮递归K变小了，可能又能继续了。        int key1 = s1 + k / 2 - 1 < nums1.length                    ? nums1[s1 + k / 2 - 1]                    : Integer.MAX_VALUE;        int key2 = s2 + k / 2 - 1 < nums2.length                    ? nums2[s2 + k / 2 - 1]                    : Integer.MAX_VALUE;        if(key1 < key2){            return findMedian(nums1, nums2, s1 + k / 2, s2, k - k / 2);        }else{            return findMedian(nums1, nums2, s1, s2 + k / 2, k - k / 2);        }    }}
```

python

记得helper递归时候，要移动到下一位，不是留在中位。

```text
class Solution:    def findMedianSortedArrays(self, nums1: List[int], nums2: List[int]) -> float:        n1 = len(nums1)        n2 = len(nums2)        n = n1+n2        def helper(x,y,xs,ys,k):            if xs >= n1:                return y[ys+k-1]            if ys >= n2:                return x[xs+k-1]            if k == 1:                return min(x[xs] ,y[ys])            xm = x[xs + int(k/2) - 1] if xs + k//2 - 1< n1 else float('inf')            ym = y[ys + int(k/2) - 1] if ys + k//2 - 1< n2 else float('inf')            if xm < ym:                return helper(x,y,xs + int(k/2), ys, k - int(k/2))#记得要从中位数往后移一位，所以不是xs + int(k/2) - 1            else:                return helper(x,y,xs, ys + int(k/2),k - int(k/2))                                                    if n % 2 == 0:            return (helper(nums1,nums2, 0,0,int(n/2)) + helper(nums1, nums2,0,0,int(n/2)+1))/2        else:            return helper(nums1,nums2, 0,0,int(n/2)+1)                                        
```

