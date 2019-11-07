# Partitioning Array

Given an array of numbers, you are required to check if it is possible to partition the array into some subsequences of length k each, such that:

* Each element in the array occurs in exactly one subsquence
* All the numbers in a subsequence are distinct
* Elements in the array having the same value must be in different subsequences Is possible to partition the array satisfying the above conditions? If it is possible, return true, else return false

#### Example

```text
Example1:Input:A:[1, 2, 3, 4]k = 2output: trueExplanation:Then one possible way is to choose the first 2 elements of the array {1, 2} as the first subsequence, the next 2 elements {3, 4} as the next subsquence.So the answer is true
```

```text
Example2:Input:A: [1, 2, 2, 3]k: 3output: falseExplanation:there is no way to partition the array into subsequences such that all subsquences are of length 3 and each element in the array occurs in exactly one subsequece.Hence the answer is false.
```

Input test data \(one parameter per line\)How to understand a testcase?  
分析 

k是subarr的大小，不能整除，和最大重复数 \# &gt; group \# 则false

```text
class Solution:    """    @param A: Integer array    @param k: a integer    @return: return is possible to partition the array satisfying the above conditions    """    def PartitioningArray(self, A, k):        # write your code here        if not A and k == 1:            return True        n = len(A)        if k > n or n%k:            return False        groupnum = n//k        cnt = collections.Counter(A)        if groupnum < max(cnt.values()):            return False        return True                               
```

