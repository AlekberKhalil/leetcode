# Reconstruct Original Digits from English



Given a non-empty string containing an out-of-order English representation of digits 0-9, output the digits in ascending order.

#### Example

**Example 1:**

```text
Input: "owoztneoer"Output: "012"
```

**Example 2:**

```text
Input: "fviefuro"Output: "45"
```

#### Notice

* Input contains only lowercase English letters.
* Input is guaranteed to be valid and can be transformed to its original digits. That means invalid inputs such as "abc" or "zerone" are not permitted.
* Input length is less than 50,000.

分析

找出s中每个数字的特有的char, nums\[num\] = s.count\(char）

```text
class Solution:    """    @param s: a string    @return: return a string    """    def originalDigits(self, s):        # write  your code here        nums = [0 for x in range(10)]        nums[0] = s.count('z')        nums[2] = s.count('w')        nums[4] = s.count('u')        nums[6] = s.count('x')        nums[8] = s.count('g')               nums[3] = s.count('h') - nums[8]        nums[7] = s.count('s') - nums[6]        nums[5] = s.count('v') - nums[7]        nums[1] = s.count('o') - nums[0] - nums[2] - nums[4]        nums[9] = (s.count('n') - nums[1] - nums[7]) // 2        res = ''        for i in range(10):            res += str(i) * nums[i]        return res        
```

