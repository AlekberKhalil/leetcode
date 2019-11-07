# Sentence Similarity II

Given two sentences`words1, words2`\(each represented as an array of strings\), and a list of similar word pairs`pairs`, determine if two sentences are similar.

For example,`words1 = ["great", "acting", "skills"]`and`words2 = ["fine", "drama", "talent"]`are similar, if the similar word pairs are`pairs = [["great", "good"], ["fine", "good"], ["acting","drama"], ["skills","talent"]]`.

Note that the similarity relation**is**transitive. For example, if "great" and "good" are similar, and "fine" and "good" are similar, then "great" and "fine"**are similar**.

Similarity is also symmetric. For example, "great" and "fine" being similar is the same as "fine" and "great" being similar.

Also, a word is always similar with itself. For example, the sentences`words1 = ["great"], words2 = ["great"], pairs = []`are similar, even though there are no specified similar word pairs.

Finally, sentences can only be similar if they have the same number of words. So a sentence like`words1 = ["great"]`can never be similar to`words2 = ["doubleplus","good"]`.

**Note:**

* The length of

  `words1`

  and

  `words2`

  will not exceed

  `1000`

  .

* The length of

  `pairs`

  will not exceed

  `2000`

  .

* The length of each

  `pairs[i]`

  will be

  `2`

  .

* The length of each

  `words[i]`

  and

  `pairs[i][j]`

  will be in the range

  `[1, 20]`

  .

分析

dfs：建图，然后2点直接不到的话，loop w1的邻居n,试着从n到w2

每俩单词一个新的路径找，所以需要新visited？

一定注意每俩单词的visited都要New set（）！！！！！！不能总体的visited，错很久

```text
class Solution:    def areSentencesSimilarTwo(self, words1: List[str], words2: List[str], pairs: List[List[str]]) -> bool:        if len(words1) != len(words2):            return False        g = collections.defaultdict(list)        for w1,w2 in pairs:            g[w1].append(w2)            g[w2].append(w1)        ll = len(words1)        for i, j in zip(words1,words2):            if not self.dfs(i,j,g,set()): #不同连通子集，每次都需要new不同set，不能一个set                return False        return True        def dfs(self,w1,w2,g,visited):        if w1 == w2:            return True         if w1 in visited:            return False        visited.add(w1)        if w1 in g:            for n in g[w1]:                if self.dfs(n,w2,g,visited):                    return True        return False
```

BFS

还是要建图，但是和DFS不同，dfs每俩单词一次新搜索，这里总体bfs一次，每一群单词组用dict\[w\] = 群号.类似于所有单词归类了自己的群

然后w1,w2比较在不在一个群或者是否相等。

```text
class Solution:    def areSentencesSimilarTwo(self, words1: List[str], words2: List[str], pairs: List[List[str]]) -> bool:        if len(words1) != len(words2):            return False        g = collections.defaultdict(list)        for w1,w2 in pairs:            g[w1].append(w2)            g[w2].append(w1)        levelnum = collections.defaultdict(int)        level = 0        for w in g:                        if w in levelnum:                continue            level += 1                          q = [w]            while q:                cur = q.pop()                levelnum[cur] = level                for n in g[cur]:                    if n not in levelnum:                        q.append(n)        for i, j in zip(words1,words2):            if i == j:                continue            if levelnum[i] !=levelnum[j]:                return False        return True
```

Union find

father 是str:str的dict

注意最后比较是find\(x\) !=find\(y\) 不能直接f\[x\]!=f\[y\]

这里find function写法注意，同时dict赋值是f\[fi\] = fj \#不能是fi = f\[fj\] key error

```text
class Solution:    def areSentencesSimilarTwo(self, words1: List[str], words2: List[str], pairs: List[List[str]]) -> bool:        if len(words1) != len(words2):            return False        words = set()                f = {}#str 指向自己        def find(x):            if x in f:                return find(f[x])            return x        for i,j in pairs:            fi = find(i)            fj = find(j)            if fi!=fj:                f[fi] = fj #不能是fi = f[fj] key error        for i,j in zip(words1,words2):            if i == j:                continue            if find(i) != find(j):#不是f[i] !=f[j] 会key error                return False        return True
```

