# Valid Palindrome II\(dfs带while循环）

Given a non-empty string`s`, you may delete**at most**one character. Judge whether you can make it a palindrome.

**Example 1:**

```text
Input:
 "aba"

Output:
 True
```

**Example 2:**

```text
Input:
 "abca"

Output:
 True

Explanation:
 You could delete the character 'c'.
```

分析

带有while循环的递归，递归完全发生在while里面，参见dfs的for loop

注意python的ternary

```text
class Solution:
    def validPalindrome(self, s):
        """
        :type s: str
        :rtype: bool
        """ 
        return self.dfs(s,0,len(s)-1, True)

    def dfs(self,s,left,right, w):
        while left < right:
            if s[left] == s[right]:
                left += 1
                right -= 1
            else:
                return self.dfs(s, left + 1,right, False) or self.dfs(s, left,right - 1, False) if w else False

        return True
```

iterative

```text
class Solution:
    def validPalindrome(self, s: str) -> bool:
        ss ,e = 0,len(s)-1
        cnt = 0
        # def helper(l,r):
        #     while l < r:
        #         if s[l] != s[r]:
        #             return False
        #         l += 1
        #         r-= 1
        #     return True
        while ss < e:
            if s[ss] == s[e]:
                ss += 1
                e -= 1
            else:
                # return helper(ss+1,e) or helper(ss,e-1)
                l1,r1 = ss+1,e
                l2,r2 = ss,e-1
                while l1 < r1 and s[l1] == s[r1]: 
                    l1+=1
                    r1-=1
                while l2 < r2 and s[l2] == s[r2]: 
                    l2+=1
                    r2-=1 
                return l1>=r1 or l2 >= r2
        return True
        
```

