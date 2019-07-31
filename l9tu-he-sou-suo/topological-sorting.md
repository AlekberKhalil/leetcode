# Topological Sorting

Given an directed graph, a topological order of the graph nodes is defined as follow:

* For each directed edge

  `A -> B`

  in graph, A must before B in the order list.

* The first node in the order can be any node in the graph with no nodes direct to it.

Find any topological order for the given graph.

**Example**

For graph as follow:

![picture](https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcThE9AgZZszyhwe0o9qpp3VyizdIj9kWwMY50HiQEysXvkSLsoZ)

The topological order can be:

```text
[0, 1, 2, 3, 4, 5]
[0, 2, 3, 1, 5, 4]
...
```

分析

用map记录每个Node的入度，然后用queue bfs，入度为0就可以加入result，否则入度减一送回queue继续

```text
/**
 * Definition for Directed graph.
 * class DirectedGraphNode {
 *     int label;
 *     ArrayList<DirectedGraphNode> neighbors;
 *     DirectedGraphNode(int x) { label = x; neighbors = new ArrayList<DirectedGraphNode>(); }
 * };
 */
public class Solution {
    /**
     * @param graph: A list of Directed graph node
     * @return: Any topological order for the given graph.
     */ 

     public ArrayList<DirectedGraphNode> topSort(ArrayList<DirectedGraphNode> graph){
         ArrayList<DirectedGraphNode> ret = new ArrayList<DirectedGraphNode>();
         Map<DirectedGraphNode, Integer> in = new HashMap<DirectedGraphNode, Integer>();
         Queue<DirectedGraphNode> q = new LinkedList<DirectedGraphNode>();

         for(DirectedGraphNode cur : graph){
             //in.put(cur, 0);

             q.offer(cur);//入度为0压入q

             if(cur.neighbors != null){
                 for(DirectedGraphNode n : cur.neighbors){
                     if(in.containsKey(n)){
                         in.put(n, in.get(n) + 1);
                     }else{
                         in.put(n, 1);
                     }
                 }
             }
         }


         while(!q.isEmpty()){//这里bfs的q有出栈入栈操作，后面的course schedule就没有 ，只有入度为0才能入q          
             DirectedGraphNode cur = q.poll();
             if(!in.containsKey(cur) || in.get(cur) == 0){
                 ret.add(cur);
                 for(DirectedGraphNode n : cur.neighbors){
                     in.put(n, in.get(n) - 1);
                 }
             }else{
                 q.offer(cur);
             }
         }

         return ret;

     }

    // public ArrayList<DirectedGraphNode> topSort(ArrayList<DirectedGraphNode> graph) {
    //     // write your code here
    //     ArrayList<DirectedGraphNode> ret = new ArrayList<DirectedGraphNode>();
    //     HashMap<DirectedGraphNode, Integer> map = new HashMap<DirectedGraphNode, Integer>();

    //     //每个点的入度用Map来存
    //     for(DirectedGraphNode n : graph){
    //         for(DirectedGraphNode neighbor : n.neighbors){
    //             if(!map.containsKey(neighbor)){
    //             map.put(neighbor, 1);
    //         }
    //         else{
    //             map.put(neighbor, map.get(neighbor)+1);//注意此处map里value如何更新，要重新Put入，而且不可以用++
    //         }
    //         }
    //     }

    //     //比起往常的第一个Node入queue，此处给了所有Node的list，所以先把入度为0的点都加入queue
    //     Queue<DirectedGraphNode> q = new LinkedList<DirectedGraphNode>();
    //     for(DirectedGraphNode n : graph){
    //         if(!map.containsKey(n)){
    //             q.offer(n);

    //         }
    //     }

    //   //在queue里，每次减少入度，只有入度为0才可入queue，最后存入结果。
    //     while(!q.isEmpty()){
    //         DirectedGraphNode cur = q.poll();
    //         ret.add(cur);
    //         for(DirectedGraphNode neighbor : cur.neighbors){
    //             map.put(neighbor, map.get(neighbor)-1);
    //             if(map.get(neighbor) == 0){
    //                 q.offer(neighbor);
    //             }
    //         }
    //     }

    //     return ret;
    // }
}
```

