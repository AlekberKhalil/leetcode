# Find Right Interval



#### Description

Given a set of intervals, for each of the interval i, check if there exists an interval j whose start point is bigger than or equal to the end point of the interval i, which can be called that j is on the "right" of i.

For any interval i, you need to store the minimum interval j's index, which means that the interval j has the minimum start point to build the "right" relationship for interval i. If the interval j doesn't exist, store -1 for the interval i. Finally, you need output the stored value of each interval as an array.

* You may assume the interval's end point is always bigger than its start point.
* You may assume none of these intervals have the same start point.

Have you met this question in a real interview?  YesProblem Correction

#### Example

**Example 1:**

```text
Input: intervals = [(1,2)]
Output: [-1]
Explanation: 
There is only one interval in the collection, so it outputs -1.
```

**Example 2:**

```text
Input: intervals = [(3,4),(2,3),(1,2)]
Output: [-1, 0, 1]
Explanation: 
There is no satisfied "right" interval for (3,4).
For (2,3), the interval (3,4) has minimum-"right" start point;
For (1,2), the interval (2,3) has minimum-"right" start point.
```

分析

starts做数组排序，loop end找到pos， 有则插入res，否则-1

找pos可以自己写二分，查找的arr是\[\(start,index in intervals\)\]

用bisect\_left的话，找到arr是\[starts\]， 返回index需要在start\_index map里找对应index。

注意bisect\_left返回len时候，就是没有找到

1 自己写二分

```text
"""
Definition of Interval.
class Interval(object):
    def __init__(self, start, end):
        self.start = start
        self.end = end
"""

class Solution:
    """
    @param intervals: a list of intervals
    @return: return a list of integers
    """
    def findRightInterval(self, intervals):
        # write your code here
        start_index = [(val.start,index) for index, val in enumerate(intervals)]
        start_index.sort()
        
        
        def findNearestIndex(end, starts):
            s,e = 0,len(starts)-1
            while s+1 < e:
                m = s + (e-s)//2
                if starts[m][0] >= end:
                    e = m
                else:
                    s = m
            if starts[s][0] >= end:
                return starts[s][1]
            if starts[e][0] >= end:
                return starts[e][1]
            return -1
        
        res = []    
        for i in intervals:
            idx = findNearestIndex(i.end, start_index)
            res.append(idx)
        return res
```

2 用bisect

注意

1找不到bisect\_left 返回的是len

2可以用lambda定义函数直接调用

```text
"""
Definition of Interval.
class Interval(object):
    def __init__(self, start, end):
        self.start = start
        self.end = end
"""
from bisect import bisect_left
class Solution:
    """
    @param intervals: a list of intervals
    @return: return a list of integers
    """
    def findRightInterval(self, intervals):
        # write your code here
        start_index = {val.start:index for index, val in enumerate(intervals)}
        starts = sorted(start_index.keys())
        right_index = lambda x : bisect_left(starts, x)
   
        res = []    
        for i in intervals:
            idx = right_index(i.end)
            if idx < len(start_index):
                res.append(start_index[starts[idx]])
            else:
                res.append(-1)
        return res
```

第三种做法

利用stack只存end, 把start end打散成点排序，loop所有点，遇到start弹出end栈内所有比它小的end，存结果，遇到end就入end栈，注意end栈存的是end index

```text
"""
Definition of Interval.
class Interval(object):
    def __init__(self, start, end):
        self.start = start
        self.end = end
"""

class Solution:
    """
    @param intervals: a list of intervals
    @return: return a list of integers
    """
    def findRightInterval(self, intervals):
        # write your code here
        ps = [(val.start,True,i) for i,val in enumerate(intervals)] +  [(val.end,False,i) for i,val in enumerate(intervals)]
        ps.sort()
        endsStack,res = [],[-1]*len(intervals)
        for p, isStart, idx in ps:
            if isStart:
                while endsStack: #注意此处是while 不是if 所有比当前start小的end都弹出来进入结果
                    res[endsStack.pop()] = idx
                
            else:
                endsStack.append(idx)
        return res
                
```



