# Meeting room II\(sweep line\)

Given an array of meeting time intervals consisting of start and end times \[\[s1,e1\],\[s2,e2\],...\] \(si &lt;ei\), find the minimum number of conference rooms required.

For example,

Given \[\[0, 30\],\[5, 10\],\[15, 20\]\],

return 2.

分析

扫描法 sweep-line。 区间问题用扫描法，时间区间拆成两个，等于建一个时间list， 然后按照时间早晚排序，时间一样就先降后升。遍历时间线，根据升降情况增减count。

```text
class Interval {      int start;      int end;      Interval() { start = 0; end = 0; }      Interval(int s, int e) { start = s; end = e; }  }  class Time{    int flag;    int time;    public Time(int flag, int time){        this.time = time;        this.flag = flag;    }  }public class Solution {    public int canAttendMeetings(Interval[] intervals) {        List<Time> t = new ArrayList<Time>();        for(Interval i : intervals){            t.add(new Time(1, i.start));            t.add(new Time(0, i.end));        }        Collections.sort(t, new Comparator<Time>() {            @Override            public int compare(Time o1, Time o2) {                if(o1.time == o2.time){                    return o1.flag - o2.flag;                }                return o1.time - o2.time;            }        });        int cnt = 0, max = 0;        for(Time x : t){            if(x.flag == 1){                cnt ++;                max = Math.max(max, cnt);//注意要记录的是最多重叠的时候 不要因为题目是Min就错            }else{                cnt --;            }        }        return max;    }     public static void main(String[] args) throws IOException {        Solution s  = new Solution();        Interval[] intervals = {new Interval(0,30),new Interval(5,10),new Interval(15,20) };        int ret = s.canAttendMeetings(intervals);        System.out.print(ret);        }    }
```

