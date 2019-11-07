# Most Profit Assigning Work

We have jobs:`difficulty[i]` is the difficulty of the `i`th job, and `profit[i]` is the profit of the `i`th job.

Now we have some workers. `worker[i]` is the ability of the `i`th worker, which means that this worker can only complete a job with difficulty at most `worker[i]`.

Every worker can be assigned at most one job, but one job can be completed multiple times.

For example, if 3 people attempt the same job that pays $1, then the total profit will be $3. If a worker cannot complete any job, his profit is $0.

What is the most profit we can make?

**Example 1:**

```text
Input: difficulty = [2,4,6,8,10], profit = [10,20,30,40,50], worker = [4,5,6,7]Output: 100 Explanation: Workers are assigned jobs of difficulty [4,4,6,6] and they get profit of [20,20,30,30] seperately.
```

```text
Notes:1 <= difficulty.length = profit.length <= 100001 <= worker.length <= 10000difficulty[i], profit[i], worker[i]  are in range [1, 10^5]
```

分析

把jobs = zip（diff, profit）排序，然后worker ability也排序。

每次选该worker能力所及的最大profit，for worker里面while jobs

```text
class Solution:    def maxProfitAssignment(self, difficulty: List[int], profit: List[int], worker: List[int]) -> int:        jobs = sorted([a,b] for a,b in zip(difficulty, profit))        res = maxp = i= 0        worker = sorted(worker)        for ability in worker:            while i < len(jobs) and ability >= jobs[i][0]:                maxp = max(maxp, jobs[i][1])                i += 1            res += maxp        return res
```

用priority queue, （difficult，profit\) ascending排序入pq，worker也排序。

每次弹出来ability够cover就更新maxprofit，否则就可以加入res同时移动worker，塞\(d,p）回pq

```text
class Solution:    def maxProfitAssignment(self, difficulty: List[int], profit: List[int], worker: List[int]) -> int:        q = list(zip(difficulty,profit))        heapq.heapify(q)        worker = sorted(worker)        i,maxp,res = 0,0,0        while q and i < len(worker):            d,p = heapq.heappop(q)            if d <= worker[i]:                maxp = max(maxp,p)            else:                res += maxp                i += 1                heapq.heappush(q,(d,p))        while i < len(worker):            res += maxp            i += 1        return res
```

