# Minimum Cost For Tickets

In a country popular for train travel, you have planned some train travelling one year in advance. The days of the year that you will travel is given as an array`days`. Each day is an integer from`1`to`365`.

Train tickets are sold in 3 different ways:

* a 1-day pass is sold for

  `costs[0]`

  dollars;

* a 7-day pass is sold for

  `costs[1]`

  dollars;

* a 30-day pass is sold for

  `costs[2]`

  dollars.

The passes allow that many days of consecutive travel. For example, if we get a 7-day pass on day 2, then we can travel for 7 days: day 2, 3, 4, 5, 6, 7, and 8.

Return the minimum number of dollars you need to travel every day in the given list of`days`.

**Example 1:**

```text
Input: days = [1,4,6,7,8,20], costs = [2,7,15]Output: 11Explanation: For example, here is one way to buy passes that lets you travel your travel plan:On day 1, you bought a 1-day pass for costs[0] = $2, which covered day 1.On day 3, you bought a 7-day pass for costs[1] = $7, which covered days 3, 4, ..., 9.On day 20, you bought a 1-day pass for costs[0] = $2, which covered day 20.In total you spent $11 and covered all the days of your travel.
```

**Example 2:**

```text
Input: days = [1,2,3,4,5,6,7,8,9,10,30,31], costs = [2,7,15]Output: 17Explanation: For example, here is one way to buy passes that lets you travel your travel plan:On day 1, you bought a 30-day pass for costs[2] = $15 which covered days 1, 2, ..., 30.On day 31, you bought a 1-day pass for costs[0] = $2 which covered day 31.In total you spent $17 and covered all the days of your travel.
```

**Note:**

```text
1 <= days.length <= 3651 <= days[i] <= 365days is in strictly increasing order.costs.length == 31 <= costs[i] <= 1000
```

分析

分组背包，组loop在v内。这里v是天数，注意不在出差天内不管直接dp\[i\] = dp\[i-1\]

出差天里3个取min。但是这里value在范围外\(负数）可以设置为0

```text
class Solution:    def mincostTickets(self, days: List[int], costs: List[int]) -> int:        n = days[-1]        dp = [float('inf')]*(n+1)         A = [1,7,30]        dp[0] = 0        for d in range(1,n+1):              if d not in days:                dp[d] = dp[d-1] #不在出差天里可以不买票不管。            else:#出差天里必有覆盖                for ind,a in enumerate(A):                      dp[d] = min(dp[d],dp[max(0,d-a)] + costs[ind]) #错在max(0,d-a)， 不能判断d-a>=0才进来算Min,如果不够大直接按0天算。表示覆盖率、        return dp[-1]
```

