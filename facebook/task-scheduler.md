# Task Scheduler

Given a char array representing tasks CPU need to do. It contains capital letters A to Z where different letters represent different tasks.Tasks could be done without original order. Each task could be done in one interval. For each interval, CPU could finish one task or just be idle.

However, there is a non-negative cooling interval**n**that means between two**same tasks**, there must be at least n intervals that CPU are doing different tasks or just be idle.

You need to return the**least**number of intervals the CPU will take to finish all the given tasks.

**Example 1:**

```text
Input: tasks = ["A","A","A","B","B","B"], n = 2
Output: 8
Explanation: A -> B -> idle -> A -> B -> idle -> A -> B.
```

**Note:**

1. The number of tasks is in the range \[1, 10000\].
2. The integer n is in the range \[0, 100\].

分析

最大数目的那个task用来做分隔点

```text
partCount = count(A) - 1
emptySlots = partCount * (n - (count of tasks with most frequency - 1))
availableTasks = tasks.length - count(A) * count of tasks with most frenquency
idles = max(0, emptySlots - availableTasks)
result = tasks.length + idles
```

```text
class Solution:
    def leastInterval(self, tasks, n):
        """
        :type tasks: List[str]
        :type n: int
        :rtype: int
        """
        cntMap = collections.defaultdict(int)
        for i in tasks:
            cntMap[i] += 1

        taskCnt = sorted(cntMap.values(),reverse=True)

        nMaxCnt = taskCnt.count(taskCnt[0])
        nPart = taskCnt[0] - 1
        nSlot = nPart * (n - (nMaxCnt - 1))
        availableTask = len(tasks) - nMaxCnt*taskCnt[0]
        idle = max(0,nSlot - availableTask)
        return len(tasks) + idle
```

更简单方法

最大cnt为界，前面cnt-1个部分 = \(cnt-1\)\*\(n+1\) n是间隔1是数字本身

最后一个部分直接加上所有最大frequency的数字

记得比较task.length。返回更大那个

```text
import collections


class Solution:
    def leastInterval(self, tasks, n):
        """
        :type tasks: List[str]
        :type n: int
        :rtype: int
        """
        maxcnt = 0
        counter = collections.defaultdict(int)
        for t in tasks:
            counter[t] +=1
            maxcnt = max(maxcnt,counter[t])
        ans = (maxcnt-1)*(n+1)
        for c in counter:
            if counter[c] == maxcnt:
                ans +=1
        return max(ans,len(tasks))
```

