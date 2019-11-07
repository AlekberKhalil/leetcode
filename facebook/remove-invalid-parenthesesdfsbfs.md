# Remove Invalid Parentheses\(dfs,bfs\)

Remove the minimum number of invalid parentheses in order to make the input string valid. Return all possible results.

**Note:** The input string may contain letters other than the parentheses`(`and`)`.

**Example 1:**

```text
Input: "()())()"Output: ["()()()", "(())()"]
```

**Example 2:**

```text
Input: "(a)())()"Output: ["(a)()()", "(a())()"]
```

**Example 3:**

```text
Input: ")("Output: [""]
```

分析

DFS：

得到多余的rmL和rmR。然后dfs，记得加一个左就Open+，右就 -- 用set去重

string + char : path += s\[pos\]

string - char: path = path\[:-1\]

```text
class Solution:    def removeInvalidParentheses(self, s):        """        :type s: str        :rtype: List[str]        """        lc = rc = 0        for c in s:            if c == '(':                lc += 1            elif c == ')':                if lc > 0:                    lc -= 1                else:                    rc += 1        ret = set()        path = ''        self.dfs(s, lc, rc, ret, path, 0, 0)        return list(ret)    def dfs(self, s, lc, rc, ret, path, pos, open):        if lc < 0 or rc < 0 or open < 0:            return        if pos == len(s):            if lc == 0 and rc == 0 and open == 0:                ret.add(str(path))            return        if s[pos] == '(':            path+=s[pos]            self.dfs(s, lc, rc, ret, path, pos + 1, open + 1)#用（            path = path[:-1]            self.dfs(s, lc - 1, rc, ret, path, pos + 1, open)        if s[pos] == ')':            path += s[pos]            self.dfs(s, lc, rc, ret, path, pos + 1, open - 1)#用）            path = path[:-1]            self.dfs(s, lc, rc - 1, ret, path, pos + 1, open)        else:            path += s[pos]            self.dfs(s, lc, rc, ret, path, pos + 1, open)#字母加            path = path[:-1]
```

BFS

filter\('\(\)'.count,s\) 这里count对\(\)都会是1，但是字母就是0，所以滤掉了字母

q是set

```text
class Solution:    def removeInvalidParentheses(self, s):        """        :type s: str        :rtype: List[str]        """        q = {s}        ret = set()        while True:            valid = filter(self.isValid, q)            if valid:                return valid            q = {s[:i] + s[i + 1:] for s in q for i in range(len(s))}    # def isValid(self, s):    #     l = 0    #     for c in s:    #         if c == '(':    #             l += 1    #         elif c == ')':    #    #             l -= 1    #    #             if l < 0:    #                 return False    #    #     return l == 0    def isValid(self,s):        s = filter('()'.count, s)        while '()' in s:            s = s.replace('()','')        return not s
```

