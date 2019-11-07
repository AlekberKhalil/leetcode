# Boats to Save People

The`i`-th person has weight`people[i]`, and each boat can carry a maximum weight of`limit`.

Each boat carries at most 2 people at the same time, provided the sum of the weight of those people is at most`limit`.

Return the minimum number of boats to carry every given person. \(It is guaranteed each person can be carried by a boat.\)

**Example 1:**

```text
Input: people = [1,2], limit = 3Output: 1Explanation: 1 boat (1, 2)
```

**Example 2:**

```text
Input: people = [3,2,2,1], limit = 3Output: 3Explanation: 3 boats (1, 2), (2) and (3)
```

**Example 3:**

```text
Input: people = [3,5,3,4], limit = 5Output: 4Explanation: 4 boats (3), (3), (4), (5)
```

**Note**:

```text
1 <= people.length <= 500001 <= people[i] <= limit <= 30000
```

分析

因为船只能载2人每次，所以可以双指针夹逼，注意是 l&lt;=r

```text
class Solution:    def numRescueBoats(self, people: List[int], limit: int) -> int:                        temp = res = 0         l = 0        r = len(people)-1        people.sort()        while l <= r:            if people[l] +people[r] <= limit:                res += 1                l += 1                r-=1            else:                res+=1                r-=1        return res
```

