# My Calendar III



Implement a `MyCalendarThree` class to store your events. A new event can **always** be added.

Your class will have one method, `book(int start, int end)`. Formally, this represents a booking on the half open interval `[start, end)`, the range of real numbers `x` such that `start <= x < end`.

A K-booking happens when **K** events have some non-empty intersection \(ie., there is some time that is common to all K events.\)

For each call to the method `MyCalendar.book`, return an integer `K` representing the largest integer such that there exists a `K`-booking in the calendar.Your class will be called like this: `MyCalendarThree cal = new MyCalendarThree();` `MyCalendarThree.book(start, end)`

**Example 1:**

```text
MyCalendarThree();MyCalendarThree.book(10, 20); // returns 1MyCalendarThree.book(50, 60); // returns 1MyCalendarThree.book(10, 40); // returns 2MyCalendarThree.book(5, 15); // returns 3MyCalendarThree.book(5, 10); // returns 3MyCalendarThree.book(25, 55); // returns 3Explanation: The first two events can be booked and are disjoint, so the maximum K-booking is a 1-booking.The third event [10, 40) intersects the first event, and the maximum K-booking is a 2-booking.The remaining events cause the maximum K-booking to be only a 3-booking.Note that the last event locally causes a 2-booking, but the answer is still 3 becauseeg. [10, 20), [10, 40), and [5, 15) are still triple booked.
```

**Note:**

* The number of calls to `MyCalendarThree.book` per test case will be at most `400`.
* In calls to `MyCalendarThree.book(start, end)`, `start` and `end` are integers in the range `[0, 10^9]`.

sweep line

和meeting room II 一样，start, end分成2个点加入arr， sort后遍历，得到最大的maxcnt

```text
class MyCalendarThree:    def __init__(self):        self.arr = collections.Counter()            def book(self, start: int, end: int) -> int:        self.arr[start] += 1        self.arr[end] -= 1                res = cnt = 0        for k in sorted(self.arr):            cnt += self.arr[k]            res = max(res, cnt)        return res                # Your MyCalendarThree object will be instantiated and called as such:# obj = MyCalendarThree()# param_1 = obj.book(start,end)
```

线段树

{% embed url="https://leetcode.com/problems/my-calendar-iii/discuss/214831/Python-13-Lines-Segment-Tree-with-Lazy-Propagation-O\(1\)-time" %}

这里直接

```text
self.seg[ID] = self.lazy[ID] + max(self.seg[2*ID], self.seg[2*ID+1])
```

query结果也是返回root 

```text
self.seg[1] + self.lazy[1]
```

没有pushdown

```text
class MyCalendarThree:    def __init__(self):        self.tree = collections.defaultdict(int) #一定要加int,否则出错        self.lazy = collections.defaultdict(int)            def book(self, start: int, end: int) -> int:        def update(s,e,l=0,r=10**9,ID=1):            if r <= s or e <= l: return             if s<=l and r<=e:                self.tree[ID] += 1                self.lazy[ID] += 1            else:                m = (l+r)//2                update(s,e,l,m,ID<<1)                update(s,e,m,r,ID<<1|1)                self.tree[ID] = self.lazy[ID] + max(self.tree[ID<<1],self.tree[ID<<1|1])            # return self.tree[ID]        update(start,end)        return self.tree[1]+self.lazy[1]                                # Your MyCalendarThree object will be instantiated and called as such:# obj = MyCalendarThree()# param_1 = obj.book(start,end)
```

