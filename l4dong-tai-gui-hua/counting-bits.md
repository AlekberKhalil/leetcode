# Counting Bits

Given a non negative integer number**num**. For every numbers**i**in the range**0 ≤ i ≤ num**calculate the number of 1's in their binary representation and return them as an array.

**Example 1:**

```text
Input: 2Output: [0,1,1]
```

**Example 2:**

```text
Input: 5Output: [0,1,1,2,1,2]
```

**Follow up:**

* It is very easy to come up with a solution with run time

  **O\(n\*sizeof\(integer\)\)**

  . But can you do it in linear time

  **O\(n\)**

  /possibly in a single pass?

* Space complexity should be

  **O\(n\)**

  .

* Can you do it like a boss? Do it without using any builtin function like

  **\_\_builtin\_popcount**

  in c++ or in any other language.

分析

用c&\(c-1\)去掉最后一位1，就是原数缺了最后一个1

c - \(c-1\)&c得到最后一个1，就是全部置空只有最后一个1的位置有1

```text
class Solution:    def countBits(self, num: int) -> List[int]:        """        :type num: int        :rtype: List[int]        """        p = [0]*(num+1)        for i in range(1,num+1):            p[i] =p[i&(i-1)] + 1        return p
```

