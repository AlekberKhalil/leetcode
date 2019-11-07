# First Position of Target

For a given sorted array \(ascending order\) and a`target`number, find the first index of this number in`O(log n)`time complexity.

If the target number does not exist in the array, return`-1`.

**Example**

If the array is`[1, 2, 3, 3, 4, 5, 10]`, for given target`3`, return`2`.

分析

二分，注意二分内移动的是end，所以可以找第一个

答案

```text
class Solution {    /**     * @param nums: The integer array.     * @param target: Target to find.     * @return: The first position of target. Position starts from 0.     */    public int binarySearch(int[] nums, int target) {        //write your code here        if(nums.length == 0)            return -1;        int s = 0;        int e = nums.length-1;        int m;        while(s+1 < e){            m = s + (e - s)/2;            if(nums[m] >= target)                e = m;            else                s = m;        }        if(nums[s] == target)            return s;        if(nums[e] == target)            return e;            return -1;    }}
```

