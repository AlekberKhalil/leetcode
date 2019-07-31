# Nested List Weight SumII\(dfs,bfs\)

Given a nested list of integers, return the sum of all integers in the list weighted by their depth.

Each element is either an integer, or a list -- whose elements may also be integers or other lists.

Different from the previous question where weight is increasing from root to leaf, now the weight is defined from bottom up. i.e., the leaf level integers have weight 1, and the root level integers have the largest weight.

Example 1:  
Given the list \[\[1,1\],2,\[1,1\]\], return 8. \(four 1's at depth 1, one 2 at depth 2\)

Example 2:  
Given the list \[1,\[4,\[6\]\]\], return 17. \(one 1 at depth 3, one 4 at depth 2, and one 6 at depth 1; 1\_3 + 4\_2 + 6\*1 = 17\)

分析

叶到root的level层数倒过来，用BFS的话就是每层sum之后 最后一个loop res-i就是weight.每层sum\*weight

DFS return \(level,ans\)

```text
"""
This is the interface that allows for creating nested lists.
You should not implement it, or speculate about its implementation

class NestedInteger(object):
    def isInteger(self):
        # @return {boolean} True if this NestedInteger holds a single integer,
        # rather than a nested list.
        if self.

    def getInteger(self):
        # @return {int} the single integer that this NestedInteger holds,
        # if it holds a single integer
        # Return None if this NestedInteger holds a nested list

    def getList(self):
        # @return {NestedInteger[]} the nested list that this NestedInteger holds,
        # if it holds a nested list
        # Return None if this NestedInteger holds a single integer
"""


class Solution(object):
    # @param {NestedInteger[]} nestedList a list of NestedInteger Object
    # @return {int} an integer
    def depthSum(self, nestedList):
        # Write your code here
        return self.dfs(nestedList)[1]

    def dfs(self,nestedList):
        if not nestedList:
            return 0
        curlevel=level=1
        ans = 0
        anslist = []

        for i in nestedList:
            if i.isInteger():
                anslist.append(i.getInteger())
            else:
                ans,level = self.dfs(i.getList())
                curlevel = max(curlevel,level)
                anslist.append(ans)
        return (curlevel,sum(anslist)*curlevel)
```

