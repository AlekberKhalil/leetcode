# Meeting Rooms

Given an array of meeting time intervals consisting of start and end times`[[s1,e1],[s2,e2],...] (si < ei)`, determine if a person could attend all meetings.

## Example

Given intervals =`[[0,30],[5,10],[15,20]]`, return`false`.

分析

start+1 end-1 每次total&gt;1就不行

也可以不必拆interval，直接排序interval， 如果i.start &lt; i-1.end 就返回false

```text
# Definition of Interval.
# class Interval(object):
#     def __init__(self, start, end):
#         self.start = start
#         self.end = end


class Solution:
    """
    @param intervals: an array of meeting time intervals
    @return: if a person could attend all meetings
    """
    def canAttendMeetings(self, intervals):
        # Write your code here
        times=[]
        for i in intervals:            
            times.append((i.start,1))
            times.append((i.end,-1))
        times.sort()
        s=0
        for _,d in times:
            s+=d
            if s>1:
                return False
        return True
```

