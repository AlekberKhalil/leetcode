# Longest Repeating Character Replacement

Given a string that consists of only uppercase English letters, you can replace any letter in the string with another letter at mostktimes. Find the length of a longest substring containing all repeating letters you can get after performing the above operations.

**Note:**  
Both the string's length andkwill not exceed 104.

**Example 1:**

```text
Input:

s = "ABAB", k = 2


Output:

4


Explanation:

Replace the two 'A's with two 'B's or vice versa.
```

**Example 2:**

```text
Input:

s = "AABABBA", k = 1


Output:

4


Explanation:

Replace the one 'A' in the middle with 'B' and form "AABBBBA".
The substring "BBBB" has the longest repeating letters, which is 4.
```

分析

每次end的count和最大maxcount比较，取更大maxcount。然后while 首尾总长 - maxcount &gt; k，一直缩头。

不知道为什么while不行 for可以

```text
class Solution:
    def characterReplacement(self, s: str, k: int) -> int:
        res,ss,e,count,l,mm = 0,0,0,0,len(s),collections.Counter()
        for e in range(len(s)):            
            mm[s[e]] += 1
            count = max(count, mm[s[e]])   
            #e+=1
            while e - ss - count + 1 > k:
                mm[s[ss]] -= 1
                ss += 1
            res = max(res, e - ss + 1)
        return res
```

