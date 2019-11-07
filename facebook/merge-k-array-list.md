# merge K array list

pq存tuple

```text
# Definition for singly-linked list.import heapqclass ArrayContainer():    def __init__(self, index, arr):        self.index = index        self.arr = arrclass Solution:    def mergeKLists(self, lists):        """        :type lists: List[List]        :rtype: List        """        pq = []        res = []        for i in lists:            heapq.heappush(pq, (i[0],ArrayContainer(0,i)))        while pq:            cur = heapq.heappop(pq)[1]            res.append(cur.arr[cur.index])            if cur.index < len(cur.arr)-1:                heapq.heappush(pq, (cur.arr[cur.index+1],ArrayContainer(cur.index+1, cur.arr)))        return res    # obj = Solution()    #    # input = [[1, 5, 8, 9],    #          [2, 3, 7, 10],    #          [4, 6, 11, 15],    #          [9, 14, 16, 19],    #          [2, 4, 6, 9]]    #    # ret = obj.mergeKLists(input)    # print(ret)
```

只用tuple不用obj的话

```text
# Definition for singly-linked list.import heapqclass Solution:    def mergeKLists(self, lists):        """        :type lists: List[List]        :rtype: List        """        pq = []        res = []        for i in lists:            heapq.heappush(pq, (i[0],0,i))        while pq:            cur = heapq.heappop(pq)            res.append(cur[0])            if cur[1] < len(cur[2])-1:                heapq.heappush(pq, (cur[2][cur[1]+1],cur[1]+1, cur[2]))        return res
```

