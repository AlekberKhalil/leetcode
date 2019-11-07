# Word Break（dp\)

Given a**non-empty**string\_s\_and a dictionary\_wordDict\_containing a list of**non-empty**words, determine if\_s\_can be segmented into a space-separated sequence of one or more dictionary words.

**Note:**

* The same word in the dictionary may be reused multiple times in the segmentation.
* You may assume the dictionary does not contain duplicate words.

**Example 1:**

```text
Input: s = "leetcode", wordDict = ["leet", "code"]Output: trueExplanation: Return true because "leetcode" can be segmented as "leet code".
```

**Example 2:**

```text
Input: s = "applepenapple", wordDict = ["apple", "pen"]Output: trueExplanation: Return true because "applepenapple" can be segmented as "apple pen apple".             Note that you are allowed to reuse a dictionary word.
```

**Example 3:**

```text
Input: s = "catsandog", wordDict = ["cats", "dog", "sand", "and", "cat"]
```

分析

dfs会超时 用DP

dp\[i\]以I结尾的word 能不能分：dp\[i\] = dp\[j\] && s\[j:i\] in wordDict 遇到true就断了不要继续了

```text
class Solution:    def wordBreak(self, s, wordDict):        """        :type s: str        :type wordDict: List[str]        :rtype: bool        """        if not s:            return False        n = len(s)        dp = [False] * (n + 1)        dp[0] = True        for i in range(1, n + 1):            for j in range(0, i):                if s[j:i] in wordDict:                    dp[i] = dp[j]                    if dp[i]:                        break #有合法值就出来！！！！        return dp[n]
```

