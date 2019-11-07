# Decode String（状态机）

Given an encoded string, return it's decoded string.

The encoding rule is:`k[encoded_string]`, where theencoded\_stringinside the square brackets is being repeated exactlyktimes. Note thatkis guaranteed to be a positive integer.

You may assume that the input string is always valid; No extra white spaces, square brackets are well-formed, etc.

Furthermore, you may assume that the original data does not contain any digits and that digits are only for those repeat numbers,k. For example, there won't be input like`3a`or`2[4]`.

**Examples:**

```text
s = "3[a]2[bc]", return "aaabcbc".
s = "3[a2[c]]", return "accaccacc".
s = "2[abc]3[cd]ef", return "abcabccdcdcdef".
```

分析

遇到除了\]所有元素入栈

遇到【弹出直到cnt\*str。接下来就2个结果：1栈空弹出结果 2不空压入栈继续

```text
class Solution:
    def decodeString(self, s):
        """
        :type s: str
        :rtype: str
        """
        stack = []
        ret=''

        for i in s:
            if i == ']':
                temp = scnt= ''
                while stack and stack[-1].isalpha():
                    temp = stack.pop() + temp
                if stack[-1] == '[':
                    stack.pop()
                    while stack and stack[-1].isdigit():
                        scnt = stack.pop() + scnt
                    cnt = int(scnt)
                    temp *= cnt                

                if stack:    
                    stack += temp//不空，重压入栈
                else:
                    ret += temp //空了，返回结果           
            else: stack.append(i)

        rem = ''.join(stack) if stack else ''//记得可能有残余单字母
        return ret + rem
```

