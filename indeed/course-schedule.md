# Course Schedule\(拓扑）

There are a total ofncourses you have to take, labeled from`0`to`n - 1`.

Some courses may have prerequisites, for example to take course 0 you have to first take course 1, which is expressed as a pair:`[0,1]`

Given the total number of courses and a list of prerequisite**pairs**, is it possible for you to finish all courses?

For example:

```text
2, [[1,0]]
```

There are a total of 2 courses to take. To take course 1 you should have finished course 0. So it is possible.

```text
2, [[1,0],[0,1]]
```

There are a total of 2 courses to take. To take course 1 you should have finished course 0, and to take course 0 you should also have finished course 1. So it is impossible.

**Note:**

1. The input prerequisites is a graph represented by **a list of edges** ,not adjacency matrices. Read more about

   [how a graph is represented](https://www.khanacademy.org/computing/computer-science/algorithms/graph-representation/a/representing-graphs)

2. You may assume that there are no duplicate edges in the input prerequisites.

**Hints:**

1. This problem is equivalent to finding if a cycle exists in a directed graph. If a cycle exists, no topological ordering exists and therefore it will be impossible to take all courses.
2. [Topological Sort via DFS](https://class.coursera.org/algo-003/lecture/52)
   * A great video tutorial \(21 minutes\) on Coursera explaining the basic concepts of Topological Sort.
3. Topological sort could also be done via

   [BFS](https://en.wikipedia.org/wiki/Topological_sorting#Algorithms)

分析

有序图用拓扑排序检查是否有环，无序图用并查集。注意这里课程是反序input。

用一个map存node和它的neighbors们List，一个数组存入度。然后BFS，用一个Queue.最后若是所有数组都遍历到，则无环。

有环的话入度不为0不会被加入queue,所以不可达。

```text
class Solution {    public boolean canFinish(int numCourses, int[][] prerequisites) {        Map<Integer, List<Integer>> neighbors = new HashMap<Integer, List<Integer>>();//node and its neighbors        Queue<Integer> q = new LinkedList<Integer>();//bfs        int[] indegree = new int[numCourses];//indegree出度        int cnt = numCourses;        for(int[] p : prerequisites){            indegree[p[0]] ++;            if(neighbors.containsKey(p[1])){                neighbors.get(p[1]).add(p[0]);            }else{                List<Integer> ns = new ArrayList<Integer>();                ns.add(p[0]);                neighbors.put(p[1], ns);            }        }        for(int i = 0; i < indegree.length; i ++){            if(indegree[i] == 0){                q.offer(i);            }        }        while(!q.isEmpty()){            int cur = q.poll();            cnt --;            if(neighbors.containsKey(cur)){              for(int i : neighbors.get(cur)){                indegree[i] --;                if(indegree[i] == 0){                    q.offer(i);                }            }            }        }        return cnt == 0;    }}
```

