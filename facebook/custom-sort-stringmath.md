# Custom Sort String\(math\)

`S`and`T`are strings composed of lowercase letters. In`S`, no letter occurs more than once.

`S`was sorted in some custom order previously. We want to permute the characters of`T`so that they match the order that`S`was sorted. More specifically, if`x`occurs before`y`in`S`, then`x`should occur before`y`in the returned string.

Return any permutation of`T`\(as a string\) that satisfies this property.

```text
Example :
Input:

S = "cba"
T = "abcd"

Output:
 "cbad"

Explanation:

"a", "b", "c" appear in S, so the order of "a", "b", "c" should be "c", "b", and "a". 
Since "d" does not appear in S, it can be at any position in T. "dcba", "cdba", "cbda" are also valid outputs.
```

**Note:**

```text
S has length at most 26, and no character is repeated in S.
T has length at most 200.
S and T consist of lowercase letters only.
```

分析

算出来T里每个char的count

先遍历S输出所有 \[i\*count\[i\]\] 然后把T剩下的输出，还是\[i\*count\[i\]\]

```text
import collections


class Solution:
    def customSortString(self, S, T):
        """
        :type S: str
        :type T: str
        :rtype: str
        """
        count = collections.defaultdict(int)
        l = []
        for i in T:
            count[i] += 1

        for i in S:
            if i in count:
                l+=[i * count[i]]
                count[i] = 0
        l+=[i*count[i] for i in count]
        return ''.join(l)
```

