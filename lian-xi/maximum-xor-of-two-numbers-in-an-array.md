# Maximum XOR of Two Numbers in an Array



Given a **non-empty** array of numbers, a0, a1, a2, … , an-1, where 0 ≤ ai &lt; 231.

Find the maximum result of ai XOR aj, where 0 ≤ i, j &lt; n.

Could you do this in O\(n\) runtime?

**Example:**

```text
Input: [3, 10, 5, 25, 2, 8]

Output: 28

Explanation: The maximum result is 5 ^ 25 = 28.
```

分析

a^b=c =&gt; a^c =b. 所以用ans^a = b =&gt; a^b = ans    \(a,b都是prevs\)

每次这里只在乎每个Num的左半部分bit， ans &gt;&gt;=1 然后 ans^1（ 就是ans+1）让ans下一位变成1，如果能找到ans^a也在prevs里，这该数b^a = ans

```text
class Solution:
    def findMaximumXOR(self, nums: List[int]) -> int:
        ans = 0
        for i in range(32)[::-1]:
            prevs = [n>>i for n in nums]
            ans <<= 1
            ans += any(ans^1^p in prevs for p in prevs)
        return ans
        
```

```text
class TrieNode:
    def __init__(self):
        self.val = 0
        self.children = {}
       
class Solution:
    """
    @param nums: 
    @return: the maximum result of ai XOR aj, where 0 Ã¢ÂÂ¤ i, j < n
    """

    def findMaximumXOR(self, arr):
        root = TrieNode()
        
        for key in arr:
            node = root
            for i in range(31, -1, -1):
                curbit = key >> i & 1
                if curbit not in node.children:
                    node.children[curbit] = TrieNode()
                node = node.children[curbit]
            node.val = key
        
        
        res = 0
        for key in arr:
            node = root
            temp = 0
            for i in range(31, -1, -1):
                curbit = key >> i & 1
                
                if 1^curbit in node.children:
                    temp += 1 << i
                    node = node.children[1^curbit]
                elif curbit in node.children:
                    node = node.children[curbit]
            res = max(temp, res)
            
        return res
```

