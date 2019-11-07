# Russian Doll Envelopes

You have a number of envelopes with widths and heights given as a pair of integers`(w, h)`. One envelope can fit into another if and only if both the width and height of one envelope is greater than the width and height of the other envelope.

What is the maximum number of envelopes can you Russian doll? \(put one inside other\)

**Note:**  
Rotation is not allowed.

**Example:**

```text
Input: [[5,4],[6,4],[6,7],[2,3]]Output: 3 Explanation: The maximum number of envelopes you can Russian doll is 3 ([2,3] => [5,4] => [6,7]).
```

分析

1 像LIS，可以按w排序后，双重循环，但是python超时

2 按w正序排序，h**反向排序**，因为\(3,4\),\(3,5\) 如果4在前就会重复计算，5在前的话，4就不会再被计算

3 这里又用到了二分寻找位置，决定是否加入当前数组。长度增加就加入，不增加就更新当前位置元素。

4 dp这里存的是某位置最大的height。

```text
class Solution:    def maxEnvelopes(self, envelopes: List[List[int]]) -> int:        envelopes.sort(key = lambda x : (x[0],-x[1]))        n = len(envelopes)        dp = []        res = 0        for w,h in envelopes:            ind = bisect.bisect_left(dp,h)            if ind == len(dp):                dp.append(h)                res+=1            else:                dp[ind] = h        return res
```

