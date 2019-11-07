# Number of Airplanes in the Sky\(sweep line\)

Given an interval list which are flying and landing time of the flight. How many airplanes are on the sky at most?

## Notice

If landing and flying happens at the same time, we consider landing should happen at first.

**Example**

For interval list

```text
[
  [1,10],
  [2,3],
  [5,8],
  [4,7]
]
```

Return`3`

分析：

扫描法 sweep-line。 区间问题用扫描法，时间区间拆成两个，等于建一个时间list， 然后按照早晚排序。遍历时间线，根据升降情况增减count。

**对于comparator override，数组用Arrays.sort\(l,new Comparator\(\)\). object的list用Collections.sort\(l, new Comparator\(\)\)**

答案：

```text
/**
 * Definition of Interval:
 * public classs Interval {
 *     int start, end;
 *     Interval(int start, int end) {
 *         this.start = start;
 *         this.end = end;
 *     }
 */
class Point{
    int time, flag;
    Point(int time, int flag){
        this.time = time;
        this.flag = flag;
    }
}
class Solution {
    /**
     * @param intervals: An interval array
     * @return: Count of airplanes are in the sky.
     */
    public int countOfAirplanes(List<Interval> airplanes) { 
        // write your code here
        if(airplanes == null || airplanes.size() == 0)
            return 0;
        List<Point> l = new ArrayList<Point>();
        for(Interval i : airplanes){
            l.add(new Point(i.start, 1));
            l.add(new Point(i.end, 0));
        }

        Collections.sort(l, new Comparator<Point>(){
            public int compare(Point x, Point y){
                if(x.time == y.time)
                    return x.flag - y.flag;//如果时间一样，先降后升
                return x.time - y.time;
            }
        });
        int count = 0, ret = 0;
        for(Point p : l){
            if(p.flag == 1){
                count ++;
                ret = Math.max(count, ret);
            }
            else
                count --;
        }
        return ret;
    }
}
```

