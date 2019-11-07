# Best Time to Buy and Sell Stock III

Say you have an array for which theithelement is the price of a given stock on dayi.

Design an algorithm to find the maximum profit. You may complete at mosttwotransactions.

**Note:**  
You may not engage in multiple transactions at the same time \(ie, you must sell the stock before you buy again\).

分析

```text
f[k, ii] represents the max profit up until prices[ii] (Note: NOT ending with prices[ii]) using at most k transactions. f[k, ii] = max(f[k, ii-1], prices[ii] - prices[jj] + f[k-1, jj]) { jj in range of [0, ii-1] }          = max(f[k, ii-1], prices[ii] + max(f[k-1, jj] - prices[jj]))f[0, ii] = 0; 0 times transation makes 0 profitf[k, 0] = 0; if there is only one price data point you can't make any money no matter how many times you can trade
```

记得里面max要初始化

```text
class Solution {    public int maxProfit(int[] prices) {        int K = 2;        int n = prices.length;        int maxPro = 0, max = 0;        int[][] f = new int[n + 1][K + 1];        if(n < 1){            return 0;        }else{            for(int k = 1; k <= K; k ++){                 max = f[0][k - 1] - prices[0];//max需要初始化！！！                for(int i = 1; i <= n; i ++){                    f[i][k] = Math.max(f[i - 1][k], prices[i - 1] + max);                    max = Math.max(f[i][k - 1] - prices[i - 1], max);                    maxPro = Math.max(maxPro, f[i][k]);                }            }        }        return maxPro;    }}
```

代码简化一下，和后面IV一样，维护localMax和globalMax,可以直接返回f\[n\]\[K\]

```text
class Solution {    public int maxProfit(int[] prices) {        int K = 2;        int n = prices.length;        int max = 0;        int[][] f = new int[n + 1][K + 1];        if(n< 1){            return 0;        }        for(int k = 1; k <= K; k ++){             max = f[0][k - 1] - prices[0];//max需要初始化！！！            for(int i = 1; i <= n; i ++){                f[i][k] = Math.max(f[i - 1][k], prices[i - 1] + max);                max = Math.max(f[i][k - 1] - prices[i - 1], max);            }        }        return f[n][K];    }}
```

