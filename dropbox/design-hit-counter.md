# Design Hit Counter

Design a hit counter which counts the number of hits received in the past 5 minutes.

Each function accepts a timestamp parameter \(in seconds granularity\) and you may assume that calls are being made to the system in chronological order \(ie, the timestamp is monotonically increasing\). You may assume that the earliest timestamp starts at 1.

It is possible that several hits arrive roughly at the same time.

**Example:**

```text
HitCounter counter = new HitCounter();// hit at timestamp 1.counter.hit(1);// hit at timestamp 2.counter.hit(2);// hit at timestamp 3.counter.hit(3);// get hits at timestamp 4, should return 3.counter.getHits(4);// hit at timestamp 300.counter.hit(300);// get hits at timestamp 300, should return 4.counter.getHits(300);// get hits at timestamp 301, should return 3.counter.getHits(301); 
```

**Follow up:**  
What if the number of hits per second could be very large? Does your design scale?

一个size 300的数组，每次新来的数都mod到相应位置，新数覆盖，旧数 cnt++

getHit时候，loop数组，curtime-300内的都 加入res

```text
class HitCounter:    def __init__(self):        """        Initialize your data structure here.        """             self.q = [(0,0)]*300                    def hit(self, timestamp: int) -> None:        """        Record a hit.        @param timestamp - The current timestamp (in seconds granularity).        """        idx = timestamp%300        time,cnt = self.q[idx]        if time == timestamp:            self.q[idx] = (time,cnt+1)        else:            self.q[idx] = (timestamp,1)                                        def getHits(self, timestamp: int) -> int:        """        Return the number of hits in the past 5 minutes.        @param timestamp - The current timestamp (in seconds granularity).        """        res = 0        for t,c in self.q:            if timestamp - t <300:                res += c        return res                  
```



Orderdict 做 保证里面的时间有序

全局cnt和Orderdict，每次有数都cnt++。dict存 time:cnt **用Map不让单独一个元素占一个位置，耗内存**

满的时候**删dict**，注意不要动态改dict

```text
class HitCounter:    def __init__(self):        """        Initialize your data structure here.        """        self.map = collections.OrderedDict()        self.cnt = 0            def hit(self, timestamp: int) -> None:        """        Record a hit.        @param timestamp - The current timestamp (in seconds granularity).        """        self.map[timestamp] = self.map.get(timestamp,0)+1        self.cnt += 1            def getHits(self, timestamp: int) -> int:        """        Return the number of hits in the past 5 minutes.        @param timestamp - The current timestamp (in seconds granularity).        """        limit = timestamp - 300        dels = []        for k in self.map:            if k <= limit:                self.cnt -= self.map[k]                dels.append(k)        for d in dels:            del self.map[d]        return self.cnt# Your HitCounter object will be instantiated and called as such:# obj = HitCounter()# obj.hit(timestamp)# param_2 = obj.getHits(timestamp)
```

deque做法，也是global的cnt一直增加，**每个timestamp在q里占一个位置，吃内存。**

后面是popLeft掉前面过期数 timestamp-300之前的，q可以动态改。

```text
class HitCounter:    def __init__(self):        """        Initialize your data structure here.        """        self.q = collections.deque()        self.cnt = 0            def hit(self, timestamp: int) -> None:        """        Record a hit.        @param timestamp - The current timestamp (in seconds granularity).        """        self.q.append(timestamp)        self.cnt += 1            def getHits(self, timestamp: int) -> int:        """        Return the number of hits in the past 5 minutes.        @param timestamp - The current timestamp (in seconds granularity).        """        limit = timestamp - 300                while self.cnt > 0 and self.q[0] <= limit:            self.q.popleft()            self.cnt -= 1                    return self.cnt
```





