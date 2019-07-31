# Best Time to Buy and Sell Stock III

题目：

Say you have an array for which the ith element is the price of a given stock on day i.

Design an algorithm to find the maximum profit. You may complete at most two transactions.

分析：

这题目中谈到了两次transaction，而且要求两次transaction不overlap，所以应该认为他是一道forward-backward traversal的题目，正着找每次交易的profit，反着再找一次，最后循环所有交易看最大利润出现在哪里。

不懂为什么此处可以用left\[i-1\]来得到最大值，但是Maximum Subarray II不可以，所以同意采用Maximum Subarray II中做法。

解答：

```text
public int maxProfit(int[] prices) {
        // write your code here
        if(prices == null || prices.length == 0 )
            return 0;
        int minPrice = prices[0];//初始化又错了！！！
        int[] left = new int[prices.length];
        for(int i = 1; i < prices.length; i++){
            left[i] = Math.max(prices[i] - minPrice, left[i-1]);//还是选择前i个最大的利润
            minPrice = Math.min(minPrice, prices[i]);
        }

         int[] right = new int[prices.length];
         int maxPrice = prices[prices.length-1];
        for(int i = prices.length-2; i >= 0; i--){
            right[i] = Math.max(maxPrice - prices[i], right[i+1]);
            maxPrice = Math.max(maxPrice, prices[i]);
        }

        int ret = 0;
        for(int i = 0; i < prices.length; i++){
            ret = Math.max(ret, left[i] + right[i]);
        }
        return ret;
    }
```

