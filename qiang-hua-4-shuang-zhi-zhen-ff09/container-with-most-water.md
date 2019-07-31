# Container With Most Water

Given n non-negative integers a1, a2, ..., an, where each represents a point at coordinate`(i, ai)`._n\_vertical lines are drawn such that the two endpoints of line\_i\_is at`(i, ai)`and`(i, 0)`. Find two lines, which together with\_x_-axis forms a container, such that the container contains the most water.

## Notice

You may not slant the container.

**Example**

Given`[1,3,2]`, the max area of the container is`2`.

分析：

对撞双指针，哪边高度高就固定哪边，短板的那端移动。

答案

```text
public class Solution {
    /*
     * @param heights: a vector of integers
     * @return: an integer
     */
    public int maxArea(int[] heights) {
        // write your code here
        int n = heights.length;
        int start = 0, end = n-1;
        int area = 0;
        while(start < end){
            if(heights[end] > heights[start]){
                area = Math.max(area, heights[start] * (end - start));
                start ++;
            }
            else{
                area = Math.max(area, heights[end] * (end - start));
                end --;
            }
        }
        return area;
    }
}
```

