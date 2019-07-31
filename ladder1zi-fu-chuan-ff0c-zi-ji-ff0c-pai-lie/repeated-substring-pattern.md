# Repeated Substring Pattern

Given a non-empty string check if it can be constructed by taking a substring of it and appending multiple copies of the substring together. You may assume the given string consists of lowercase English letters only and its length will not exceed 10000.

**Example 1:**

```text
Input: "abab"

Output: True

Explanation: It's the substring "ab" twice.
```

**Example 2:**

```text
Input: "aba"

Output: False
```

**Example 3:**

```text
Input: "abcabcabcabc"

Output: True

Explanation: It's the substring "abc" four times. (And the substring "abcabc" twice.)
```

分析

2个s相连，去首尾char，得到T，然后看看s在不在T里。

找到s在T里出现的第一个位置i，重复的字符的长度是i+1，重复字符是s\(0,i+1\)

```text
class Solution {
    public boolean repeatedSubstringPattern(String s) {
        if(s == null || s.length() == 0)
            return true;
        String ss = s + s;
        String t = ss.substring(1, ss.length() - 1);
        return t.indexOf(s) >= 0;
    }
}
```

