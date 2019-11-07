# Smallest Range

You have`k`lists of sorted integers in ascending order. Find the**smallest**range that includes at least one number from each of the`k`lists.

We define the range \[a,b\] is smaller than range \[c,d\] if`b-a < d-c`or`a < c`if`b-a == d-c`.

**Example 1:**

```text
Input:[[4,10,15,24,26], [0,9,12,20], [5,18,22,30]]Output: [20,24]Explanation:List 1: [4, 10, 15, 24,26], 24 is in range [20,24].List 2: [0, 9, 12, 20], 20 is in range [20,24].List 3: [5, 18, 22, 30], 22 is in range [20,24].
```

Note:

```text
The given list may contain duplicates, so ascending order means >= here.1 <= k <= 3500-105 <= value of elements <= 105.For Java users, please note that the input type has been changed to List<List<Integer>>. And after you reset the code template, you'll see this point.
```

分析

就是heapq前K大的思想

pq存每个List\[index\],list,index right=max\[pq\]，left=pq.pop\(\)

pop element A\[i\]\[j\], replace it with A\[i\]\[j+1\]，同时得到新right=max\(right,v\)

```text
Keep a heap of the smallest elements. As we pop element A[i][j], we'll replace it with A[i][j+1]. For each such element left, we want right, the maximum of the closest value in each row of the array that is >= left, which is also equal to the current maximum of our heap. We'll keep track of right as we proceed.
```

```text
class Solution:    def smallestRange(self, nums: List[List[int]]) -> List[int]:        pq = [(v[0],i,0) for i,v in enumerate(nums)]        heapq.heapify(pq)        right = max(i[0] for i in pq)        ans = -1e9, 1e9        while pq:            left,i,j = heapq.heappop(pq)            if right-left < ans[1] - ans[0]:                ans = left,right            if j+1 == len(nums[i]):                return ans            v = nums[i][j+1]            right = max(right,v)            heapq.heappush(pq,(v,i,j+1))        return ans
```

