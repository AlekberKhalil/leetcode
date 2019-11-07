# Valid Palindrome II\(dfs带while循环）

Given a non-empty string`s`, you may delete**at most**one character. Judge whether you can make it a palindrome.

**Example 1:**

```text
Input: "aba"Output: True
```

**Example 2:**

```text
Input: "abca"Output: TrueExplanation: You could delete the character 'c'.
```

分析

带有while循环的递归，递归完全发生在while里面，参见dfs的for loop

注意python的ternary

```text
class Solution:    def validPalindrome(self, s):        """        :type s: str        :rtype: bool        """         return self.dfs(s,0,len(s)-1, True)    def dfs(self,s,left,right, w):        while left < right:            if s[left] == s[right]:                left += 1                right -= 1            else:                return self.dfs(s, left + 1,right, False) or self.dfs(s, left,right - 1, False) if w else False        return True
```

