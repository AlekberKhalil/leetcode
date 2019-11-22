# Group Anagrams



Given an array of strings, group anagrams together.

**Example:**

```text
Input: ["eat", "tea", "tan", "ate", "nat", "bat"],
Output:
[
  ["ate","eat","tea"],
  ["nat","tan"],
  ["bat"]
]
```

**Note:**

* All inputs will be in lowercase.
* The order of your output does not matter.

分析

用dict\[sorted\(w\)\] =list of anagrams

注意sorted\(w\)是list，要tuple才能做key

```text
class Solution:
    def groupAnagrams(self, strs: List[str]) -> List[List[str]]:
        m = collections.defaultdict(list)
        g = [m[tuple(sorted(x))].append(x) for x in strs]
        return m.values()
```

