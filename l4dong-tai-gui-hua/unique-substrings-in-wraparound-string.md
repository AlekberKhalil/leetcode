# Unique Substrings in Wraparound String

Consider the string`s`to be the infinite wraparound string of "abcdefghijklmnopqrstuvwxyz", so`s`will look like this: "...zabcdefghijklmnopqrstuvwxyzabcdefghijklmnopqrstuvwxyzabcd....".

Now we have another string`p`. Your job is to find out how many unique non-empty substrings of`p`are present in`s`. In particular, your input is the string`p`and you need to output the number of different non-empty substrings of`p`in the string`s`.

**Note:**`p`consists of only lowercase English letters and the size of p might be over 10000.

**Example 1:**

```text
Input:
 "a"

Output:
 1


Explanation:
 Only the substring "a" of string "a" is in the string s.
```

**Example 2:**

```text
Input:
 "cac"

Output:
 2

Explanation:
 There are two substrings "a", "c" of string "cac" in the string s.
```

**Example 3:**

```text
Input:
 "zab"

Output:
 6

Explanation:
 There are six substrings "z", "a", "b", "za", "ab", "zab" of string "zab" in the string s.
```

分析

dp是以**每个字母**结尾的最长字符串长度。

1. 以某字母结尾的字符串：子串总数目 =最长字符串长度,这里是增量，所以必须包含该字母。 The max number of unique substring ends with a letter equals to the length of max contiguous substring ends with that letter. Example "abcd", the max number of unique substring ends with 'd' is 4, apparently they are "abcd", "bcd", "cd" and "d".
2. 如果有重复字母，取最长的长度，因为包含了短的情况。If there are overlapping, we only need to consider the longest one because it covers all the possible substrings. Example: "abcdbcd", the max number of unique substring ends with 'd' is 4 and all substrings formed by the 2nd "bcd" part are covered in the 4 substrings already.
3. No matter how long is a contiguous substring in p, it is in s since s has infinite length.
4. 找到所有字母的最长子串，相加就是结果。Now we know the max number of unique substrings in p ends with 'a', 'b', ..., 'z' and those substrings are all in s. Summary is the answer, according to the question.

```text
class Solution:
    def findSubstringInWraproundString(self, p: str) -> int:
        n = len(p)                
        dp = [0]*26
        maxLen = 0
        res = 0

        for i in range(n):             
            if i>0 and (ord(p[i])-ord(p[i-1]) == 1 or ord(p[i])-ord(p[i-1]) == -25):
                maxLen += 1
            else:
                maxLen = 1
            idx = ord(p[i])-ord('a')
            dp[idx] = max(dp[idx],maxLen)

        for i in range(26):
            res+=dp[i]
        return res
```

