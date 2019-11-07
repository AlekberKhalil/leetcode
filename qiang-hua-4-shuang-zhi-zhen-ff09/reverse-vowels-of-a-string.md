# Reverse Vowels of a String

Write a function that takes a string as input and reverse only the vowels of a string.

**Example 1:**

```text
Input: 
"hello"
Output: 
"holle"
```

**Example 2:**

```text
Input: 
"leetcode"
Output: 
"leotcede"
```

**Note:**  
The vowels does not include the letter "y".

分析

string里的swap char， 先转成List\(str\) ,swap完了再''.join\(list\)

注意包括大写

```text
class Solution:
    def reverseVowels(self, s: str) -> str:
        l = len(s)
        ss,e = 0,l-1
        s = list(s)
        while ss < e:
            while ss < e and s[ss] not in 'aeiouAEIOU':
                ss += 1
            while ss < e and s[e] not in 'aeiouAEIOU':
                e -= 1
            s[ss],s[e] = s[e],s[ss]
            ss += 1
            e -= 1

        return ''.join(s)
```

