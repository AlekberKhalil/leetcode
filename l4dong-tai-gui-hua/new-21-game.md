# New 21 Game

Alice plays the following game, loosely based on the card game "21".

Alice starts with`0`points, and draws numbers while she has less than`K`points. During each draw, she gains an integer number of points randomly from the range`[1, W]`, where`W`is an integer. Each draw is independent and the outcomes have equal probabilities.

Alice stops drawing numbers when she gets`K`or more points. What is the probability that she has`N`or less points?

**Example 1:**

```text
Input: 
N = 10, K = 1, W = 10

Output: 
1.00000

Explanation: 
 Alice gets a single card, then stops.
```

**Example 2:**

```text
Input: 
N = 6, K = 1, W = 10

Output: 
0.60000

Explanation: 
 Alice gets a single card, then stops.
In 6 out of W = 10 possibilities, she is at or below N = 6 points.
```

**Example 3:**

```text
Input: 
N = 21, K = 17, W = 10

Output: 
0.73278
```

**Note:**

```text
0 <= K <= N <= 10000
1 <= W <= 10000
Answers will be accepted as correct if they are within 10^-5 of the correct answer.
The judging time limit has been reduced for this question.
```

分析：

&gt;=K停，K &lt;= N &lt; K+W，概率：范围前0后1

当前数可以从前W个数跳来，如同climbing stair， wsum/w。

K后p\[i\]不增加了。因为不能再多pick了。

```text
class Solution:
    def new21Game(self, N: int, K: int, W: int) -> float:
        if K==0 or N >= K + W:
            return 1 
        p = [1] + [0]*N
        wsum = 1
        for i in range(1,N+1):
            p[i] = wsum/W
            if i < K:
                wsum += p[i] #还可以继续选，所以p一直增加，之后不增了。
            if i >= W:
                wsum -= p[i-W] #可以从前W个数跳过来。
        return sum(p[K:])
```

