# Minimum Swaps To Make Sequences Increasing\(动归

We have two integer sequences`A`and`B`of the same non-zero length.

We are allowed to swap elements`A[i]`and`B[i]`. Note that both elements are in the same index position in their respective sequences.

At the end of some number of swaps,`A`and`B`are both strictly increasing. \(A sequence is\_strictly increasing\_if and only if`A[0] < A[1] < A[2] < ... < A[A.length - 1]`.\)

Given A and B, return the minimum number of swaps to make both sequences strictly increasing. It is guaranteed that the given input always makes it possible.

```text
Example:
Input:
 A = [1,3,5,4], B = [1,2,3,7]

Output:
 1

Explanation: 

Swap A[3] and B[3].  Then the sequences are:
A = [1, 3, 5, 7] and B = [1, 2, 3, 4]
which are both strictly increasing.
```

**Note:**

* `A, B`are arrays with the same length, and that length will be in the range`[1, 1000]`.
* `A[i], B[i]`are integer values in the range`[0, 2000]`

  .

分析

3个case ：

```text
a) We either swap or not in position i for condition: A[i]>A[i-1] && A[i]>B[i-1] && B[i] > A[i-1] && B[i] > B[i-1].
b) If i-1 swaps, i swaps. If i-1 does not swap, i does not swap. A[i]>A[i-1] && B[i]>B[i-1]
c) If i-1 swaps, i does not swaps. If i-1 does not swap, i swaps.
```

维持2个变量，换个数和不换个数，最后选个小的。1换不换都行 2 可以不换 3 必须换

[https://leetcode.com/problems/minimum-swaps-to-make-sequences-increasing/discuss/163811/C++-Ultimately-Easy-Solution\(Different-From-the-Official-Solution\](https://leetcode.com/problems/minimum-swaps-to-make-sequences-increasing/discuss/163811/C++-Ultimately-Easy-Solution%28Different-From-the-Official-Solution%29\)

```text
class Solution {
    public int minSwap(int[] A, int[] B) {

        int s1 = 1,n1 = 0;
        for(int i=1; i<A.length; i++) {
            int s2, n2;
            if(A[i] >A[i-1] && B[i] >B[i-1]&& A[i] >B[i-1]&& B[i] >A[i-1]) {

                s2 = Math.min(s1,n1) + 1;
                n2 = Math.min(s1,n1);
            } else  if(A[i] >A[i-1] && B[i] >B[i-1]){
                //可不换，若前换后必须换
                s2 = s1 + 1;
                n2 = n1;
            }else {
            //必须换，前不换后必须换
                s2 = n1 + 1;
                n2 = s1;
            }
            s1 = s2;
            n1 = n2;
        }
        return Math.min(s1, n1);
    }
}
```

python

```text
class Solution:
    def minSwap(self, A, B):
        """
        :type A: List[int]
        :type B: List[int]
        :rtype: int
        """
        n1=n2=s1=s2=0
        n = len(A)
        for i in range(n):
            if A[i]>A[i-1] and B[i]>B[i-1] and A[i]>B[i-1] and B[i]>A[i-1]:
                n2 = min(n1,s1)
                s2 = min(n1,s1)+1
            elif A[i]>A[i-1] and B[i]>B[i-1]:
                n2 = n1
                s2 = s1+1
            else:
                n2 = s1
                s2 = n1+1

            n1,s1=n2,s2
        return min(n1,s1)
```

