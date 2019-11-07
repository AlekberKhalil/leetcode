# K-diff Pairs in an Array

Given an array of integers and an integer**k**, you need to find the number of**unique**k-diff pairs in the array. Here a**k-diff**pair is defined as an integer pair \(i, j\), where**i**and**j**are both numbers in the array and their[absolute difference](https://en.wikipedia.org/wiki/Absolute_difference)is**k**.

**Example 1:**

```text
Input: [3, 1, 4, 1, 5], k = 2Output: 2Explanation: There are two 2-diff pairs in the array, (1, 3) and (3, 5).Although we have two 1s in the input, we should only return the number of unique pairs.
```

**Example 2:**

```text
Input:[1, 2, 3, 4, 5], k = 1Output: 4Explanation: There are four 1-diff pairs in the array, (1, 2), (2, 3), (3, 4) and (4, 5).
```

**Example 3:**

```text
Input: [1, 3, 1, 5, 4], k = 0Output: 1Explanation: There is one 0-diff pair in the array, (1, 1).
```

分析

就是2sum的思想，**排序后**，a和a-k pair存入map

```text
class Solution:    def findPairs(self, nums: List[int], k: int) -> int:        nums.sort()        ll = len(nums)        mm = dict()        res = set()        for i in range(ll):            if nums[i]-k in mm:                res.add((nums[i]-k,nums[i]))            mm[nums[i]] = i        return len(res)
```

