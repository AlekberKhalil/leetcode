# Best Time to Buy and Sell Stock

Say you have an array for which theithelement is the price of a given stock on dayi.

If you were only permitted to complete at most one transaction \(ie, buy one and sell one share of the stock\), design an algorithm to find the maximum profit.

**Example 1:**

```text
Input: [7, 1, 5, 3, 6, 4]Output: 5max. difference = 6-1 = 5 (not 7-1 = 6, as selling price needs to be larger than buying price)
```

**Example 2:**

```text
Input: [7, 6, 4, 3, 1]Output: 0In this case, no transaction is done, i.e. max profit = 0.
```

分析

初始化Min是第一个数，这里不是presum

```text
class Solution {    public int maxProfit(int[] prices) {        if(prices == null || prices.length == 0)            return 0;        int min = prices[0], max = 0;        for(int i = 1; i < prices.length; i ++){            max = Math.max(max, prices[i] - min);            min = Math.min(min, prices[i]);        }        return max;    }}
```

