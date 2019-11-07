# Meeting room\(sweep line\)

Given an array of meeting time intervals consisting of start and end times \[\[s1,e1\],\[s2,e2\],...\] \(si &lt;ei\), determine if a person could attend all meetings.

For example,

Given \[\[0, 30\],\[5, 10\],\[15, 20\]\],

return false.

分析

按照起始时间排序，然后遍历起始每个Interval。判断起始时间是否晚于前面结束时间。

```text
//  Definition for an interval.
class Interval {
      int start;
      int end;
      Interval() { start = 0; end = 0; }
      Interval(int s, int e) { start = s; end = e; }
  }


public class Solution {
    public boolean canAttendMeetings(Interval[] intervals) {
        Arrays.sort(intervals, new Comparator<Interval>() {
            @Override
            public int compare(Interval o1, Interval o2) {
                return o1.start - o2.start;
            }
        });

        for(int i = 1; i < intervals.length; i ++){
            if(intervals[i].start < intervals[i-1].end){
                return false;
            }
        }
        return true;
    }
}
```

