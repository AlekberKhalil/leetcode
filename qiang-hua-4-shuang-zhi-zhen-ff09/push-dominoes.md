# Push Dominoes

There are`N`dominoes in a line, and we place each domino vertically upright.

In the beginning, we simultaneously push some of the dominoes either to the left or to the right.

![](https://s3-lc-upload.s3.amazonaws.com/uploads/2018/05/18/domino.png)

After each second, each domino that is falling to the left pushes the adjacent domino on the left.

Similarly, the dominoes falling to the right push their adjacent dominoes standing on the right.

When a vertical domino has dominoes falling on it from both sides, it stays still due to the balance of the forces.

For the purposes of this question, we will consider that a falling domino expends no additional force to a falling or already fallen domino.

Given a string "S" representing the initial state. `S[i] = 'L'`, if the i-th domino has been pushed to the left;`S[i] = 'R'`, if the i-th domino has been pushed to the right;`S[i] = '.'`, if the`i`-th domino has not been pushed.

Return a string representing the final state.

**Example 1:**

```text
Input: 
".L.R...LR..L.."

Output: 
"LL.RR.LLRRLL.."
```

**Example 2:**

```text
Input: 
"RR.L"

Output: 
"RR.L"

Explanation: 
The first domino expends no additional force on the second domino.
```

**Note:**

```text
0 <= N <= 10^5
String dominoes contains only 'L', 'R' and '.'
```

分析

Whether be pushed or not, depend on the shortest distance to 'L' and 'R'.  
Also the direction matters.  
Base on this idea, you can do the same thing inspired by this problem.  
[https://leetcode.com/problems/shortest-distance-to-a-character/discuss/125788/](https://leetcode.com/problems/shortest-distance-to-a-character/discuss/125788/)

Here is another idea that focus on 'L' and 'R'.  
'R......R' =&gt; 'RRRRRRRR'  
'R......L' =&gt; 'RRRRLLLL' or 'RRRR.LLLL'  
'L......R' =&gt; 'L......R'  
'L......L' =&gt; 'LLLLLLLL'

**Time Complexity**:  
O\(N\)

分析

只看L,R，遇到点跳过，根据LR处理点。

中间的点靠近哪个l或者r近就跟哪个，注意方向。

先加入起点LR,不影响res，从1开始loop

1 s=e

2 s = L , e = R

3 s = R, e=L（巧妙用了//2和%2）

```text
class Solution:
    def pushDominoes(self, dominoes: str) -> str:
        d = 'L'+dominoes+'R' #首尾加入多余LR来防越界。
        ll = len(d)
        s=0
        res = []
        for e in range(1,ll):
            if d[e] == '.':
                continue
            mid = e - s - 1 #不包括首尾s,e
            if s: #每次开始加入起点，所以最后多余R不会被加入。
                res.append(d[s])
            if d[s] == d[e]:
                res.append(d[s]*mid)
            elif d[s] == 'L' and d[e] == 'R':
                res.append('.'*mid)
            else:
                res.append('R'*(mid//2) + '.'*(mid%2) + 'L'*(mid//2))

            s = e
        return ''.join(res)
```

