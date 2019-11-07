# Indeed

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

分析

就是找环，有环就不可以。有序图找环用拓扑排序。无序图找环用并查集。

一个Neighbors的map存node和相应的neighbors。一个Indegree的array存每个点的入度。然后BFS用一个queue

```text
class Solution {
    public boolean canFinish(int numCourses, int[][] prerequisites) {
        Map<Integer, List<Integer>> neighbors = new HashMap<Integer, List<Integer>>();//node and its neighbors
        Queue<Integer> q = new LinkedList<Integer>();//bfs
        int[] indegree = new int[numCourses];//indegree出度
        int cnt = numCourses;
        for(int[] p : prerequisites){
            indegree[p[1]] ++;
            if(neighbors.containsKey(p[0])){
                neighbors.get(p[0]).add(p[1]);
            }else{
                List<Integer> ns = new ArrayList<Integer>();
                ns.add(p[1]);
                neighbors.put(p[0], ns);
            }
        }
        for(int i = 0; i < indegree.length; i ++){
            if(indegree[i] == 0){
                q.offer(i);
            }
        }
        while(!q.isEmpty()){
            int cur = q.poll();
            cnt --;
            if(neighbors.containsKey(cur)){
              for(int i : neighbors.get(cur)){
                indegree[i] --;
                if(indegree[i] == 0){
                    q.offer(i);
                }
            }
            }

        }
        return cnt == 0;
    }
}
```

