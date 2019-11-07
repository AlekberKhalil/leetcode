# Majority Element II



Given an integer array of size n, find all elements that appear more than `⌊ n/3 ⌋` times.

**Note:** The algorithm should run in linear time and in O\(1\) space.

**Example 1:**

```text
Input: [3,2,3]Output: [3]
```

**Example 2:**

```text
Input: [1,1,1,3,3,2,2,2]Output: [1,2]
```

分析

求出现频率超过1/3的数字

可以每次出现3组数的时候就减掉Triple,这样抵消到最后。剩余的数字算算有没全局的1/3

这里注意dict相减法，和直接set（dict）得到所有unique key

```text
collections.Counter(set(cnt))
```

```text
class Solution:    def majorityElement(self, nums: List[int]) -> List[int]:        cnt = collections.Counter()        for i in nums:            cnt[i] += 1            if len(cnt) == 3:                cnt -= collections.Counter(set(cnt))        return [n for n in cnt if nums.count(n) > int(len(nums) / 3)]        
```

