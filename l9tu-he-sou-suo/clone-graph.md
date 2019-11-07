# Clone Graph

Clone an undirected graph. Each node in the graph contains a`label`and a list of its`neighbors`.

**OJ's undirected graph serialization:**

Nodes are labeled uniquely.

We use

`#`

as a separator for each node, and

`,`

as a separator for node label and each neighbor of the node.

As an example, consider the serialized graph`{0,1,2#1,2#2,2}`.

The graph has a total of three nodes, and therefore contains three parts as separated by`#`.

```text
First node is labeled as 0. Connect node 0 to both nodes 1 and 2.Second node is labeled as 1. Connect node 1 to node 2.Third node is labeled as 2. Connect node 2 to node 2 (itself), thus forming a self-cycle.
```

Visually, the graph looks like the following:

```text
       1      / \     /   \    0 --- 2         / \         \_/
```

分析

和前面copy random likedlist 类似，都是先copy原图和现图，把nodes都建立好，用一个map映射新图和旧图。

然后for loop，根据关系再连接新图的关系。

```text
/** * Definition for undirected graph. * class UndirectedGraphNode { *     int label; *     List<UndirectedGraphNode> neighbors; *     UndirectedGraphNode(int x) { label = x; neighbors = new ArrayList<UndirectedGraphNode>(); } * }; */public class Solution {    public UndirectedGraphNode cloneGraph(UndirectedGraphNode node) {        if(node ==  null){            return node;        }        Map<UndirectedGraphNode, UndirectedGraphNode> map = new HashMap<UndirectedGraphNode, UndirectedGraphNode>();        Queue<UndirectedGraphNode> q = new LinkedList<UndirectedGraphNode>();        Map<UndirectedGraphNode, Boolean> visited = new HashMap<UndirectedGraphNode, Boolean>();        q.offer(node);        visited.put(node, true);        while(!q.isEmpty()){            UndirectedGraphNode cur = q.poll();            map.put(cur, new UndirectedGraphNode(cur.label));            for(UndirectedGraphNode n : cur.neighbors){                if(!visited.containsKey(n)){                    visited.put(n, true);                    q.offer(n);                    map.put(n, new UndirectedGraphNode(n.label));                }                           }        }        for(UndirectedGraphNode entry : map.keySet()){            if(entry.neighbors != null){                UndirectedGraphNode nNode = map.get(entry);                nNode.neighbors = new ArrayList<UndirectedGraphNode>();                for(UndirectedGraphNode n : entry.neighbors){                    UndirectedGraphNode nNeighbor = map.get(n);                       nNode.neighbors.add(nNeighbor);                }            }        }       return map.get(node);     }}
```

