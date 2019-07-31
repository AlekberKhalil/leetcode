# Is Graph Bipartite\(BFS和DFS\)

Given an undirected `graph`, return`true`if and only if it is bipartite.

Recall that a graph is\_bipartite\_if we can split it's set of nodes into two independent subsets A and B such that every edge in the graph has one node in A and another node in B.

The graph is given in the following form:`graph[i]`is a list of indexes`j`for which the edge between nodes`i`and`j`exists. Each node is an integer between`0`and`graph.length - 1`. There are no self edges or parallel edges:`graph[i]`does not contain`i`, and it doesn't contain any element twice.

```text
Example 1:
Input:
 [[1,3], [0,2], [1,3], [0,2]]

Output:
 true

Explanation:

The graph looks like this:
0----1
|    |
|    |
3----2
We can divide the vertices into two groups: {0, 2} and {1, 3}.
```

```text
Example 2:
Input:
 [[1,2,3], [0,2], [0,1,3], [0,2]]

Output:
 false

Explanation:

The graph looks like this:
0----1
| \  |
|  \ |
3----2
We cannot find a way to divide the set of nodes into two independent subsets.
```

Note:

```text
graph will have length in range [1, 100].
graph[i] will contain integers in range [0, graph.length - 1].
graph[i] will not contain i or duplicate values.
The graph is undirected: if any element j is in graph[i], then i will be in graph[j].
```

分析

因为有不可达的离散点，所以DFS BFS都要FOR LOOP来检验那些不可达的点。

BFS

```text
class Solution {
    public boolean isBipartite(int[][] graph) {
        int n = graph.length;
        int[] visited = new int[n];
        for(int i = 0; i < n; i++){
            if(visited[i] == 0){
                Queue<Integer> q = new LinkedList<>();
                visited[i] = 1;
                q.offer(i);
                while(!q.isEmpty()){
                    int cur = q.poll();
                    for(int nb : graph[cur]){
                        if(visited[nb] == 0){
                            visited[nb] = - visited[cur];
                            q.offer(nb);
                        }else if(visited[nb] == visited[cur]){
                            return false;
                        }
                    }
                }
            }
        }
        return true;
    }
}
```

DFS

```text
class Solution {
    public boolean isBipartite(int[][] graph) {
         int n = graph.length;
        int[] visited = new int[n];
        for(int i = 0; i < n; i++){
            if(visited[i] == 0 && !dfs(graph,visited,i,1)){
                return false;
            }
        }
        return true;
    }

    boolean dfs(int[][] graph, int[] visited, int p, int color){
        if(visited[p] != 0){
            return visited[p] == color;
        }
        visited[p] = color;
        for(int nb : graph[p]){
        //比较此处的和BFS， 这里直接判断邻居。BFS需要赋值，存入之类的
            if(!dfs(graph,visited,nb,-color)){             
                return false;
            }
        }
        return true;
    }
}
```

