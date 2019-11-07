# Trapping Rain Water

Given\_n\_non-negative integers representing an elevation map where the width of each bar is`1`, compute how much water it is able to trap after raining.

![Trapping Rain Water](https://lintcode-media.s3.amazonaws.com/problem/rainwatertrap.png)

**Example**

Given`[0,1,0,2,1,0,1,3,2,1,2,1]`, return`6`.

分析：

左右两边定边界比较高度，哪边低从哪边开始，然后比较中间的。

然后顺序loop，cur低的话就累加入res，cur高的话作为标杆，更新标杆。

```text
public class Solution {
    /*
     * @param heights: a list of integers
     * @return: a integer
     */
    public int trapRainWater(int[] heights) {
        // write your code here
        int n = heights.length, ret = 0;
        int left = 0,right = n-1;
        if(left >= right)
            return ret;

        int leftHeight = heights[left];
        int rightHeight = heights[right];

        while(left < right){

            if(leftHeight < rightHeight){
                //左边
                left ++;
                if(leftHeight > heights[left]){
                    ret += leftHeight - heights[left];
                }else{
                    leftHeight = heights[left];
                }
            }else{
                right --;
                if(rightHeight > heights[right]){
                    ret += rightHeight - heights[right];
                }else{
                    rightHeight = heights[right];
                }
            }
        }
        return ret;
    }
}
```

