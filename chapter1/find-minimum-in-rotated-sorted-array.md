# Find Minimum in Rotated Sorted Array

题目：

Suppose a sorted array is rotated at some pivot unknown to you beforehand.

\(i.e., 0 1 2 4 5 6 7 might become 4 5 6 7 0 1 2\).

Find the minimum element.

分析：

Finde minimum比search target简单的多，因为分类的时候就2种情况。A\[mid\]在上面和A\[mid\]在下面。

解法：

```text
    public int findMin(int[] nums) {

        // write your code here
      //找第一个<=最后一个数的数，画图可知第一个小于最后数的就是最小数
      if(nums.length == 0)
        return -1;

    int s = 0, e = nums.length - 1;
    int target = nums[e];

    while(s + 1 < e){
        int m = s + (e - s)/2;
        if(nums[m] <= target){
            e = m;
        }else{
            s = m;
        }
    }

    if(nums[s] <= target)
        return nums[s];

    return nums[e];//错了，返回了s和e

    }
```

