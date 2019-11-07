# Reconstruct Itinerary

Given a list of airline tickets represented by pairs of departure and arrival airports`[from, to]`, reconstruct the itinerary in order. All of the tickets belong to a man who departs from`JFK`. Thus, the itinerary must begin with`JFK`.

**Note:**

1. If there are multiple valid itineraries, you should return the itinerary that has the smallest lexical order when read as a single string. For example, the itinerary

   `["JFK", "LGA"]`

   has a smaller lexical order than

   `["JFK", "LGB"]`

   .

2. All airports are represented by three capital letters \(IATA code\).
3. You may assume all tickets form at least one valid itinerary.

**Example 1:**

```text
Input: 
[["MUC", "LHR"], ["JFK", "MUC"], ["SFO", "SJC"], ["LHR", "SFO"]]
Output: 
["JFK", "MUC", "LHR", "SFO", "SJC"]
```

**Example 2:**

```text
Input: 
[["JFK","SFO"],["JFK","ATL"],["SFO","ATL"],["ATL","JFK"],["ATL","SFO"]]
Output: 
["JFK","ATL","JFK","SFO","ATL","SFO"]
Explanation: 
Another possible reconstruction is 
["JFK","SFO","ATL","JFK","ATL","SFO"]
.
             But it is larger in lexical order.
```

分析

选一条jfk出发的可行路线，lexico最小

首先建有序图，然后排序neighbors,每次选最小那个neighbor，key顺序不重要

**neighbor list用过的点要去掉，要不会一直重复，想象票用了就不可再用。**

因为dfs最后加入start点，所以结果要reverse

sorted\(tickets\)会自动按照第一个数然后第二个数排序，\[::-1\]之后2个都倒序了。

```text
class Solution:
    def findItinerary(self, tickets: List[List[str]]) -> List[str]:
        g = {}
        for s,a in sorted(tickets):
            if s not in g:
                g[s] = [a]  
            else: g[s].append(a)

        for k,v in g.items():
            v.sort()

        path = []
        def dfs(s):
            nonlocal path
            if s in g:
                while g[s]: 
                    dfs(g[s].pop(0))   
            path+=[s]

        dfs("JFK")
        return path[::-1]
```

比较这种解法的List排序的方法

```text
class Solution:
    def findItinerary(self, tickets: List[List[str]]) -> List[str]:
        g = {}
        for s,a in sorted(tickets)[::-1]:#倒序
            if s not in g:
                g[s] = [a]  
            else: g[s].append(a)

        # for k,v in g.items():
        #     v.sort()

        path = []
        def dfs(s):
            nonlocal path
            if s in g:
                while g[s]: 
                    dfs(g[s].pop())   #不是pop(0)
            path+=[s]

        dfs("JFK")
        return path[::-1]
```

