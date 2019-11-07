# Valid Palindrome

Given a string, determine if it is a palindrome, considering only alphanumeric characters and ignoring cases.

**Note:** For the purpose of this problem, we define empty string as valid palindrome.

**Example 1:**

```text
Input:
 "A man, a plan, a canal: Panama"

Output:
 true
```

**Example 2:**

```text
Input:
 "race a car"

Output:
 false
```

分析

考虑只有字母 isalnum 和大小写

**别忘了lower case!!!!!**

```text
class Solution:
    def isPalindrome(self, s):
        """
        :type s: str
        :rtype: bool
        """
        s = [c.lower() for c in s if c.isalnum()]
        start, end = 0, len(s) - 1
        while start < end:
            if s[start] != s[end]:
                return False
            start += 1
            end -= 1
        return True
```

```text
class Solution:
    def isPalindrome(self, s):
        """
        :type s: str
        :rtype: bool
        """
        if not s:
            return True
        start, end = 0, len(s) - 1
        while start < end:
            while start < end and not s[start].isalnum():
                start +=1
            while start < end and not s[end].isalnum():
                end-=1

            if s[start].lower() != s[end].lower():
                return False
            start += 1
            end -= 1
        return True
```

