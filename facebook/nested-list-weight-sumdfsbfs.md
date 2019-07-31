# Nested List Weight Sum\(dfs,bfs\)

Given a nested list of integers, return the sum of all integers in the list weighted by their depth. Each element is either an integer, or a list -- whose elements may also be integers or other lists.

## Example

Given the list`[[1,1],2,[1,1]]`, return`10`. \(four 1's at depth 2, one 2 at depth 1, 4 \* 1 \* 2 + 1 \* 2 \* 1 = 10\)  
Given the list`[1,[4,[6]]]`, return`27`. \(one 1 at depth 1, one 4 at depth 2, and one 6 at depth 3; 1 + 4 \* 2 + 6 \* 3 = 27\)

分析

dfs用level做参数

```text
"""
This is the interface that allows for creating nested lists.
You should not implement it, or speculate about its implementation

class NestedInteger(object):
    def isInteger(self):
        # @return {boolean} True if this NestedInteger holds a single integer,
        # rather than a nested list.

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
        return self.dfs(nestedList,1)

    def dfs(self,nestedList,level):
        ans = 0
        if not nestedList:
            return ans

        for i in nestedList:
            if i.isInteger():
                ans+= i.getInteger() * level
            else:
                ans += self.dfs(i.getList(),level+1)
        return ans
```

bfs

```text
"""
This is the interface that allows for creating nested lists.
You should not implement it, or speculate about its implementation

class NestedInteger(object):
    def isInteger(self):
        # @return {boolean} True if this NestedInteger holds a single integer,
        # rather than a nested list.

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
        q = [i for i in nestedList]
        level = 1
        ans = 0
        while q:
            n = len(q)
            for i in range(n):
                cur = q.pop(0)
                if cur.isInteger():
                    ans+=cur.getInteger()*level
                else:
                    for i in cur.getList():
                        q.append(i)
            level+=1
        return ans
```

