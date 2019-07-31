# Total Hamming Distance\(位运算 bit）

The[Hamming distance](https://en.wikipedia.org/wiki/Hamming_distance)between two integers is the number of positions at which the corresponding bits are different.

Now your job is to find the total Hamming distance between all pairs of the given numbers.

**Example:**

```text
Input:
 4, 14, 2


Output:
 6


Explanation:
 In binary representation, the 4 is 0100, 14 is 1110, and 2 is 0010 (just
showing the four bits relevant in this case). So the answer will be:
HammingDistance(4, 14) + HammingDistance(4, 2) + HammingDistance(14, 2) = 2 + 2 + 2 = 6.
```

**Note:**

1. Elements of the given array are in the range of0 to`10^9`
2. Length of the array will not exceed`10^4`

   .

分析

位运算，得到最大数字，然后while m&lt;maxx。每一位bit都用m&lt;&lt;1然后 m\# 。每个bit都 cnt0 \* cnt1。不懂为什么\*

cnt0 \* cnt1 因为不一样的组合，比如2个0 3个1， 01的组合就是2\*3=6 对

```text
class Solution:
    def totalHammingDistance(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        n = len(nums)
        if n <= 1:
            return 0
        ret= 0
        maxx = max(nums)
        m = 1
        while m <= maxx: #是<=不是<
            c1=0 #要在while里
            for num in nums:
                if m & num:
                    c1 += 1
            m <<= 1
            ret += c1*(n-c1)

        return ret
```

