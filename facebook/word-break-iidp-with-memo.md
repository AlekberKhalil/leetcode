# Word Break II\(dp with memo\)

Given a string s and a dictionary of words dict, add spaces in s to construct a sentence where each word is a valid dictionary word.

Return all such possible sentences.

## Example

Gieve s =`lintcode`,  
dict =`["de", "ding", "co", "code", "lint"]`.

A solution is`["lint code", "lint co de"]`.

分析

带memo的dfs.用S 做cache的key

每次substr + x for x in self.dfs

```text
import collections


class Solution:
    """
    @param: s: A string
    @param: wordDict: A set of words.
    @return: All possible sentences.
    """

    def wordBreak(self, s, wordDict):
        # write your code here
        cache = collections.defaultdict(list)
        return self.dfs(s, wordDict,cache)

    def dfs(self, s, wordDict, cache):
        if s in cache:
            return cache[s]
        res = []
        if s == '':
            return ['']

        for i in range(len(s)):
            if s[:i+1] in wordDict:
                ns = s[i+1:]  #i+1这里，loop处理每个i
                c= "" if ns=="" else " "
                res += [s[:i+1] +c+ x for x in self.dfs(ns, wordDict,cache)]
        cache[s] = res
        return res
```

先判断pos以后是否能用can\[pos\]，利用这个在dfs里剪枝，同时f\[i\]\[j\]来存储str\[i,j\]是否在字典里

```text
class Solution:
    def wordBreak(self, s, wordDict):
        """
        :type s: str
        :type wordDict: List[str]
        :rtype: List[str]
        """
        if not s:
            return []
        n = len(s)
        f = [[False]*n for _ in range(n)]
        can = [False]*n
        for i in range(n-1,-1,-1):
            for j in range(i,n):
                if s[i:j+1] in wordDict:
                    f[i][j] = True
                if f[i][j] and (j==n-1 or can[j+1]):
                    can[i] = True


        ret= []
        self.dfs(s,wordDict,"",ret,f,0,can)
        return ret
    def dfs(self,s,wordDict,path,ret,f,pos,can):
        n = len(s)
        if pos == n:
            ret.append(path.strip())
            return
        if not can[pos]:
            return

        for i in range(pos,n):
            if f[pos][i]:
                self.dfs(s,wordDict,path+' '+s[pos:i+1],ret,f,i+1,can)
```

记忆化搜索只能用s做key，不能用pos，因为str有star和长度，pos只有start

```text
class Solution:
    def wordBreak(self, s, wordDict):
        """
        :type s: str
        :type wordDict: List[str]
        :rtype: List[str]
        """
        cache = {}
        return self.dfs(s, wordDict, cache, 0)

    def dfs(self, s, wordDict, cache, pos):
        if pos in cache:
            return cache[pos]
        ret = [""]
        n = len(s)
        if pos == n:
            return ret

        for i in range(pos, n):
            if s[pos:i + 1] in wordDict:
                ns = s[pos:i + 1]
                c = "" if i +1 == n else " "
                ret=[ ns+ c+ e for e in self.dfs(s, wordDict, cache, i + 1)]

        cache[pos] = ret
        return ret
```

