# Kth Largest Element in an Array\(快排）

Find the**k**th largest element in an unsorted array. Note that it is the kth largest element in the sorted order, not the kth distinct element.

**Example 1:**

```text
Input:
[3,2,1,5,6,4] 
and k = 2

Output:
 5
```

**Example 2:**

```text
Input:
[3,2,3,1,2,4,5,5,6] 
and k = 4

Output:
 4
```

**Note:**  
You may assume k is always valid, 1 ≤ k ≤ array's length.

分析

heapq的nlargest是返回N前N大而且倒序

```text
class Solution:
    def findKthLargest(self, nums, k):
        """
        :type nums: List[int]
        :type k: int
        :rtype: int
        """
        heapq.heapify(nums)
        return heapq.nlargest(k,nums)[-1]
```

用快排做

注意partition if start==end:

```text
        return nums\[start\] 可以没有。
```

```text
class Solution:
    def findKthLargest(self, nums, k):
        """
        :type nums: List[int]
        :type k: int
        :rtype: int
        """
        if not nums:
            return -1

        ll=len(nums)
        return self.partition(nums,ll-k,0,ll-1)

    def partition(self,nums,k,start,end):
        if start==end:
            return nums[start]
        pivot,left,right = nums[start],start,end
        while left < right:
            while left<right and nums[right]>=pivot:
                right-=1
            nums[left]=nums[right]
            while left<right and nums[left]<=pivot:
                left+=1
            nums[right]=nums[left]
        nums[left] = pivot
        if left == k:
            return nums[left]
        if left > k:
            return self.partition(nums,k,start,left-1)
        else:
            return self.partition(nums, k, left+1, end)
```

