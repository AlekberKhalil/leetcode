# Graph and  Search

克隆图

先点后边，hashmap 建立旧点新点映射

拓扑排序

有向图不能用DFS 因为多个点指向一个点，会不断回溯

树BFS vs 图BFS

看是否有左右子树， 图是否有neighbor for 循环

宽度优先搜索不会回溯，每个点只遍历一遍

```text
private String replace(String s, int index, char c) {
        char[] chars = s.toCharArray();
        chars[index] = c;
        return new String(chars);
    }
```

