# Find the Duplicate Number

Given an arraynumscontainingn+ 1 integers where each integer is between 1 andn\(inclusive\), prove that at least one duplicate number must exist. Assume that there is only one duplicate number, find the duplicate one.

**Example 1:**

```text
Input:[1,3,4,2,2]Output: 2
```

**Example 2:**

```text
Input: [3,1,3,4,2]Output: 3
```

**Note:**

```text
Note:You must not modify the array (assume the array is read only).You must use only constant, O(1) extra space.Your runtime complexity should be less than O(n2).There is only one duplicate number in the array, but it could be repeated more than once.
```

二分法

```text
At first the search space is numbers between 1 to n. Each time I select a number mid (which is the one in the middle) and count all the numbers equal to or less than mid. Then if the count is more than mid, the search space will be [1 mid] otherwise [mid+1 n]. I do this until search space is only one number.
```

```text
class Solution:    def findDuplicate(self, nums: List[int]) -> int:        l = len(nums)        start, end = 1, l-1        while start < end:            mid = start + (end - start)//2            cnt = 0            for i in nums:                if i <= mid:                    cnt += 1            if cnt > mid:                end = mid            else:                start = mid + 1        return start
```

快慢指针

```text
For this example, [2 5 1 1 4 3]Let's point all elements to their corresponding indice. 2 points to index 1 which is number 5. 5 points to index 4 which is number 4. 1 points to index 0 which is number 2. 1 points to index 0 which is number 2. 4 points to index 3 which is number 1. 3 points to index 2 which is number 1.Draw this on a paper and you will find 2 -> 5 -> 4 -> 1 -> 2 which shapes a circle.Hopes this helps.
```

```text
class Solution:    def findDuplicate(self, nums: List[int]) -> int:        l = len(nums)        slow,quick=nums[0],nums[nums[0]]        while slow!= quick:            slow = nums[slow]            quick = nums[nums[quick]]        slow = 0        while slow!=quick:            slow = nums[slow]            quick = nums[quick]        return slow
```

