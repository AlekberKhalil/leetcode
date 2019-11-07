# Recover Rotated Sorted Array

题目：

Given a **rotated** sorted array, recover it to sorted array in-place.

**Example**

`[4, 5, 1, 2, 3]`-&gt;`[1, 2, 3, 4, 5]`

分析：

三步翻转法可以实现rotated

1.recover rotated sorted array

45 123 找到这个位置没必要二分，直接N过来· -&gt;54 321-&gt; 123 45

解法：

```text
    public void recoverRotatedSortedArray(List<Integer> nums) {

        int pos = -1;
        for(int i = 0; i < nums.size()-1; i++){
            if(nums.get(i) > nums.get(i+1)){
                pos = i;
                break;
            }
        }
        reverse(nums, 0, pos);
        reverse(nums, pos+1, nums.size()-1);
        reverse(nums, 0, nums.size()-1);
    }

    public void reverse(List<Integer> nums, int start, int end){
        while(start < end){
            int temp = nums.get(start);
            nums.set(start++, nums.get(end));// arraylist set用法
            nums.set(end--, temp);
        }
    }
```

