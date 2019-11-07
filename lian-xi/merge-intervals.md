# Merge Intervals\(sweep line\)

Given a collection of intervals, merge all overlapping intervals.

For example,  
Given`[1,3],[2,6],[8,10],[15,18]`,  
return`[1,6],[8,10],[15,18]`.

```text
/** * Definition for an interval. * public class Interval { *     int start; *     int end; *     Interval() { start = 0; end = 0; } *     Interval(int s, int e) { start = s; end = e; } * } */class Solution {    public List<Interval> merge(List<Interval> intervals) {        if(intervals.size() <= 1)            return intervals;        List<Interval> ret = new ArrayList<Interval>();        intervals.sort((i1, i2) -> Integer.compare(i1.start, i2.start));        int start = intervals.get(0).start;        int end = intervals.get(0).end;        for(Interval i : intervals){            if(i.start <= end){                end = Math.max(end, i.end);            }else{                ret.add(new Interval(start, end));                start = i.start;                end = i.end;            }        }        ret.add(new Interval(start, end));//还要加上最后一个interval        return ret;    }}
```

