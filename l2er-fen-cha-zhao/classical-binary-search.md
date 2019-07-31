# Classical Binary Search

Find any position of a target number in a sorted array. Return -1 if target does not exist.

**Example**

Given`[1, 2, 2, 4, 5, 5]`.

For target =`2`, return 1 or 2.

For target =`5`, return 4 or 5.

For target =`6`, return -1.

分析

binary search。记得判断Nums数组，还有不要把最后判断再写进while loop里了！

答案

```text
public int findPosition(int[] nums, int target) {
        if(nums == null || nums.length == 0){
            return -1;
        }
        int s = 0, e = nums.length - 1;

        while(s + 1 < e){
            int m = s + (e - s)/2;
            if(nums[m] < target){
                s = m;
            }else{
                e = m;
            }
        }

        if(nums[s] == target){
                return s;
            }
            if(nums[e] == target){
                return e;
            }
            return -1;
}
```

