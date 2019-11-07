# Sort Colors\(双指针）

Given an array with\_n\_objects colored red, white or blue, sort them[**in-place**](https://en.wikipedia.org/wiki/In-place_algorithm)so that objects of the same color are adjacent, with the colors in the order red, white and blue.

Here, we will use the integers 0, 1, and 2 to represent the color red, white, and blue respectively.

**Note:** You are not suppose to use the library's sort function for this problem.

**Example:**

```text
Input:
 [2,0,2,1,1,0]

Output:
 [0,0,1,1,2,2]
```

**Follow up:**

* A rather straight forward solution is a two-pass algorithm using counting sort.

  First, iterate the array counting number of 0's, 1's, and 2's, then overwrite array with total number of 0's, then 1's and followed by 2's.

* Could you come up with a one-pass algorithm using only constant space?

分析

双指针

大的和后面换，小的和前面换。记得和小的一起走，大的不要走。因为小的前面已经排序可以过了。

right 是待定的位置，所以是i&lt;=right

left 都是&lt;=Mid （small and mid\)所以要同时前进,因为Mid情况也要++ 但是right不一定，可能换来的是small 需要继续判断

```text
# class Solution:
#     def sortColors(self, nums):
#         """
#         :type nums: List[int]
#         :rtype: void Do not return anything, modify nums in-place instead.
#         """
#         n = len(nums)
#         red,white,blue = 0,0,n-1
#         while white <= blue:
#             if nums[white] == 0:
#                 nums[white],nums[red] = nums[red],nums[white]
#                 white +=1
#                 red+=1
#             elif nums[white] ==1:
#                 white += 1
#             else:
#                 nums[white], nums[blue] = nums[blue], nums[white]
#                 # white += 1
#                 blue -= 1

class Solution:
    def sortColors(self, nums):
        """
        :type nums: List[int]
        :rtype: void Do not return anything, modify nums in-place instead.
        """
        n = len(nums)
        i,left, right = 0,0,n-1
        while i <= right:
            if nums[i] == 0:
                nums[left],nums[i]=nums[i],nums[left]
                left+=1
                i+=1
            elif nums[i] == 2:
                nums[right],nums[i]=nums[i],nums[right]
                right-=1
            else:
                i +=1
```

