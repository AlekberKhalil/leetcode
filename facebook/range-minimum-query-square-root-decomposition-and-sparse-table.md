# Range Minimum Query \(Square Root Decomposition and Sparse Table\)

[https://www.geeksforgeeks.org/range-minimum-query-for-static-array/](https://www.geeksforgeeks.org/range-minimum-query-for-static-array/)

**spare table** is 2D k\*i k = floor\(log size\)

lookuptable 就是I起点 走2^k步，就是1，2，4，8 ....初始化这个表,表里存min的index

query时候就是lookup【l，k】对比lookup\[r-2^k, k\] 这俩range有重叠。 哪个range的min小返回哪个

space o\(n logn\) time o\(1\)

**square root**

分成√n block 每段里有√n个元素。每次就是中间block和头尾2个edge block算

space time o\(√n）

**spare table**

```text
import mathclass Query:    def __init__(self):        self.f = None    def preprocess(self,arr):        n = len(arr)        k = int(math.floor(math.log(n,2)))        f = [[0]*k for _ in range(n)]        for i in range(n):            f[i][0] = i        i,j=0,1        while (1<<j) <=n:            while i+ (1<<j) - 1< n:                f[i][j] = f[i][j - 1] if arr[f[i][j-1]] < arr[f[i+(1<<(j-1))][j-1]] else f[i+(1<<(j-1))][j-1]                i+=1            j+=1        self.f = f    def query(self,arr, l,r):        k = int(math.floor(math.log(r-l+1,2)))        return arr[self.f[l][k]] if arr[self.f[l][k]] <= arr[self.f[r- (1<<k) +1][k]] else arr[self.f[r- (1<<k) +1][k]]    def RMQ(self,arr, queries):        self.preprocess(arr)        for q in queries:            print(self.query(arr,q[0],q[1]))
```

