# Max Points on a Line

Given\_n\_points on a 2D plane, find the maximum number of points that lie on the same straight line.

**Example 1:**

```text
Input:
 [[1,1],[2,2],[3,3]]

Output:
 3

Explanation:

^
|
|        o
|     o
|  o  
+-------------
>

0  1  2  3  4
```

**Example 2:**

```text
Input:
 [[1,1],[3,2],[5,3],[4,1],[2,3],[1,4]]

Output:
 4

Explanation:

^
|
|  o
|     o        o
|        o
|  o        o
+-------------------
>

0  1  2  3  4  5  6
```

分析

**定出发点，找斜率相同直线”的方法**。然后遍历所有直线，用HashMap计数，x遍历1-n，y从x+1开始到n。

Map&lt;Integer, Map&lt;Integer, Integer&gt;&gt; map 存的是（x,\(y, 此斜率个数\)）

此处x, y是2个点x1-x2, y1-y2，为了防止溢出，用的gcd最大公约数相除。

**此题不用斜率存入Map，因为double的斜率也还是会不准确，用最大公约数把x,y处理了，好让它们不会越界。**

注意2次max，第二次才加上共点。

答案

```text
/**
 * Definition for a point.
 * class Point {
 *     int x;
 *     int y;
 *     Point() { x = 0; y = 0; }
 *     Point(int a, int b) { x = a; y = b; }
 * }
 */
//此题不用斜率存入Map，因为double的斜率也还是会不准确，用最大公约数把x,y处理了，好让它们不会越界。
class Solution {
    public int maxPoints(Point[] points) {
        if(points == null || points.length == 0) {
            return 0;
        }

        Map<Integer, Map<Integer, Integer>> map = new HashMap<>();
        int n = points.length, result = 0;
        for(int i = 0; i < n; i ++) {
            int max =0, samePoint = 0;
            map.clear();//漏了这一步，一定记得要清空map
            for(int j = i + 1; j < n; j ++) {
                int x  = points[i].x - points[j].x;
                int y = points[i].y - points[j].y;
                if(x == 0 && y == 0) {
                    samePoint ++;
                    continue;
                }
                int gcd = getGcd(x, y);
                x = x / gcd;
                y = y / gcd;
                if(map.containsKey(x)) {
                    if(map.get(x).containsKey(y)){
                        map.get(x).put(y, map.get(x).get(y) + 1);
                    }else {
                        map.get(x).put(y,1);
                    }
                }else{
                    Map<Integer,Integer> temp = new HashMap<>();
                    temp.put(y, 1);
                    map.put(x, temp);
                }
                max = Math.max(max, map.get(x).get(y));//此处只要得到map里斜率最大的，不要加上共点。
            }
            result = Math.max(result, max + samePoint + 1);//此处才需要加上共点们。
        }
        return result;
    }

    public int getGcd(int a, int b) {
        if(b == 0) {
            return a;
        }
        return getGcd(b, a % b);
    }
}
```

