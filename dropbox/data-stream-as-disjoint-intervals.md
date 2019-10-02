# Data Stream as Disjoint Intervals

Given a data stream input of non-negative integers a1, a2, ..., an, ..., summarize the numbers seen so far as a list of disjoint intervals.

For example, suppose the integers from the data stream are 1, 3, 7, 2, 6, ..., then the summary will be:

```text
[1, 1]
[1, 1], [3, 3]
[1, 1], [3, 3], [7, 7]
[1, 3], [7, 7]
[1, 3], [6, 7]
```

**Follow up:**

What if there are lots of merges and the number of disjoint intervals are small compared to the data stream's size?

排序的intervals，每次新数找到位置，或者插入，或者合并。

此处用stack做temp，loop heap, 存heap倒出来的，合并需要合并的，然后heap=stack,赋值回去。

```text
class SummaryRanges:

    def __init__(self):
        """
        Initialize your data structure here.
        """
        self.q = []
        

    def addNum(self, val: int) -> None:
        heapq.heappush(self.q, (val,[val,val]))
        
        
            
        

    def getIntervals(self) -> List[List[int]]:
        stack = []
        while self.q:
            idx,cur = heapq.heappop(self.q)
            if not stack:
                stack.append((idx,cur))
            else: 
                _,pre = stack[-1]
                if cur[0] <= pre[1]+1:
                    pre[1] = max(pre[1],cur[1])
                else:
                    stack.append((idx,cur))
        self.q = stack
        return list(map(lambda x: x[1], self.q))
        
                    
            
         
        


# Your SummaryRanges object will be instantiated and called as such:
# obj = SummaryRanges()
# obj.addNum(val)
# param_2 = obj.getIntervals()
```

