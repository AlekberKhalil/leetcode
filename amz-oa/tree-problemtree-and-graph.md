# Tree problem\(Tree & Graph\)

## Tree problem

Given a tree of`n`nodes. The`ith`node's father is`fa[i-1]`and the value of the`ith`node is`val[i-1]`. Especially,`1`represents the root,`2`represents the second node and so on. We gurantee that`-1`is the father of root\(the first node\) which means that`fa[0] = -1`.  
The average value of a subtree is the result of the sum of all nodes in the subtree divide by the number of nodes in it.  
Find the maximum average value of the subtrees in the given tree, return the number which represents the root of the subtree.

## Example

Given`fa=[-1,1,1,2,2,2,3,3]`, representing the father node of each point, and`val=[100,120,80,40,50,60,50,70]`, representing the value of each node, return`1`.

```text
Sample diagram：
                      -1  ------No.1
                    /     \
         No.2 ----1        1---------No.3
               /  |  \     /  \
              2   2   2    3   3
```

```text
No.1 node is (100+120+80+40+50+60+50+70) / 8 = 71.25
No.2 node are (120 + 40 + 50 + 60) / 4 = 67.5
No.3 node are (80+50+70) / 3 = 66.6667
So return 1.
```

## Notice

the number of nodes do not exceed 100000  
If there are more than one subtree meeting the requirement, return the minimum number.

分析

建图，这里graph key:val = parent:list of children

dfs图，返回\[cnt,sum\] 然后不断更新global的 MaxAvg和max index

结果返回max index，注意这里单个节点也要考虑在内。

```text
class Solution:
    """
    @param fa: the father
    @param val: the val
    @return: the biggest node
    """
    maxAvg = float('-inf')
    maxI = -1
    def treeProblem(self, fa, val):
        # Write your code here
        n = len(fa)
        if not n:
            return -1
        graph = {i: [] for i in range(1, n + 1)}
        graph.update({-1: []})
        for i in range(1, n + 1):
            graph[fa[i - 1]].append(i)

        map = {}
        self.dfs(graph,-1,val,map)
        return self.maxI

    def dfs(self,graph,i,val,map):

        if i in map:
            return map[i]

        cnt = 1 if i != -1 else 0
        sum = val[i-1] if i != -1 else 0

        for child in graph[i]:
            cres = self.dfs(graph,child,val,map)
            cnt += cres[0]
            sum += cres[1]

        avg = sum/cnt
        if avg > self.maxAvg:
            self.maxAvg = avg
            self.maxI = i

        map[i] = [cnt,sum]

        return map[i]
```

