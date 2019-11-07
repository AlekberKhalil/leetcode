# Long Pressed Name

Your friend is typing his`name` into a keyboard. Sometimes, when typing a character`c`, the key might get_long pressed_, and the character will be typed 1 or more times.

You examine the`typed` characters of the keyboard. Return`True`if it is possible that it was your friends name, with some characters \(possibly none\) being long pressed.

**Example 1:**

```text
Input: name = "alex", typed = "aaleex"Output: trueExplanation: 'a' and 'e' in 'alex' were long pressed.
```

**Example 2:**

```text
Input: name = "saeed", typed = "ssaaedd"Output: falseExplanation: 'e' must have been pressed twice, but it wasn't in the typed output.
```

**Example 3:**

```text
Input: name = "leelee", typed = "lleeelee"Output: true
```

**Example 4:**

```text
Input: name = "laiden", typed = "laiden"Output: trueExplanation: It's not necessary to long press any character.
```

**Note:**

```text
name.length <= 1000typed.length <= 1000The characters of name and typed are lowercase letters.
```

分析

source和target一起走

本题因为是重复字母，所以可以提前return 如果既！=source 又不是duplicate a\[i\]!=a\[j-1\]

```text
class Solution:    def isLongPressedName(self, name: str, typed: str) -> bool:        p=q = 0        lp = len(name)        lq = len(typed)        while p < lp and q < lq:            if name[p] == typed[q]:                p +=1                q +=1            elif q ==0 or typed[q]!=typed[q-1]:#加这个会快很多，也可以不加                return False            else:                q += 1        if p == lp:            return True        return False
```

