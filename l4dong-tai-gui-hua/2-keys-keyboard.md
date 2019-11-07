# 2 Keys Keyboard

Initially on a notepad only one character 'A' is present. You can perform two operations on this notepad for each step:

1. `Copy All`

   : You can copy all the characters present on the notepad \(partial copy is not allowed\).

2. `Paste`

   : You can paste the characters which are copied

   **last time**

   .

Given a number`n`. You have to get**exactly**`n`'A' on the notepad by performing the minimum number of steps permitted. Output the minimum number of steps to get`n`'A'.

**Example 1:**

```text
Input:
 3

Output:
 3

Explanation:

Intitally, we have one character 'A'.
In step 1, we use 
Copy All
 operation.
In step 2, we use 
Paste
 operation to get 'AA'.
In step 3, we use 
Paste
 operation to get 'AAA'.
```

**Note:**

1. The

   `n`

   will be in the range \[1, 1000\].

分析

DP:想象每次8从4copy+paste来，就是额外增加2次操作。

dp\[8\] = dp\[4\]+8/4

[https://leetcode.com/problems/2-keys-keyboard/discuss/105899/Java-DP-Solution](https://leetcode.com/problems/2-keys-keyboard/discuss/105899/Java-DP-Solution)

贪心：每次一个数可以被N整除就加上那个数，不行再换下一个，res就是所有可以被整除的数的总和。

```text
class Solution:
    def minSteps(self, n: int) -> int:
    #greedy
        res = 0 
        if n == 1:
            return 0
        for i in range(2,n+1):            
            while n%i == 0:                
                res+=i
                n/=i
        return res
```

