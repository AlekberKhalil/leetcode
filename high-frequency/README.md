# High Frequency

XOR ^

a^a=0 相同数异或会抵消,两两抵消

0^a = a

满足交换律和结合律 a^b = b^a a^\(b^c\)=\(a^b\)^c

\(c-1\)&c 去掉最后一个1

c - \(c-1\)&c得到最后一个1

```text
bitwise note
num | (1<<k): set num's k-th bit as 1
num & (1<<k): get num's k-th bit

int prev = s ^ (1 << j);
```

Subarray

_**凡是和subarray子数组相关的问题，都要想到子数组和是俩前缀和相减（惯用套路）nums\[i...j\] = sum\[j\]-sum\[i-1\]**_

subarray sum用hashmap 存sum\[i\] -- target-sum\[i\]， 但是closest不能用hash， hash只能精确相等

头尾指针比较交换: 排序，头尾指针 A\[s\] +A\[e\] 比较 target 太大就移动尾巴 太小就移动头指针 o\(1\)space o\(logn\) time

power\(x,n\)

x^n = \(x^\(n/2\)\)^2 快速幂 -&gt;o（logn）

在L7数组里有总结maximum subarray 和 stock buy and sell的动归总结

3sum问题：

重复的：用counter map和排列组合公式，3个if条件 1=2=3 1=2！=3 1&lt;3 and 2&lt;3

不重复的：排序，for loop只到i-2，每次比较i!=i-1

