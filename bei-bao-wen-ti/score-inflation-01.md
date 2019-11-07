# Score Inflation \(01\)

The more points students score in our contests, the happier we here at the USACO are. We try to design our contests so that people can score as many points as possible, and would like your assistance.

We have several categories from which problems can be chosen, where a "category" is an unlimited set of contest problems which all require the same amount of time to solve and deserve the same number of points for a correct solution. Your task is write a program which tells the USACO staff how many problems from each category to include in a contest so as to maximize the total number of points in the chosen problems while keeping the total solution time within the length of the contest.

The input includes the length of the contest, M \(1 &lt;= M &lt;= 10,000\) \(don't worry, you won't have to compete in the longer contests until training camp\) and N, the number of problem categories, where 1 &lt;= N &lt;= 10,000.

Each of the subsequent N lines contains two integers describing a category: the first integer tells the number of points a problem from that category is worth \(1 &lt;= points &lt;= 10000\); the second tells the number of minutes a problem from that category takes to solve \(1 &lt;= minutes &lt;= 10000\).

Your program should determine the number of problems we should take from each category to make the highest-scoring contest solvable within the length of the contest. Remember, the number from any category can be any nonnegative integer \(0, one, or many\). Calculate the maximum number of possible points.

## PROGRAM NAME: inflate

## INPUT FORMAT

| Line 1: | M, N -- contest minutes and number of problem classes |
| :--- | :--- |
| Lines 2-N+1: | Two integers: the points and minutes for each class |

## SAMPLE INPUT \(file inflate.in\)

```text
300 4
100 60
250 120
120 100
35 20
```

## OUTPUT FORMAT

A single line with the maximum number of points possible given the constraints.

## SAMPLE OUTPUT \(file inflate.out\)

605

分析

为什么time是顺序？？？？？？？？？？？？？？？

```text
class ScoreInflation:
    def maxScore(self,M,N,points,times):
        f = [0]*(M+1)
        for i in range(N):
            for j in range(times[i] ,M+1):
                f[j] = max(f[j], f[j-times[i]]+points[i])
        return f[M]

points = [10,250,120,35]
times = [60,120,100,20]
s = ScoreInflation()
ret = s.maxScore(300,4,points,times)
print(ret)
```

