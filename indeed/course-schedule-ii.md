# Course Schedule II

There are a total ofncourses you have to take, labeled from`0`to`n - 1`.

Some courses may have prerequisites, for example to take course 0 you have to first take course 1, which is expressed as a pair:`[0,1]`

Given the total number of courses and a list of prerequisite**pairs**, return the ordering of courses you should take to finish all courses.

There may be multiple correct orders, you just need to return one of them. If it is impossible to finish all courses, return an empty array.

For example:

```text
2, [[1,0]]
```

There are a total of 2 courses to take. To take course 1 you should have finished course 0. So the correct course order is`[0,1]`

```text
4, [[1,0],[2,0],[3,1],[3,2]]
```

There are a total of 4 courses to take. To take course 3 you should have finished both courses 1 and 2. Both courses 1 and 2 should be taken after you finished course 0. So one correct course order is`[0,1,2,3]`. Another correct ordering is`[0,2,1,3]`.

分析

bfs，注意此处input的课程顺序是反序。visited == numCourses 既用来填充result的下标，也用来判断是否有环。

输出的结果包括所有课程，是图里所有路径而非单条最短路径。

```text
class Solution {    public int[] findOrder(int numCourses, int[][] prerequisites) {        Map<Integer, List<Integer>> neighbors = new HashMap<Integer, List<Integer>>();//node and its neighbors        Queue<Integer> q = new LinkedList<Integer>();//bfs        int[] indegree = new int[numCourses];//indegree出度        int[] ret = new int[numCourses];        for(int[] p : prerequisites){            indegree[p[0]] ++;            if(neighbors.containsKey(p[1])){                neighbors.get(p[1]).add(p[0]);            }else{                List<Integer> ns = new ArrayList<Integer>();                ns.add(p[0]);                neighbors.put(p[1], ns);            }        }        for(int i = 0; i < indegree.length; i ++){            if(indegree[i] == 0){                q.offer(i);            }        }        int visited = 0;        while(!q.isEmpty()){            int cur = q.poll();            ret[visited ++] = cur;            if(neighbors.containsKey(cur)){              for(int i : neighbors.get(cur)){                indegree[i] --;                if(indegree[i] == 0){                    q.offer(i);                }            }            }        }         return visited == numCourses ? ret : new int[0];    }}
```

