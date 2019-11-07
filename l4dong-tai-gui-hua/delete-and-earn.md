# Delete and Earn

Given an array`nums`of integers, you can perform operations on the array.

In each operation, you pick any`nums[i]`and delete it to earn`nums[i]`points. After, you must delete**every**element equal to`nums[i] - 1`or`nums[i] + 1`.

You start with 0 points. Return the maximum number of points you can earn by applying such operations.

**Example 1:**

```text
Input: nums = [3, 4, 2]Output: 6Explanation:Delete 4 to earn 4 points, consequently 3 is also deleted.Then, delete 2 to earn 2 points. 6 total points are earned.
```

**Example 2:**

```text
Input: nums = [2, 2, 3, 3, 3, 4]Output: 9Explanation:Delete 3 to earn 3 points, deleting both 2's and the 4.Then, delete 3 again to earn 3 points, and 3 again to earn 3 points.9 total points are earned.
```

**Note:**

* The length of

  `nums`

  is at most

  `20000`

  .

* Each element

  `nums[i]`

  is an integer in the range

  `[1, 10000]`

  .

分析

类似house rober，从前两天的得到今天,python可以同时赋值2天的。

区别是这里数字都当做点，arr的Index对应该数，里面的值是该数的总和，比如3个5，就是arr\[5\] = 5\*3 = 15

对待每个点，和House rober的每个数字一样。也是不能取相邻的，只能取前两天较大。

```text
class Solution:    def deleteAndEarn(self, nums: List[int]) -> int:        prev,cur,cnt = 0,0,collections.Counter(nums)        for i in range(1,10003):            prev, cur = cur, max(prev+i*cnt[i],cur)        return cur
```

