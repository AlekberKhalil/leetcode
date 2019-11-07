# Maximum Swap

Given a non-negative integer, you could swap two digits**at most**once to get the maximum valued number. Return the maximum valued number you could get.

**Example 1:**

```text
Input:
 2736

Output:
 7236

Explanation:
 Swap the number 2 and the number 7.
```

**Example 2:**

```text
Input:
 9973

Output:
 9973

Explanation:
 No swap.
```

**Note:**

1. The given number is in the range \[0, 108\]

分析

排序数组和原数组比较 第一个小于sort的就是需要交换的。记得从右边起找到第一个换，同时要break

最左的小数和最右的大数交换

```text
class Solution:
    def maximumSwap(self,num):
        """
        :type num: int
        :rtype: int
        """
        nums = list(map(int, str(num)))
        sorted_nums = sorted(nums, reverse=True)
        n = len(nums)
        for i in range(n):
            if nums[i] < sorted_nums[i]:
                idx = n - 1 - nums[::-1].index(sorted_nums[i])
                nums[idx], nums[i] = nums[i], nums[idx]
                break;
        return int(''.join(map(str, nums)))
```

