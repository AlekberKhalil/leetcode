# Nested List Weight Sum II

Given a nested list of integers, return the sum of all integers in the list weighted by their depth.

Each element is either an integer, or a list -- whose elements may also be integers or other lists.

Different from the[previous question](https://leetcode.com/problems/nested-list-weight-sum/)where weight is increasing from root to leaf, now the weight is defined from bottom up. i.e., the leaf level integers have weight 1, and the root level integers have the largest weight.

**Example 1:**

```text
Input: [[1,1],2,[1,1]]Output: 8 Explanation: Four 1's at depth 1, one 2 at depth 2.
```

**Example 2:**

```text
Input: [1,[4,[6]]]Output: 17 Explanation: One 1 at depth 3, one 4 at depth 2, and one 6 at depth 1; 1*3 + 4*2 + 6*1 = 17.
```

分析

和第一题比就是level倒了

bfs，每次叠加第一层的level sum 这样就不用\*level了

```text
class Solution:    def depthSumInverse(self, nestedList: List[NestedInteger]) -> int:        if not nestedList:            return 0        subsum = res = 0        while nestedList:            size = len(nestedList)            q =[]            for i in nestedList:                                if i.isInteger():                    subsum += i.getInteger()                else:                    q += i.getList()            res += subsum            nestedList = q        return res
```

dfs:先dfs计算depth，再用depth再dfs计算sum

```text
class Solution:    def depthSumInverse(self, nestedList: List[NestedInteger]) -> int:        d = self.depth(nestedList)        return self.dfs(nestedList, d)    def dfs(self, nestedList: List[NestedInteger], d:int) ->int:        s= 0        for i in nestedList:            if i.isInteger():                s+=i.getInteger()*d             else:                s += self.dfs(i.getList(),d-1)        return s                         def depth(self, nestedList: List[NestedInteger]) -> int:        d = 0        for i in nestedList:            if not i.isInteger():                d = max(d,self.depth(i.getList()))        return 1 + d
```

