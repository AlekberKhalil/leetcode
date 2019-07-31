# Least Substring

## Description

Given a string containing`n`lowercase letters, the string needs to divide into several continuous substrings, the letter in the substring should be same, and the number of letters in the substring does not exceed`k`, and output the minimal substring number meeting the requirement.

* n \leq 1e5

  n

  ≤

  1

  e

  5

Have you met this question in a real interview?

Yes

Problem Correction

## Example

Give`s = "aabbbc", k = 2`, return`4`

```text
Explaination:
we can get "aa", "bb", "b", "c" four substring.
```

Give`s = "aabbbc", k = 3`, return`3`

```text
Explaination:
we can get "aa", "bbb", "c" three substring.
```

分析

遇到cnt == k或者字母变化就res+=1 cnt = 0 否则cnt ++

不是很懂

```text
    # def getAns(self, s, k):
    #     # Write your code here
    #     cnt = 1
    #     res = 1
    #     sLen = len(s)
    #     cur = s[0]
    #     for i in range(1,sLen):
    #         if cnt == k or s[i] != s[i-1]:
    #             res += 1 
    #             cnt = 0
    #         cnt += 1
    #     return res
```

