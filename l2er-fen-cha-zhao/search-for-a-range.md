# Search for a Range

Given an array of integers sorted in ascending order, find the starting and ending position of a given target value.

Your algorithm's runtime complexity must be in the order ofO\(logn\).

If the target is not found in the array, return`[-1, -1]`.

For example,  
Given`[5, 7, 7, 8, 8, 10]`and target value 8,  
return`[3, 4]`.

分析

[二分range](https://algorithm.yuanbin.me/zh-hans/basics_algorithm/binary_search.html)

[https://algorithm.yuanbin.me/zh-hans/basics\_algorithm/binary\_search.html](https://algorithm.yuanbin.me/zh-hans/basics_algorithm/binary_search.html)

两次二分。当寻找第一次target出现位置的循环中，

`array[mid] == target`

表示， target可以出现在mid或者mid更前的位置， 所以将ed移动到mid。当循环跳出时， st的位置在ed之前，所以先判断在st位置上是否是target， 再判断ed位置。 其实一句话概括就是左边界肯定先找左边start，右边界肯定先找右边end

当寻找最后一次target出现位置的循环中，

`array[mid] == target`

表示， target可以出现在mid或者mid之后的位置， 所以将st移动到mid。

return new int\[\]{left, right};

答案

```text
class Solution {
    public int[] searchRange(int[] nums, int target) {
        if(nums == null || nums.length == 0){
            return new int[]{-1, -1};
        }
        int s = 0, e = nums.length - 1, left = 0, right = e;

        while(s + 1 < e){
            int m = s + (e - s)/2;
            if(nums[m] < target){
                s = m;
            }else{
                e = m;
            }
        }

        if(nums[s] == target){
            left = s;
        }else if(nums[e] == target){
            left = e;
        }else{
            return new int[]{-1, -1};
        }


        s  = 0 ; e = nums.length - 1;
        while(s + 1 < e){
            int m = s + (e - s)/2;
            if(nums[m] <= target){
                s = m;
            }else{
                e = m;
            }
        }

        if(nums[e] == target){
            right = e;
        }else if(nums[s] == target){
            right = s;
        }else{
            return new int[]{-1, -1};
        }

        return new int[]{left, right};
    }
}
```

