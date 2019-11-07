# Best Time to Buy and Sell Stock IV

Say you have an array for which theithelement is the price of a given stock on dayi.

Design an algorithm to find the maximum profit. You may complete at most**k**transactions.

**Note:**  
You may not engage in multiple transactions at the same time \(ie, you must sell the stock before you buy again\).

分析

也是维护global max和local max

如果k&gt;=n/2以后，就贪心法做

```text
class Solution {    public int maxProfit(int k, int[] prices) {                int n = prices.length;               if(n< 1)            return 0;        if (k >=  n/2) {            int maxPro = 0;            for (int i = 1; i < n; i++) {                if (prices[i] > prices[i-1])                    maxPro += prices[i] - prices[i-1];            }            return maxPro;        }        int localMax = 0;        int[][] f = new int[n + 1][k + 1];        for(int j = 1; j <= k; j ++){             localMax = f[0][j - 1] - prices[0];//max需要初始化！！！            for(int i = 1; i <= n; i ++){            //这次卖或者不卖，卖的话所以加                f[i][j] = Math.max(f[i - 1][j], prices[i - 1] + localMax);            //之前某次买的，所以要减，这次保存了Local就能省一次loop，有loop的话这里就是f[k][j - 1] - prices[k - 1]k次买的                localMax = Math.max(f[i][j - 1] - prices[i - 1], localMax);            }        }        return f[n][k];        }}
```

