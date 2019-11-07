# Reaching Points

A move consists of taking a point `(x, y)` and transforming it to either `(x, x+y)` or `(x+y, y)`.

Given a starting point `(sx, sy)` and a target point `(tx, ty)`, return `True` if and only if a sequence of moves exists to transform the point `(sx, sy)` to `(tx, ty)`. Otherwise, return `False`.

#### Example

**Example 1:**

```text
Input: sx = 1, sy = 1, tx = 3, ty = 5Output: TrueExplanation:One series of moves that transforms the starting point to the target is:(1, 1) -> (1, 2)(1, 2) -> (3, 2)(3, 2) -> (3, 5)
```

**Example 2:**

```text
Input: sx = 1, sy = 1, tx = 2, ty = 2Output: False
```

**Example 3:**

```text
Input: sx = 1, sy = 1, tx = 1, ty = 1Output: True
```

#### Notice

`sx, sy, tx, ty` will all be integers in the range `[1, 10^9]`.

分析

不断%=更小的数字直到sx或sy，最后判断 \(tx-sy\)%sx

```text
class Solution:    """    @param sx: x for starting point    @param sy: y for starting point    @param tx: x for target point     @param ty: y for target point    @return: if a sequence of moves exists to transform the point (sx, sy) to (tx, ty)    """        def reachingPoints(self, sx, sy, tx, ty):        # write your code here        while sx < tx and sy < ty:            if tx < ty:                ty %= tx            else:                tx %= ty                        # return sx == tx and (ty-sx)%sy == 0 or sy == ty and (tx-sy)%sx == 0        return sx == tx and (ty-sy)%sx == 0 or sy == ty and (tx-sx)%sy == 0                            
```



