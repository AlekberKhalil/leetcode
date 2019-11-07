# L2\_二分查找

[https://algorithm.yuanbin.me/zh-hans/basics\_algorithm/binary\_search.html](https://algorithm.yuanbin.me/zh-hans/basics_algorithm/binary_search.html)

二分里等于的那个头，start或者end，后面后判断。因为等于了还被移动，答案就在另一半了。

二分花花模板，最后返回的L要按条件调整

```text
#左闭右开 [l,r)  注意这里好像r = n+1，但是可能溢出def binarySearch(l,r):    while l < r:        m = l + (r-l)/2        if g(m):             r = m #new range[l,m)        else:            l = m + 1 # new range[m+1,r)    return l#闭合区间 [l,r]def binary_search(l,r):    while l <= r:        m = l + (r-l)/2        if g(m):            r = m - 1        else:            l = m + 1    return l
```

