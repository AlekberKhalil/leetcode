# Minimum Genetic Mutation



A gene string can be represented by an 8-character long string, with choices from `"A"`, `"C"`, `"G"`, `"T"`.

Suppose we need to investigate about a mutation \(mutation from "start" to "end"\), where ONE mutation is defined as ONE single character changed in the gene string.

For example, `"AACCGGTT"` -&gt; `"AACCGGTA"` is 1 mutation.

Also, there is a given gene "bank", which records all the valid gene mutations. A gene must be in the bank to make it a valid gene string.

Now, given 3 things - start, end, bank, your task is to determine what is the minimum number of mutations needed to mutate from "start" to "end". If there is no such a mutation, return -1.

#### Example

**Example 1:**

```text
Input:"AACCGGTT""AACCGGTA"["AACCGGTA"]Output: 1Explanation:start: "AACCGGTT"end:  "AACCGGTA"bank: ["AACCGGTA"]
```

**Example 2:**

```text
Input:"AACCGGTT""AAACGGTA"["AACCGGTA", "AACCGCTA", "AAACGGTA"]Output: 2
```

**Example 3:**

```text
Input:"AAAAACCC""AACCCCCC"["AAAACCCC", "AAACCCCC", "AACCCCCC"]Output: 3
```

#### Notice

1. Starting point is assumed to be valid, so it might not be included in the bank.
2. If multiple mutations are needed, all mutations during in the sequence must be valid.
3. You may assume start and end string is not the same.

分析

BFS

```text
class Solution:    """    @param start:     @param end:     @param bank:     @return: the minimum number of mutations needed to mutate from "start" to "end"    """    def minMutation(self, start, end, bank):        # Write your code here        chars = ["A", "C", "G", "T"]        bank = set(bank)        def bfs():            q = [start]            distance = {start:0}            while q:                cur = q.pop(0)                if cur == end:                   return distance[cur]                for i in range(len(cur)):                    for j in chars:                        nw = cur[:i] + j + cur[i+1:]                        if nw in bank and nw not in distance:                            distance[nw] = distance[cur] + 1                            q.append(nw)            return -1        return bfs()                                        
```

