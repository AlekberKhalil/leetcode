# Longest String Chain

Given a list of words, each word consists of English lowercase letters.

Let's say`word1`is a predecessor of`word2` if and only if we can add exactly one letter anywhere in`word1`to make it equal to`word2`. For example, `"abc"` is a predecessor of`"abac"`.

A\_word chain \_is a sequence of words`[word_1, word_2, ..., word_k]` with`k >= 1`, where`word_1`is a predecessor of`word_2`,`word_2`is a predecessor of`word_3`, and so on.

Return the longest possible length of a word chain with words chosen from the given list of`words`.

**Example 1:**

```text
Input: ["a","b","ba","bca","bda","bdca"]Output: 4Explanation: one of the longest word chain is "a","ba","bda","bdca".
```

```text
Note:1 <= words.length <= 10001 <= words[i].length <= 16words[i] only consists of English lowercase letters.
```

分析

本题**顺序可以重组**，所以sort,注意可以直接**sort\(key=len\)**

**每个词只有一个子**，所以只要找到子+1就好，dp是dict: word-&gt;count

```text
class Solution:    def longestStrChain(self, words: List[str]) -> int:        n = len(words)        dp = {w:1 for w in words}        words.sort(key= len)        res = 1        for w in words:             for i in range(len(w)):                nw = w[:i] + w[i+1:]                if nw in words:                    dp[w] =dp[nw]+1        return max(dp[w] for w in words)
```

