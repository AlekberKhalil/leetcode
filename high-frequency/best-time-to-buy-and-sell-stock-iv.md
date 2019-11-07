# Best Time to Buy and Sell Stock IV

Say you have an array for which the_i\_th element is the price of a given stock on day\_i_.

Design an algorithm to find the maximum profit. You may complete at most`k`transactions.

分析：

动态规划，f\[n\]\[i\] -&gt;n次交易在i天内最大收益。不知道为什么多一层循环j不行, k&gt;len/2之后直接用贪心算法。

```text
class Solution {    public int maxProfit(int k, int[] prices) {        if(prices == null || prices.length == 0)            return 0;        int len = prices.length;        if (k >= len / 2) return quickSolve(prices);        int temp;        int[][] f = new int[k+1][prices.length];        //因为有i-1,k-1 所以都从1开始        for(int n = 1;n<=k;n++){            temp = -prices[0];            for(int i=1;i<prices.length;i++){            //f[k, ii] = max(f[k, ii-1], prices[ii] - prices[jj] + f[k-1, jj]) { jj in range of [0, ii-1] }                f[n][i]=Math.max(f[n][i-1],temp+prices[i]);                temp=Math.max(temp,f[n-1][i]-prices[i]);                            }        }        return f[k][prices.length-1];    }    private int quickSolve(int[] prices) {        int len = prices.length, profit = 0;        for (int i = 1; i < len; i++)            // as long as there is a price gap, we gain a profit.            if (prices[i] > prices[i - 1]) profit += prices[i] - prices[i - 1];        return profit;    }}
```

