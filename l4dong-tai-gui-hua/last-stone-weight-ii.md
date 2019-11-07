# Last Stone Weight II

We have a collection of rocks, each rock has a positive integer weight.

Each turn, we choose**any two rocks** and smash them together. Suppose the stones have weights`x`and`y`with`x <= y`. The result of this smash is:

* If

  `x == y`

  , both stones are totally destroyed;

* If

  `x != y`

  , the stone of weight

  `x`

  is totally destroyed, and the stone of weight

  `y`

  has new weight

  `y-x`

  .

At the end, there is at most 1 stone left. Return the**smallest possible**weight of this stone \(the weight is 0 if there are no stones left.\)

**Example 1:**

```text
Input: 
[2,7,4,1,8,1]

Output: 
1

Explanation: 

We can combine 2 and 4 to get 2 so the array converts to [2,7,1,8,1] then,
we can combine 7 and 8 to get 1 so the array converts to [2,1,1,1] then,
we can combine 2 and 1 to get 1 so the array converts to [1,1,1] then,
we can combine 1 and 1 to get 0 so the array converts to [1] then that's the optimal value.
```

**Note:**

1. `1`

   `<`

   `= stones.length`

   `<`

   `= 30`

2. `1`

   `<`

   `= stones[i]`

   `<`

   `= 100`

分析

其实就是分成2个尽量大的组，2个sum的diff

看成01背包，分成2个尽量等分背包d。最后就是sum-2\*d.2个等分抵消

记住这里dp\[v\]是bool，表示该数是否可以到达，最后结果是sum-2\*v 开始写成sum-2\*dp\[v \]错半死

```text
class Solution:
    def lastStoneWeightII(self, stones: List[int]) -> int:
        n = len(stones)
        sm = sum(stones)
        sm2 = sm//2
        mx = float('-inf')
        dp = [0]*(sm2+1)
        dp[0] = True
        # mindiff = float('inf')
        for i in range(n):
            for v in range(sm2,stones[i]-1,-1):
                dp[v] |= dp[v-stones[i]]
                if dp[v]:
                    mx = max(mx, v)

        return sm - 2*mx
```

本题也可以看成2个group A,B ,2个组和的diff, res=abs\( A-B\)。 所以当前元素入A就+ 入B就-。最后取正数

记住set的相加就是\|

```text
class Solution:
    def lastStoneWeightII(self, stones: List[int]) -> int:
        n = len(stones)
        dp ={0}
        for i in range(n):
            dp = {x-stones[i] for x in dp} | {x+stones[i] for x in dp} #2种可能性都要加入

        return min(abs(x) for x in dp)
```

