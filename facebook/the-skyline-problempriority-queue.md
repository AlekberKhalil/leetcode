# The Skyline Problem\(priority queue\)

A city's skyline is the outer contour of the silhouette formed by all the buildings in that city when viewed from a distance. Now suppose you are**given the locations and height of all the buildings**as shown on a cityscape photo \(Figure A\), write a program to**output the skyline**formed by these buildings collectively \(Figure B\).

[![Buildings](https://leetcode.com/static/images/problemset/skyline1.jpg)](https://leetcode.com/static/images/problemset/skyline1.jpg)

[![Skyline Contour](https://leetcode.com/static/images/problemset/skyline2.jpg)](https://leetcode.com/static/images/problemset/skyline2.jpg)

The geometric information of each building is represented by a triplet of integers`[Li, Ri, Hi]`, where`Li`and`Ri`are the x coordinates of the left and right edge of the ith building, respectively, and`Hi`is its height. It is guaranteed that`0 ≤ Li, Ri ≤ INT_MAX`,`0 < Hi ≤ INT_MAX`, and`Ri - Li > 0`. You may assume all buildings are perfect rectangles grounded on an absolutely flat surface at height 0.

For instance, the dimensions of all buildings in Figure A are recorded as:`[ [2 9 10], [3 7 15], [5 12 12], [15 20 10], [19 24 8] ]`.

The output is a list of "**key points**" \(red dots in Figure B\) in the format of`[ [x1,y1], [x2, y2], [x3, y3], ... ]`that uniquely defines a skyline.**A key point is the left endpoint of a horizontal line segment**. Note that the last key point, where the rightmost building ends, is merely used to mark the termination of the skyline, and always has zero height. Also, the ground in between any two adjacent buildings should be considered part of the skyline contour.

For instance, the skyline in Figure B should be represented as:`[ [2 10], [3 15], [7 12], [12 0], [15 10], [20 8], [24, 0] ]`.

**Notes:**

* The number of buildings in any input list is guaranteed to be in the range

  `[0, 10000]`

  .

* The input list is already sorted in ascending order by the left x position

  `Li`

  .

* The output list must be sorted by the x position.
* There must be no consecutive horizontal lines of equal height in the output skyline. For instance,

  `[...[2 3], [4 5], [7 5], [11 5], [12 7]...]`

  is not acceptable; the three lines of height 5 should be merged into one in the final output as such:

  `[...[2 3], [4 5], [12 7], ...]`

分析

1 x坐标相同，进入按height从大到小，出来按从小到大。为了防止重复加入点。

2 priority queque是max heap，记得用Collections.reverseOrder\(\)

3 所有edge压入pq。只有当前edge&gt;pq.peek\(\)才能入结果（拐点）

```text
class Edge {
    int x;
    int height;
    boolean isStart;
    public Edge(int x, int height, boolean isStart){
        this.x = x;
        this.height = height;
        this.isStart = isStart;

    }
}
class Solution {
    public List<int[]> getSkyline(int[][] buildings) {
        List<int[]> result = new ArrayList<>();
        if (buildings== null || buildings.length == 0
                || buildings[0].length == 0) {
            return result;
        }
        List<Edge> edges = new ArrayList<>();
        for(int[] b : buildings){
            edges.add(new Edge(b[0],b[2],true));
            edges.add(new Edge(b[1],b[2],false));
        }
        Collections.sort(edges, new Comparator<Edge>() {
            @Override
            public int compare(Edge o1, Edge o2) {
                if(o1.x!=o2.x){
                    return o1.x-o2.x;
                }
                if(o1.isStart && o2.isStart){
                    return o2.height-o1.height;//进入高度从大到小
                }
                if(!o1.isStart && !o2.isStart){
                    return o1.height-o2.height;//出来高度从小到大
                }

                return o1.isStart ? -1 : 1;//同x，start先end后
            }
        });
        PriorityQueue<Integer> q = new PriorityQueue<>(Collections.reverseOrder());

        for (Edge e : edges){
            if(e.isStart){
                if (q.isEmpty() || q.peek() < e.height){
                    result.add(new int[]{e.x, e.height});
                }
                q.offer(e.height);

            }else{
                q.remove(e.height);
                if(q.isEmpty()){
                    result.add(new int[]{e.x,0});
                }
                else if(q.peek() < e.height){
                    result.add(new int[]{e.x,q.peek()});
                }
            }
        }
        return result;

    }
}
```

另一种做法，把height按负数来排序，很巧妙。记得入pq之后一定要把负数height还原。

初始pq要压入0作为开始！！！！！！

所有edge都压入栈。只有出现pre!=cur 有变化是拐点，要入结果。

```text
class Solution {
    public List<int[]> getSkyline(int[][] buildings) {
        List<int[]> result = new ArrayList<>();
        if (buildings== null || buildings.length == 0
                || buildings[0].length == 0) {
            return result;
        }
        List<int[]> edges = new ArrayList<>();
        for(int[] b : buildings){
            edges.add(new int[]{b[0],-b[2]});
            edges.add(new int[]{b[1],b[2]});
        }
        Collections.sort(edges, new Comparator<int[]>() {
            @Override
            public int compare(int[] o1, int[] o2) {
                if(o1[0]!=o2[0]){
                    return o1[0]-o2[0];
                }
                else
                    return o1[1]-o2[1];//因为是负数，所以start的数字从大到小，end的数字从小到大

            }
        });

        PriorityQueue<Integer> q = new PriorityQueue<>((a,b)->(b-a));
        q.offer(0);
        int prev = 0;
        for(int[] e :edges){
            if(e[1]<0){
                q.offer(-e[1]);
            }else{
                q.remove(e[1]);
            }
            int cur = q.peek();
            if(cur!=prev){//发生变化就是拐点
                result.add(new int[]{e[0],cur});
                prev = cur;
            }


        }

        return result;

    }
}
```

