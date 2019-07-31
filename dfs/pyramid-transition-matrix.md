# Pyramid Transition Matrix

We are stacking blocks to form a pyramid. Each block has a color which is a one letter string.

We are allowed to place any color block`C`on top of two adjacent blocks of colors`A`and`B`, if and only if`ABC`is an allowed triple.

We start with a bottom row of`bottom`, represented as a single string. We also start with a list of allowed triples`allowed`. Each allowed triple is represented as a string of length 3.

Return true if we can build the pyramid all the way to the top, otherwise false.

**Example 1:**

```text
Input:
 bottom = "BCD", allowed = ["BCG", "CDE", "GEA", "FFF"]

Output:
 true

Explanation:

We can stack the pyramid like this:
    A
   / \
  G   E
 / \ / \
B   C   D

We are allowed to place G on top of B and C because BCG is an allowed triple.  Similarly, we can place E on top of C and D, then A on top of G and E.
```

**Example 2:**

```text
Input:
 bottom = "AABA", allowed = ["AAA", "AAB", "ABA", "ABB", "BAC"]

Output:
 false

Explanation:

We can't stack the pyramid to the top.
Note that there could be allowed triples (A, B, C) and (A, B, D) with C != D.
```

**Note:**

1. `bottom`

   will be a string with length in range

   `[2, 8]`

   .

2. `allowed`

   will have length in range

   `[0, 200]`

   .

3. Letters in all strings will be chosen from the set

   `{'A', 'B', 'C', 'D', 'E', 'F', 'G'}`

   .

分析

map里存所有2字母可达的第三字母

product返回数组的所有组合，这里product所有map里的value,也就是所有可达组合，然后dfs递归

```text
class Solution:
    def pyramidTransition(self, bottom: str, allowed: List[str]) -> bool:
        mm = collections.defaultdict(list)
        for a in allowed:
            mm[a[:2]].append(a[2])
        def dfs(bottom):
            if len(bottom) == 1:
                return True
            for k in itertools.product(*(mm[a+b] for a,b in zip(bottom[:-1],bottom[1:]))):
                if dfs(k):
                    return True
            return False
        return dfs(bottom)
```

