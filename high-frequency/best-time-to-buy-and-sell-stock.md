# Best Time to Buy and Sell Stock

题目：

Say you have an array for which the ith element is the price of a given stock on day i.

If you were only permitted to complete at most one transaction \(ie, buy one and sell one share of the stock\), design an algorithm to find the maximum profit.

分析：

只要维护minPrice和maxProfit就可以解决问题

解答：

```text
public int maxProfit(int[] prices) {        // write your code here        if(prices == null || prices.length == 0 )        return 0;        int minPrice = Integer.MAX_VALUE, maxP = 0;//初始化每次都错！！！        for(int i = 0; i < prices.length; i++){            maxP = Math.max((prices[i] - minPrice), maxP);            minPrice = Math.min(minPrice, prices[i]);        }        return maxP;    }
```

