# Clone Graph\(bfs,dfs\)

Given the head of a graph, return a deep copy \(clone\) of the graph. Each node in the graph contains a`label` \(`int`\) and a list \(`List[UndirectedGraphNode]`\) of its`neighbors`. There is an edge between the given node and each of the nodes in its neighbors.

```text
OJ's undirected graph serialization (so you can understand error output):
Nodes are labeled uniquely.

We use # as a separator for each node, and , as a separator for node label and each neighbor of the node.


As an example, consider the serialized graph {0,1,2#1,2#2,2}.

The graph has a total of three nodes, and therefore contains three parts as separated by #.

First node is labeled as 0. Connect node 0 to both nodes 1 and 2.
Second node is labeled as 1. Connect node 1 to node 2.
Third node is labeled as 2. Connect node 2 to node 2 (itself), thus forming a self-cycle.
```

Visually, the graph looks like the following:

```text
       1
      / \
     /   \
    0 --- 2
         / \
         \_/
```

**Note**: The information about the tree serialization is only meant so that you can understand error output if you get a wrong answer. You don't need to understand the serialization to solve the problem.

分析

先复制离散点，建立新旧点map，用visited去重

连新点的neighbor

```text
# Definition for a undirected graph node
# class UndirectedGraphNode:
#     def __init__(self, x):
#         self.label = x
#         self.neighbors = []
import collections


class Solution:
    # @param node, a undirected graph node
    # @return a undirected graph node
    def cloneGraph(self, node):
        if not node:
            return node
        q = [node]
        visited = [node]
        dict=collections.defaultdict(UndirectedGraphNode)
        while q:
            cur = q.pop(0)
            dict[cur] = UndirectedGraphNode(cur.label)
            for n in cur.neighbors:
                if n not in visited:
                    q.append(n)
                    visited.append(n)

        for k in dict.keys():
            if k.neighbors:
                for n in k.neighbors:
                    dict[k].neighbors.append(dict[n])

        return dict[node]
```

dfs, 每次要么返回map里的新值，要不建新Node，然后赋neighbors（调用子dfs\)

```text
# Definition for a undirected graph node
# class UndirectedGraphNode:
#     def __init__(self, x):
#         self.label = x
#         self.neighbors = []

class Solution:
    # @param node, a undirected graph node
    # @return a undirected graph node
    def cloneGraph(self, node):
        if not node:
            return node
        visited = {}
        return self.copy(node,visited)

    def copy(self,node,visited):
        if node in visited:
            return visited[node]
        visited[node] = UndirectedGraphNode(node.label)
        visited[node].neighbors = [self.copy(x,visited) for x in node.neighbors]
        return visited[node]
```

