# Kth Largest Element in a Stream

Design a class to find the**k**th largest element in a stream. Note that it is the kth largest element in the sorted order, not the kth distinct element.

Your `KthLargest` class will have a constructor which accepts an integer`k`and an integer array`nums`, which contains initial elements from the stream. For each call to the method`KthLargest.add`, return the element representing the kth largest element in the stream.

**Example:**

```text
int k = 3;
int[] arr = [4,5,8,2];
KthLargest kthLargest = new KthLargest(3, arr);
kthLargest.add(3);   // returns 4
kthLargest.add(5);   // returns 5
kthLargest.add(10);  // returns 5
kthLargest.add(9);   // returns 8
kthLargest.add(4);   // returns 8
```

**Note:**  
You may assume that `nums`' length ≥ `k-1` and`k`≥ 1.

分析

使用最小堆啊！

```text
""
```

```text
"
Create a pq - keep it only having the k-largest elements by popping off small elements.
With only k elements, the smallest item (self.pool[0]) will always be the kth largest.

If a new value is bigger than the smallest, it should be added into your heap.
If it's bigger than the smallest (that are already the kth largest), it will certainly be within the kth largest of the stream.
"
""
```

```text
import heapq


class KthLargest:

    def __init__(self, k, nums):
        """
        :type k: int
        :type nums: List[int]
        """
        self.pool = nums
        self.k = k
        heapq.heapify(self.pool)
        while len(self.pool)>k:
            heapq.heappop(self.pool)

    def add(self, val):
        """
        :type val: int
        :rtype: int
        """
        if len(self.pool) < self.k:
            heapq.heappush(self.pool,val)
        else:
            heapq.heappushpop(self.pool,val)
        return self.pool[0]



# Your KthLargest object will be instantiated and called as such:
# obj = KthLargest(k, nums)
# param_1 = obj.add(val)
```

