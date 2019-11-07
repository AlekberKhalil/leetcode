# Graph Valid Tree\(union find\)

Given`n`nodes labeled from`0`to`n - 1`and a list of`undirected`edges \(each edge is a pair of nodes\), write a function to check whether these edges make up a valid tree.

## Notice

You can assume that no duplicate edges will appear in edges. Since all edges are`undirected`,`[0, 1]`is the same as`[1, 0]`and thus will not appear together in edges.

**Example**

Given`n = 5`and`edges = [[0, 1], [0, 2], [0, 3], [1, 4]]`, return true.

Given`n = 5`and`edges = [[0, 1], [1, 2], [2, 3], [1, 3], [1, 4]]`, return false.

分析

用并查集union find，如果2个点（一条边的2端）已经属于一个集合，则此边连上就变成环了。

```text
public class Solution {    /*     * @param n: An integer     * @param edges: a list of undirected edges     * @return: true if it's a valid tree, or false     */      int[] father;     int find(int x){            if(x == father[x]){                return x;            }            return father[x] = find(father[x]);        }    public boolean validTree(int n, int[][] edges) {        if (n - 1 != edges.length) {            return false;        }        father = new int[n];        for(int i = 0; i < n; i ++){            father[i] = i;        }        for(int[] e : edges){            int root1 = find(e[0]);            int root2 = find(e[1]);            if(root1 == root2){                return false;            }            father[root1] = root2;        }        return true;    }}
```

