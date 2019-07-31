# Best Time to Buy and Sell Stock II

题目：

Say you have an array for which the ith element is the price of a given stock on day i.

Design an algorithm to find the maximum profit. You may complete as many transactions as you like \(ie, buy one and sell one share of the stock multiple times\). However, you may not engage in multiple transactions at the same time \(ie, you must sell the stock before you buy again\).

分析：

贪心算法，每次股票上涨都买卖，最后求和就能得到最大利润。

需要注意的一点是，当连续两天上涨的时候，利润依然等于\(p\[2\] - p\[1\]\) + \(p\[3\] - p\[2\]\)。也就是如果在p\[2\]不出手，和卖出再买入，是一样的。

```text
public int maxProfit(int[] prices) {
        // 贪心算法，只要有赚就买
        if(prices == null || prices.length == 0 )
            return 0;
        int diff, profit = 0;//初始化每次都错！！！
        for(int i = 1; i < prices.length; i++){
            diff = prices[i] - prices[i-1];
            if(diff > 0)
                profit += diff;
            }
            return profit;
    }
```

