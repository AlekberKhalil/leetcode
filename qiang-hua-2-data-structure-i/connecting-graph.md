# Connecting Graph I II III

Connecting graph I

```text
public class ConnectingGraph{    private int[] father = null;    private int find(int x){        if(father[x] == 0)            return x;        return father[x] = find(father[x]);    }    public ConnectingGraph(int n){            father = new int[n+1];            //index从1开始，所以指向0，如果从0开始，则指向自己。            for(int i = 1; i < n; i++){                father[i] = 0;            }    }    public void connect(int a, int b){        int root_a = find(a);        int root_b = find(b);        if(root_a != root_b){            father[root_a] = root_b;        }    }    public boolean query(int a, int b){        int root_a = find(a);        int root_b = find(b);        return root_a == root_b;    }}
```

Connecting graph II

求A所在连通块的节点个数

```text
public class ConnectingGraph{    private int[] father = null;    private int[] size = null;    public int find(int x){        if(father[x] == 0)            return x;        return father[x] = find(father[x]);    }    public ConnectingGraph(int n){            father = new int[n+1];            size = new int[n+1];            //index从1开始，所以指向0，如果从0开始，则指向自己。            for(int i = 1; i < n; i++){                father[i] = 0;                size[i] = 1;            }    }    public void connect(int a, int b){        int root_a = find(a);        int root_b = find(b);        if(root_a != root_b){            father[root_a] = root_b;            size[root_b] += size[root_a];        }    }    public boolean query(int a){        int root_a = find(a);        return size[root_a];    }}
```

Connecting graph III

当前图的连通块的个数

```text
public class ConnectingGraph{    private int[] father = null;    private count;    public int find(int x){        if(father[x] == 0)            return x;        return father[x] = find(father[x]);    }    public ConnectingGraph(int n){            father = new int[n+1];            count = n;            //index从1开始，所以指向0，如果从0开始，则指向自己。            for(int i = 1; i < n; i++){                father[i] = 0;            }    }    public void connect(int a, int b){        int root_a = find(a);        int root_b = find(b);        if(root_a != root_b){            father[root_a] = root_b;            count --;        }    }    public boolean query(){        return count;    }}
```

