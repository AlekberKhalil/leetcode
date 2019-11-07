# Video Stitching

You are given a series of video clips from a sporting event that lasted`T`seconds. These video clips can be overlapping with each other and have varied lengths.

Each video clip`clips[i]` is an interval: it starts at time`clips[i][0]`and ends at time`clips[i][1]`. We can cut these clips into segments freely: for example, a clip`[0, 7]`can be cut into segments `[0, 1] + [1, 3] + [3, 7]`.

Return the minimum number of clips needed so that we can cut the clips into segments that cover the entire sporting event \(`[0, T]`\). If the task is impossible, return`-1`.

**Example 1:**

```text
Input: clips = [[0,2],[4,6],[8,10],[1,9],[1,5],[5,9]], T = 10Output: 3Explanation: We take the clips [0,2], [8,10], [1,9]; a total of 3 clips.Then, we can reconstruct the sporting event as follows:We cut [1,9] into segments [1,2] + [2,8] + [8,9].Now we have segments [0,2] + [2,8] + [8,10] which cover the sporting event [0, 10].
```

**Example 2:**

```text
Input: clips = [[0,1],[1,2]], T = 5Output: -1Explanation: We can't cover [0,5] with only [0,1] and [0,2].
```

**Example 3:**

```text
Input: clips = [[0,1],[6,8],[0,2],[5,6],[0,4],[0,3],[6,7],[1,3],[4,7],[1,4],[2,5],[2,6],[3,4],[4,5],[5,7],[6,9]], T = 9Output: 3Explanation: We can take clips [0,4], [4,7], and [6,9].
```

**Example 4:**

```text
Input: clips = [[0,4],[2,8]], T = 5Output: 2Explanation: Notice you can have extra video after the event ends.
```

```text
Note:1 <= clips.length <= 1000 <= clips[i][0], clips[i][1] <= 1000 <= T <= 100
```

分析

DP存最小个数：一loop所有长度，内loop所有range,长度在range内的话的dp取最小。

```text
class Solution:    def videoStitching(self, clips: List[List[int]], T: int) -> int:       # clips.sort(key = lambda x:(x[1],x[0])) 可有可无        dp = [float('inf')]* (T+1)        dp[0]=0        for t in range(T+1):                       for s,e in clips:                if s <= t<=e:                    dp[t] = min(dp[t],dp[s]+1)            if dp[t] == float('inf'):                return -1        return dp[-1]
```

dp存最远可达距离

```text
class Solution:    def videoStitching(self, clips: List[List[int]], T: int) -> int:        n = len(clips)        dp = [-1]*(n+1) #最远能到达的距离        dp[0] = 0        for i in range(1,n+1):            for s,e in clips:                               if dp[i-1] >= s:                    dp[i] = max(dp[i],e)            if dp[i] >= T:                return i        return -1
```

贪心

```text
class Solution:    def videoStitching(self, clips: List[List[int]], T: int) -> int:        preend,end,res=-1,0,0        for s,e in sorted(clips):            if s > end or end>= T:                break            if preend < s <= end:                res,preend = res+1,end            end = max(end,e)        return res if end >= T else -1
```

