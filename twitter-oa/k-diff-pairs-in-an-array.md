# K-diff Pairs in an Array

Given an array of integers and an integer **k**, you need to find the number of **unique** k-diff pairs in the array. Here a **k-diff** pair is defined as an integer pair \(i, j\), where i and j are both numbers in the array and their absolute difference is **k**.

#### Example

**Example 1:**

```text
Input: [3, 1, 4, 1, 5], k = 2
Output: 2
Explanation: There are two 2-diff pairs in the array, (1, 3) and (3, 5).
Although we have two 1s in the input, we should only return the number of unique pairs.
```

**Example 2:**

```text
Input:[1, 2, 3, 4, 5], k = 1
Output: 4
Explanation: There are four 1-diff pairs in the array, (1, 2), (2, 3), (3, 4) and (4, 5).
```

**Example 3:**

```text
Input: [1, 3, 1, 5, 4], k = 0
Output: 1
Explanation: There is one 0-diff pair in the array, (1, 1).
```

#### Notice

1.The pairs \(i, j\) and \(j, i\) count as the same pair.  
2.The length of the array won't exceed 10,000.  
3.All the integers in the given input belong to the range: \[-1e7, 1e7\].Input test data \(one parameter per line\)How to understand a testcase?

分析

Counter 数组，然后遍历counter\(不是数组），只需要判断i+k 和 k==0& cnt\[cur\]&gt;=2

```text
class Solution:
    """
    @param nums: an array of integers
    @param k: an integer
    @return: the number of unique k-diff pairs
    """
    def findPairs(self, nums, k):
        # Write your code here
        nummap = collections.Counter(nums)
        res = 0
        for i in nummap:
            if k > 0 and i+k in nummap or k == 0 and nummap[i]>=2:
                res+=1
               
            
        return res

```

