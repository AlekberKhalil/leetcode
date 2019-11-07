# 4 Keys Keyboard

Imagine you have a special keyboard with the following keys:

`Key 1: (A)`: Print one 'A' on screen.

`Key 2: (Ctrl-A)`: Select the whole screen.

`Key 3: (Ctrl-C)`: Copy selection to buffer.

`Key 4: (Ctrl-V)`: Print buffer on screen appending it after what has already been printed.

Now, you can only press the keyboard for**N**times \(with the above four keys\), find out the maximum numbers of 'A' you can print on screen.

**Example 1:**

```text
Input: N = 3Output: 3Explanation:We can at most get 3 A's on screen by pressing following key sequence:A, A, A
```

**Example 2:**

```text
Input: N = 7Output: 9Explanation:We can at most get 9 A's on screen by pressing following key sequence:A, A, A, Ctrl A, Ctrl C, Ctrl V, Ctrl V
```

**Note:**

1. 1 

   &lt;

   = N 

   &lt;

   = 50

2. Answers will be in the range of 32-bit signed integer.

分析

I可以直接print来，不copy, dp\[i\] = i

j之前print, j之后都copy, j的 range = \[1,i-3\] . dp\[i\] = dp\[j\]\*\(i-j-1\)

```text
class Solution:    def maxA(self, N: int) -> int:        dp=[0]*(N+1)        for i in range(1,N+1):                                    dp[i] = i            for j in range(1,i-3):                dp[i] = max(dp[i], dp[j]*(i-j-1))        return dp[N]
```

