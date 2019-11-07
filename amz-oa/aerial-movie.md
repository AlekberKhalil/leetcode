# Aerial Movie\(双指针，2sum）

## Description

In order to prevent passengers from being too bored during the flight, LQ Airlines decided to play two movies during the flight. Since the movie cannot be played during the take-off and landing of the aircraft, LQ Airlines must ensure that the`duration of the two movies`to be less than or equal to`the flight duration minus 30 minutes`, and the total length of the two movies should be as long as possible. Now given`t`,the flight duration\(minutes\), and array`dur[]`,the length of movies. Please output the length of the two movies in order of length. If there are multiple groups of the same length, select the one which contains the longest single moive.It is guarantee that there is a least one solution.

30&lt;t&lt;=1000  
dur\[i\]&lt;=1000  
1&lt;=len\(dur\)&lt;=100000

Have you met this question in a real interview?

Yes

Problem Correction

## Example

Given`t=87`,`dur=[20,25,19,37]`,return`[20,37]`

```text
Explanation:
87-30=57
20+25=45,57-45=12
20+19=39,57-39=19
20+37=57,57-57=0
25+19=44,57-44=13
25+37=62,57
<
62
19+37=56,57-56=1
```

Given`t=67`,`dur=[20,17,19,18]`,return`[17,20]`

```text
Explanation:
67-30=37
17+20=37,18+19=37
The longest movie in the first group is 20，and 19 in the second grouo, so output`[17,20]`
```

分析

双指针 two sum closest，记得要sort

```text
class Solution:
    """
    @param t: the length of the flight
    @param dur: the length of movies
    @return: output the lengths of two movies
    """
    def aerial_Movie(self, t, dur):
        # Write your code here
        target = t - 30
        if not dur:
            return []
        dur.sort()
        mindiff=float('inf')
        s,e = 0,len(dur)-1
        res = []
        while s < e:
            localsum = dur[s] + dur[e]
            diff = target - localsum
            if diff == 0:
                return [dur[s],dur[e]]
            else:
                if diff < 0:
                    e -= 1
                else:
                    if diff < mindiff:
                        mindiff = diff
                        res = [dur[s],dur[e]]
                    s +=1


        return res
```

