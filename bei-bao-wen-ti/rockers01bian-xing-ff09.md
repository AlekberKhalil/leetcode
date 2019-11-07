# Rockers（01变形）

You just inherited the rights to N \(1 &lt;= N &lt;= 20\) previously unreleased songs recorded by the popular group Raucous Rockers. You plan to release a set of M \(1 &lt;= M &lt;= 20\) compact disks with a selection of these songs. Each disk can hold a maximum of T \(1 &lt;= T &lt;= 20\) minutes of music, and a song can not overlap from one disk to another.

Since you are a classical music fan and have no way to judge the artistic merits of these songs, you decide on the following criteria for making the selection:

* The songs on the set of disks must appear in the order of the dates that they were written.
* The total number of songs included will be maximized.

## PROGRAM NAME: rockers

## INPUT FORMAT

| Line 1: | Three integers: N, T, and M. |
| :--- | :--- |
| Line 2: | N integers that are the lengths of the songs ordered by the date they were written. |

## SAMPLE INPUT \(file rockers.in\)

```text
4 5 2
4 3 4 2
```

## OUTPUT FORMAT

A single line with an integer that is the number of songs that will fit on M disks.

## SAMPLE OUTPUT \(file rockers.out\)

```text
3
```

分析

这里value直接用总数M\*T。jump函数如果reminder能用就用当前，不够的话就从前盘开始。一定记得是回退前盘不是前进后盘。因为状态只能&lt;=当前，不行就回退。

```text
# Line 1:    Three integers: N, T, and M.
# Line 2:    N integers that are the lengths of the songs ordered by the date they were written.
class Rocker:
    def jump(self,song,val,T):
        if song > val:
            return -1
        return val-song if val%T >= song else (val//T) * T-song
    def maxSong(self,N,T,M,songs):
        val = M*T
        f=[0]*(val+1)

        for i in range(N):
            for j in range(val,songs[i]-1,-1):
                index = self.jump(songs[i],j,T)
                f[j] = max(f[j],f[index]+1 if index>=0 else 0)
        return f[val]
```

