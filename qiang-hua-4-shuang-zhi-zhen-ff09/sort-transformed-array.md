# Sort Transformed Array

Given a**sorted**array of integersnumsand integer valuesa,bandc. Apply a quadratic function of the form f\(x\) =ax2+bx+cto each elementxin the array.

The returned array must be in**sorted order**.

Expected time complexity:**O\(n\)**

**Example 1:**

```text
Input: nums = [-4,-2,2,4], a = 1, b = 3, c = 5Output: [3,9,15,33]
```

**Example 2:**

```text
Input: nums = [-4,-2,2,4], a = -1, b = 3, c = 5Output: [-23,-5,1,7]
```

分析

就是map函数映射，记得用lambda

```text
class Solution:    def sortTransformedArray(self, nums: List[int], a: int, b: int, c: int) -> List[int]:        nl = map(lambda x: a*x**2 + b*x+c, nums)        return sorted(nl)
```

