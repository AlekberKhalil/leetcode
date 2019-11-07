# Best Time to Buy and Sell Stock II

Say you have an array for which theithelement is the price of a given stock on dayi.

Design an algorithm to find the maximum profit. You may complete as many transactions as you like \(ie, buy one and sell one share of the stock multiple times\). However, you may not engage in multiple transactions at the same time \(ie, you must sell the stock before you buy again\).

分析

贪心法，每次有利润就入，就是今天比昨天大。prev = prices\[0\]

```text
class Solution {    public int maxProfit(int[] prices) {        if(prices == null || prices.length == 0)            return 0;        int prev = prices[0];        int sum = 0;        for(int p : prices){            if(p > prev){                sum += p - prev;                           }            prev = p;        }        return sum;    }}
```

