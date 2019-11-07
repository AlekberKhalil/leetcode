# Max Pair双指针

## Description

Give two Lists, give a maximum value, find a bunch in each of the two lists, and find all the pairs that are closest to the maximum but not larger than the maximum.

The length of the two lists do not exceed100000100000.  
Each element do not exceed10000000001000000000.

Have you met this question in a real interview?

Yes

Problem Correction

## Example

Give`a=[2,3,4,5,6], b=[4,5,7], x=8'`, return`[[3,5],[4,4]]`.

```text
Explanation:
the sum of [3,5] or [4,4] is 8, which is no larger than 8.
```

Give`a=[2,3,4,5,6], b=[4,5,7], x=10'`, return`[[3,7],[5,5],[6,4]]`.

```text
Explanation:
the sum of [3,7],[5,5],[6,4] is 10, which is no larger than 10.
```

分析

还是都排序， start从a头走，end 从B尾走。判断3个 target =&gt;&lt; subsum,同时每个里面根据diff和Mindiff决定 是新res 还是append res

```text
class Solution:
    """
    @param a: the first list
    @param b: the second list
    @param x: the max sum
    @return: the pairs whose sum are not exceed x
    """
    def getAns(self, a, b, x):
        # Write your code here.
        a.sort()
        b.sort()
        s = 0
        e = len(b) - 1

        res = []
        mindiff = float('inf')
        while s < len(a) and e >= 0:
            subsum = a[s] + b[e]           
            d = x - subsum
            if d == 0:
                if d == mindiff:
                    res.append([a[s] , b[e]])
                else:
                    res = [[a[s] , b[e]]]
                    mindiff = d

                s+=1 
                e-=1

            elif d > 0:
                if d < mindiff:
                    res = [[a[s] , b[e]]]
                    mindiff = d
                elif d == mindiff:
                    res.append([a[s] , b[e]])
                s += 1

            else:
                e -= 1


        return res
```

