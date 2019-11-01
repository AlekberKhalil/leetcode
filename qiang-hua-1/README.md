# sweep line & interval

career event:

用（end, duration\)排序，Greedy做法，好多容纳更多event.



代表2段interval有交集。

```text
if (Math.max(b[0], start) < Math.min(b[1], end)) return false;
```

meeting room I II

the skyline problem

merge interval

注意先降后升所以降-1&lt;升+1

interval排序时候，sort默认先按a\[0\]再按a\[1\]（就是都排了）

如果只按start排序，注意要用key

**merge interval** 需要按start sort， end排不排无所谓

**meeting room**需要都排，所以才需要拆成times，先降后升

