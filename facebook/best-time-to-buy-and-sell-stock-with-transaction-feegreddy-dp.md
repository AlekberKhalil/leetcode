# Best Time to Buy and Sell Stock with Transaction Fee\(greddy, dp\)

Your are given an array of integers`prices`, for which the`i`-th element is the price of a given stock on day`i`; and a non-negative integer`fee`representing a transaction fee.

You may complete as many transactions as you like, but you need to pay the transaction fee for each transaction. You may not buy more than 1 share of a stock at a time \(ie. you must sell the stock share before you buy again.\)

Return the maximum profit you can make.

```text
Input: prices = [1, 3, 2, 8, 4, 9], fee = 2
Output: 8
Explanation: The maximum profit can be achieved by:
Buying at prices[0] = 1
Selling at prices[3] = 8
Buying at prices[4] = 4
Selling at prices[5] = 9
The total profit is ((8 - 1) - 2) + ((9 - 4) - 2) = 8.
```

note

```text
0 < prices.length <= 50000.
0 < prices[i] < 50000.
0 <= fee < 50000.
```

分析

贪心法

```text
. state is a switch variable
. when state >= fee, all incoming positive price movement will become profit
. when state <= 0, that, all incoming negative price movement will be discarded
```

```text
class Solution {
    public int maxProfit(int[] prices, int fee) {
        int ret = 0, state = 0;
        int lastPrice = prices[0];
        for(int i = 1; i < prices.length; i ++){
            state += prices[i] - lastPrice;
            if(state > fee){
                ret += state - fee;
                state = fee;
            }else if(state < 0){
                state = 0;
            }
            lastPrice = prices[i];
        }
        return ret;
    }
}
```

dp:

[https://leetcode.com/problems/best-time-to-buy-and-sell-stock-with-transaction-fee/discuss/136388/Easiest-solution-\(Python\).-O\(n\)-Complexity.-With-Explanation](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-with-transaction-fee/discuss/136388/Easiest-solution-%28Python%29.-O%28n%29-Complexity.-With-Explanation).

```text
hold[i] - the maximum profit you can earn if you have to hold at day[i]
sold[i] - the maximum profit you can earn if you have to sold at day[i]

Formula:
hold[i] = max(hold[i - 1], sold[i - 1] - p[i])       // if hold at [i-1], no op; if sold at [i-1], buy at [i] with cost of p[i];
sold[i] = max(sold[i - 1], hold[i - 1] + p[i] - fee) // if sold at [i-1], no op; if hold at [i-1], sell at [i] with gain of p[i] - fee;

Initialization:
hold[0] = 0 - price[0];  // buy shares with cost of p[0];
sold[0] = 0;             // no op no cost;
```

```text
class Solution {
    public int maxProfit(int[] prices, int fee) {
        int n = prices.length;
        int[] sell= new int[n];
        int[] hold = new int[n];

        hold[0] = -prices[0];
        for(int i = 1; i < n; i ++){
            sell[i] = Math.max(sell[i-1], hold[i-1] + prices[i] - fee);
            hold[i] = Math.max(hold[i-1], sell[i-1] - prices[i]);
        }
        return sell[n-1];
    }
}
```

[https://leetcode.com/problems/best-time-to-buy-and-sell-stock-with-transaction-fee/discuss/108884/JavaC++-Clean-Code-\(DPGreedy](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-with-transaction-fee/discuss/108884/JavaC++-Clean-Code-%28DPGreedy%29\)

股票问题集合

[https://leetcode.com/problems/best-time-to-buy-and-sell-stock-with-transaction-fee/discuss/108870/Most-consistent-ways-of-dealing-with-the-series-of-stock-problems](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-with-transaction-fee/discuss/108870/Most-consistent-ways-of-dealing-with-the-series-of-stock-problems)

