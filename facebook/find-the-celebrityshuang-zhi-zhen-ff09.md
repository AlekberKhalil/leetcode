# Find the Celebrity\(双指针）

Suppose you are at a party with`n`people \(labeled from`0`to`n - 1`\) and among them, there may exist one celebrity. The definition of a celebrity is that all the other`n - 1`people know him/her but he/she does not know any of them.

Now you want to find out who the celebrity is or verify that there is not one. The only thing you are allowed to do is to ask questions like: "Hi, A. Do you know B?" to get information of whether A knows B. You need to find out the celebrity \(or verify there is not one\) by asking as few questions as possible \(in the asymptotic sense\).

You are given a helper function`bool knows(a, b)`which tells you whether A knows B. Implement a function`int findCelebrity(n)`, your function should minimize the number of calls to`knows`.

## Example

Given n =`2`

```text
2 // next n * (n - 1) lines 
0 knows 1
1 does not know 0
```

return`1`// 1 is celebrity

## Notice

There will be exactly one celebrity if he/she is in the party. Return the celebrity's label if there is a celebrity in the party. If there is no celebrity, return`-1`.

分析

双指针。s,e都行。最后要验证答案

题目意思是一个人可以认识几个人，所以while那里不能直接break

```text
"""
The knows API is already defined for you.
@param a, person a
@param b, person b
@return a boolean, whether a knows b
you can call Celebrity.knows(a, b)
"""


class Solution:
    # @param {int} n a party with n people
    # @return {int} the celebrity's label or -1
    def findCelebrity(self, n):
        # Write your code here
        s,e=0,n-1
        while s<e:
            if Celebrity.knows(s, e):
                s+=1
            else:
                e-=1
        for i in range(0,n):
            if i == e or (Celebrity.knows(i, e) and not Celebrity.knows(e, i)):
                continue
            else:
                return -1
        return e
```

