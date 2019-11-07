# L9\_图和搜索\(拓扑，DFS,BFS\)

**BFS**

一直需要判断

每次while+for loop,那个for loop为了得到当前层,word ladder2没用for loop,1有

BFS不回溯，DFS会

DFS不打算用回前面的字母，比如permutation,而是顺序向前的话，就用pos

用DFS解决的问题都可以用BFS

BFS按一层层来，适合有目标求最短路的步数，比如最小不熟，最少交换次数。层数就代表步数 word ladder。

因为BFS离根很近，所以遇到一个解一定是最优解，搜索可以停止。DFS要搜索完了才能知道最近的。

DFS用于连通性问题，容易爆栈。DFS不保存搜索状态，省空间。要搜索全部解用DFS省空间。

能用BFS就BFS，不行就DFS

二维数组N&lt;20的，可用DFS

_这里的bfs的q可以用while和pop【0】_

_或者 for cur in q,就不用pop\[0\]_

**拓扑：**

一定要判断 numCourses == len\(q\)!!!!!! Course Schedule II

1. 三个元素，2个链表一个Map，图\(邻接链表，像每个桶里装数组，arraylist的数组），入度\(int\[\]或者map\)，q\(queue或者arraylist，这里可能linkedlist可以所以arraylist也可以）
2. 填充图，入度和Q。初始化图，就是遍历所有元素都建立一个对应链表。计算入度
3. **入度为0的放入q里，将来遍历也是入度为0就进入bfs。或者都进入Q，然后for loop里每次入Q和出Q。**

   遍历q，把每个元素对应的链表再遍历

4. 模板

alien dict

```text
from heapq import *
class Solution:
    """
    @param words: a list of words
    @return: a string which is correct order
    """
    def alienOrder(self, words):
        # Construct Graph
        in_degree = {ch: 0 for word in words for ch in word}
        neighbors = {ch: [] for word in words for ch in word}
        for pos in range(len(words) - 1):
            for i in range(min(len(words[pos]), len(words[pos+1]))):
                pre, next = words[pos][i], words[pos+1][i]
                if pre != next:
                    in_degree[next] += 1
                    neighbors[pre].append(next)
                    break

        # Topological Sort
        heap = [ch for ch in in_degree if in_degree[ch] == 0]
        heapify(heap)
        order = []
        while heap:
            for _ in range(len(heap)):
                ch = heappop(heap)
                order.append(ch)
                for child in neighbors[ch]:
                    in_degree[child] -= 1
                    if in_degree[child] == 0:
                        heappush(heap, child)

        # order is invalid
        if len(order) != len(in_degree):
            return ""
        return ''.join(order)
```

**查环**

有序用_拓扑排序_： **BFS之后如果还有入度in degree &gt; 0的，就有环。后面题目是入度为0就进入q，q.size\(\) ==n 判断是否有环。**

无序用_并查集union find._

Bottom up 好像就是几个for loop的DP一点点加起来

Top down 就是递归或DFS，慢慢减，可以每次用数组或者Map记录中间结果，就变成记忆化。

**BFS Python 快速写法**

K是层数。这里q不pop，每次q都是该层，记得初始visited就要加入q

```text
while K:
            q = [i for j in q for i in m[j] if i not in seen]
            seen |= set(q)
            K -= 1
```

**ballman**

更新v-1次得到最短距离，比较慢。有负权值的使用它，否则就**Dijkstra。** 因为得到最优值要loop v-1次，该题要求k次，所以不一定有解。Cheapest Flights Within K Stops

