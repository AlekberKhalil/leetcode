# Sqrt\(x\)

Implement`int sqrt(int x)`.

Compute and return the square root ofx.

分析

1 .用long 表示start, end.

2.结果&lt;=x,不是==x

3.先移动start 还是end?只能移动s，e不行.可能是因为while里先移动e的话条件是m \* m &gt;= x.但是最后的答案是需要m \* m &lt;= x。所以需要先移动s。下次做二分先移动哪个需要看题目的条件。

答案

```text
class Solution {    public int mySqrt(int x) {       if(x == 0)           return 0;        long s = 1, e = x;        while(s + 1 < e){            long m = s + (e - s) / 2;            if(m * m <= x){                s = m;            }else{                e = m;            }        }//此处先判断s的话也行        if(e * e <= x){            return (int)e;        }        return (int)s;    }}
```

用花花模板，只能闭区间，开区间那个不行

用m &gt; x / m 不用m\*m&gt;x是为了防止溢出，不过Python没事

```text
class Solution:    def mySqrt(self, x: int) -> int:        l,r = 1,x        while l <= r:            m = l + (r-l)//2 #要取整数，得到是上限，结果要去1            if m > x / m:                r = m - 1            else:                l = m + 1        return l-1
```

newton

```text
每次用该数和两数的商对半调整 r = (r + x//r) // 2
```

```text
class Solution:    def mySqrt(self, x: int) -> int:                if not x:            return x        r = x        while r*r > x :            r = (r + x//r) // 2        return r
```

