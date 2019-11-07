# Sum of Distances in Tree

An undirected, connected tree with`N`nodes labelled`0...N-1`and`N-1edges` are given.

The`i`th edge connects nodes `edges[i][0]`and`edges[i][1]` together.

Return a list`ans`, where`ans[i]`is the sum of the distances between node`i`and all other nodes.

**Example 1:**

```text
Input: N = 6, edges = [[0,1],[0,2],[2,3],[2,4],[2,5]]Output: [8,12,6,10,10,10]Explanation: Here is a diagram of the given tree:  0 / \1   2   /|\  3 4 5We can see that dist(0,1) + dist(0,2) + dist(0,3) + dist(0,4) + dist(0,5)equals 1 + 1 + 2 + 2 + 2 = 8.  Hence, answer[0] = 8, and so on.
```

Note:`1 <= N <= 10000`

分析

count\[i\] i子树里所有点数,加点个数这里是为了对每个点都推进一个距离。

res\[i\]答案 ，在第一层post traversal是得到所有子树到该点距离。

第二层pre traversal更新，联系每次向子点推进，子点往下所有儿子距离-1，子点往上所有父点距离+1

```text
Initial an array count, count[i] counts all nodes in the subtree i.Initial an array of res, res[i] counts sum of distance in subtree i.post:count[root] = sum(count[i]) + 1 为了每次遍历每个子点距离都增加 所以要追踪子点数量。res[root] = sum(res[i]) + sum(count[i]) 每个子点距离都要加一，所以这用sum(count[i])得到所有子点个数n，省略n*1pre:res[i] = res[root] - count[i] + N - count[i]
```

前序遍历得到

