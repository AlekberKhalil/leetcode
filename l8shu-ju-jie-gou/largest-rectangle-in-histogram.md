# Largest Rectangle in Histogram

Givennnon-negative integers representing the histogram's bar height where the width of each bar is 1, find the area of largest rectangle in the histogram.

![](https://leetcode.com/static/images/problemset/histogram.png)

Above is a histogram where width of each bar is 1, given height =`[2,1,5,6,2,3]`.

![](https://leetcode.com/static/images/problemset/histogram_area.png)

The largest rectangle is shown in the shaded area, which has area =`10`unit.

For example,  
Given heights =`[2,1,5,6,2,3]`,  
return`10`.

分析

感觉histogram就是左边高度一直往右维持到不能再维持。所以维护递增栈。

递增的栈，每次遇到比当前高的就压入，短的就开始不断弹出栈，并计算面积。直到遇到比它还短的，继续递增。

每次计算面积时候，算到左边第一个比它小的。比如6就是5， 2就是1.width = i - s.peek\(\) - 1

此处i是top下一个数，而s.peek（）就是第一个比它小的数。

最后加入高度为0，好让前面的元素出栈。比如123，一直递增没有递减无法出栈。加入0后直接width = i

int h = \(i == n ? 0 : heights\[i\]\);

heights\[temp\] \* \(**s.isEmpty\(\) ? i** : i - s.peek\(\) - 1\)

算中间有几条线段，可以直接i-j

```text
class Solution {    public int largestRectangleArea(int[] heights) {        int n = heights.length;        Stack<Integer> s = new Stack<Integer>();        int max = 0;        for(int i = 0; i <= n; ){             int h = (i == n ? 0 : heights[i]);            if(s.isEmpty() || heights[s.peek()] <= h){                s.push(i ++);            }else{                                int temp = s.pop();                //此时的s.peek（）是左边第一个比当前top元素小的数                //理解的话就是当前top高度能维持多久，比如图中1,2，中间5，6都可以维持2的高度，直到1不行了                //当前处于i是短的且不动，栈里往前找也是短的，其实是取中间的                //最后栈里没数了用i，可以理解为最后一个数或者前面没有数比它小了，直接起点为0，终点为i                max = Math.max(max, heights[temp] * (s.isEmpty() ?  i : i - s.peek() - 1));            }                   }      return max;      }}
```

