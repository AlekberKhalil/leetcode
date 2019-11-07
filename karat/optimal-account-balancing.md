# Optimal Account Balancing



A group of friends went on holiday and sometimes lent each other money. For example, Alice paid for Bill's lunch for $10. Then later Chris gave Alice $5 for a taxi ride. We can model each transaction as a tuple \(x, y, z\) which means person x gave person y $z. Assuming Alice, Bill, and Chris are person 0, 1, and 2 respectively \(0, 1, 2 are the person's ID\), the transactions can be represented as `[[0, 1, 10], [2, 0, 5]]`.

Given a list of transactions between a group of people, return the minimum number of transactions required to settle the debt.

**Note:**

1. A transaction will be given as a tuple \(x, y, z\). Note that `x ≠ y` and `z > 0`.
2. Person's IDs may not be linear, e.g. we could have the persons 0, 1, 2 or we could also have the persons 0, 2, 6.

**Example 1:**

```text
Input:[[0,1,10], [2,0,5]]Output:2Explanation:Person #0 gave person #1 $10.Person #2 gave person #0 $5.Two transactions are needed. One way to settle the debt is person #1 pays person #0 and #2 $5 each.
```

**Example 2:**

```text
Input:[[0,1,10], [1,0,1], [1,2,5], [2,0,5]]Output:1Explanation:Person #0 gave person #1 $10.Person #1 gave person #0 $1.Person #1 gave person #2 $5.Person #2 gave person #0 $5.Therefore, person #1 only need to give person #0 $4, and all debt is settled.
```

分析

每个人付出-，收到+，建立map， values做 debts list

dfs从某起点开始，loop加入后面每个debts，进行下一步dfs\(start+1\)，记得debts数组要恢复。debts==0忽略

等于每次清掉start的债务，丢掉start,然后继续下一轮，直到全部债务清除。

```text
class Solution:    def minTransfers(self, transactions: List[List[int]]) -> int:        mm = collections.defaultdict(int)        for a,b,m in transactions:            mm[a] = mm.get(a,0) - m            mm[b] = mm.get(b,0) + m        debts = list(mm.values())        n = len(debts)        def dfs(pos):            while pos < n and debts[pos] == 0:                pos += 1            if pos == n:                return 0            r = float('inf')            for i in range(pos+1, n):                if debts[i]*debts[pos] < 0:                    debts[i] += debts[pos]                    r= min(r,1+dfs(pos+1))                    debts[i] -= debts[pos]            return r        return dfs(0)                            
```



