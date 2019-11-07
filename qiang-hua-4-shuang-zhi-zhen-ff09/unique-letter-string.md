# Unique Letter String

A character is unique in string`S`if it occurs exactly once in it.

For example, in string`S = "LETTER"`, the only unique characters are`"L"`and`"R"`.

Let's define`UNIQ(S)`as the number of unique characters in string`S`.

For example,`UNIQ("LETTER") = 2`.

Given a string`S`with only uppercases, calculate the sum of`UNIQ(substring)`over all non-empty substrings of`S`.

If there are two or more equal substrings at different positions in`S`, we consider them different.

Since the answer can be very large, return the answer modulo `10 ^ 9 + 7`.

**Example 1:**

```text
Input: 
"ABC"

Output: 
10

Explanation: 
All possible substrings are: "A","B","C","AB","BC" and "ABC".
Evey substring is composed with only unique letters.
Sum of lengths of all substring is 1 + 1 + 1 + 2 + 2 + 3 = 10
```

**Example 2:**

```text
Input: 
"ABA"

Output: 
8

Explanation: 
The same as example 1, except uni("ABA") = 1.
```

**Note:**`0 <= S.length <= 10000`.

分析

比较Subarray Product Less Than K

动态规划

Take the below example:

```text
BBBBBBBBBBBBBBBBBOABCDOABCOABC
                 ^    ^   ^
                 s    f   i

dp[i] = dp[i-1] + (i-f) - (f-s)
```

When extending`s[i]`to all substrings ending with`s[i-1]`, there are`(i-f)`more unique char`s[i]`, and`(f-s)`less unique char because of duplicate of`s[i]`.

每次到i位置，f-i段贡献了unique，但是f-s段重复了需要去掉。注意坐标

i-f几条线段，每段线段长度都加1，就是增量，还要加上Base=前面几段线段长度总和

```text
class Solution:
    def uniqueLetterString(self, S: str) -> int:
        dp = 0
        first = [0]*26
        second = [0]*26
        res = 0
        for i,v in enumerate(list(S)):
            idx = ord(v)-ord('A')

            dp = dp + 1 + i-2*first[idx] + second[idx]#注意坐标 +1
            first[idx],second[idx] = i+1,first[idx]#注意坐标 +1
            res += dp
        return res% 1000000007
```

