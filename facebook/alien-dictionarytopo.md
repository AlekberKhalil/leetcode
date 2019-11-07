# Alien Dictionary\(topo\)

There is a new alien language which uses the latin alphabet. However, the order among letters are unknown to you. You receive a list of**non-empty**words from the dictionary, where words are**sorted lexicographically by the rules of this new language**. Derive the order of letters in this language.

## Example

Given the following words in dictionary,

```text
[  "wrt",  "wrf",  "er",  "ett",  "rftt"]
```

The correct order is:`"wertf"`

Given the following words in dictionary,

```text
[  "z",  "x"]
```

The correct order is:`"zx"`.

## Notice

1. You may assume all letters are in lowercase.
2. You may assume that if a is a prefix of b, then a must appear before b in the given dictionary.
3. If the order is invalid, return an empty string.
4. There may be multiple valid order of letters,

   `return the smallest in lexicographical order`

Input test data

\(

one parameter per line

\)

分析

相邻2个word比较，选长度短的for，比完就break

字典序，要用priority queue

初始化入度和图，防止漏初始点

```text
import collectionsimport heapqclass Solution:    """    @param words: a list of words    @return: a string which is correct order    """    def alienOrder(self, words):        # Write your code here        #不初始化的话会忽略头结点        indegree = {j:0 for w in words for j in w}        graph = {j:[] for w in words for j in w}        n = len(words)        for i in range(n-1):            for j in range(min(len(words[i]),len(words[i+1]))):                if words[i][j] != words[i+1][j]:                    graph[words[i][j]].append(words[i+1][j])                     indegree[words[i+1][j]] += 1                    break #每次只相邻2个word比较，所以要Break        q = [k for k,v in indegree.items() if v == 0]        heapq.heapify(q)#保持最小字典序，必须heapify        ret = ""        while q:            cur = heapq.heappop(q)            ret += cur            for i in graph[cur]:                indegree[i]-=1                if not indegree[i]:                    heapq.heappush(q,i)        if len(ret) != len(indegree):            return ""        return ret
```

