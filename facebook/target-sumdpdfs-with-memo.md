# Target Sum\(01背包dp,dfs with memo\)

You are given a list of non-negative integers, a1, a2, ..., an, and a target, S. Now you have 2 symbols`+`and`-`. For each integer, you should choose one from`+`and`-`as its new symbol.

Find out how many ways to assign symbols to make sum of integers equal to target S.

**Example 1:**

```text
Input: nums is [1, 1, 1, 1, 1], S is 3. Output: 5Explanation:-1+1+1+1+1 = 3+1-1+1+1+1 = 3+1+1-1+1+1 = 3+1+1+1-1+1 = 3+1+1+1+1-1 = 3There are 5 ways to assign symbols to make the sum of nums be target 3
```

分析

求方案总数的01背包问题：[https://www.kancloud.cn/kancloud/pack/70133](https://www.kancloud.cn/kancloud/pack/70133)

`f[i][v]=sum{f[i-1][v],f[i][v-c[i]]}`

初始条件f\[0\]\[0\]=1。

其实就是**01背包问题**。取不取dp\[i\]\[j+/-value\] 这里因为j-value会有负数，所以**平移** 0&lt;=j&lt;=2sum

初始化dp\[0\]\[sum\]= 1 其实这里sum代表了起始0点，然后往左0和往右2sum。0数 = 0的确是一种

这里算出来所有的sum，然后结果取到S即可。记住这里起始点是sum， 所以是sum+S

这里背包容量V= 2\*sum，所以target是sum+S

```text
class Solution:    def findTargetSumWays(self, nums, S):        """        :type nums: List[int]        :type S: int        :rtype: int        """        n = len(nums)        if n == 0:            return 0        ss = sum(nums)        if( S>ss or S<-ss) :            return 0        ssum = ss*2        dp = [[0] * (ssum+1) for _ in range(n + 1)]        dp[0][ss] = 1        for i in range(1, n + 1):            for j in range(0, ssum+1):                if j - nums[i - 1]>=0:                    dp[i][j] = dp[i - 1][j - nums[i - 1]]                if j + nums[i - 1] <= ssum:                    dp[i][j] += dp[i - 1][j + nums[i - 1]]        return dp[n][S+ss]
```

dfs with memo

记住判断map的key是否存在 是key in dict，不是dict\[key\]或者Get\(key\)

```text
class Solution:    def findTargetSumWays(self, nums, S):        """        :type nums: List[int]        :type S: int        :rtype: int        """        n = len(nums)        d = {}        return self.dfs(nums,0,S,0,d)    def dfs(self,nums,sum,S,pos,d):        if (pos, sum) in d:            return d.get((pos,sum))        if pos == len(nums):            return 1 if S ==sum else 0        l =  self.dfs(nums,sum-nums[pos],S,pos+1,d)        r =  self.dfs(nums,sum+nums[pos],S,pos+1,d)        cur = l+r        d[(pos,sum)] = cur        return cur
```

这是01背包**方案数**： f\[i\]\[v\]=sum{f\[i-1\]\[v\],f\[i\]\[v-c\[i\]\]} 初始化f\[0\]\[0\]=1 联想答案都是前面相加，总得有个初始点给出数值。

这里难点是target，做法1的target 是把array分成p,q两段，所以相加是all，q不取p是取，所以相减是S

方案数最后的target/背包大小都要/2?

网上做法1

```text
class Solution(object):    def findTargetSumWays(self, nums, S):        s = sum(nums)        N = s+S        if N%2 or S>s: return 0        N = N//2        dp = [0 for _ in xrange(N+1)]        dp[0] = 1        for num in nums:            for i in xrange(N, num-1, -1):                dp[i] += dp[i-num]        return dp[-1]        #01 knapsack        # sum(p) - sum(q) = S        # sum(p) + sum(q) = sum(all)        # sum(p) = (sum(all) + S)/2
```

网上做法2

```text
#include <vector>#include <numeric>using namespace std;class Solution {public:    int findTargetSumWays(vector<int>& nums, int S) {        int sum = accumulate(nums.begin(), nums.end(), 0);        if (S > sum || S < -sum || S + sum < 0 || (S + sum) % 2 == 1) {            return 0;        }        int target = (S + sum) / 2;        int n = nums.size();        vector<vector<int>> dp(n + 1, vector<int>(target + 1, 0));        dp[0][0] = 1;        for (int i = 1; i <= n; ++i) {            for (int j = 0; j <= target; ++j) {                dp[i][j] = dp[i - 1][j];                if (nums[i - 1] <= j) {                    dp[i][j] += dp[i - 1][j - nums[i - 1]];                }            }        }        return dp[n][target];    }};#if DEBUGint main(int argc, char** argv) {    return 0;}#endif
```

