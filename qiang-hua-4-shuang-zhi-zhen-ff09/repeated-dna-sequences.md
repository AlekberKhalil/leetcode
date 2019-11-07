# Repeated DNA Sequences

All DNA is composed of a series of nucleotides abbreviated as A, C, G, and T, for example: "ACGAATTCCG". When studying DNA, it is sometimes useful to identify repeated sequences within the DNA.

Write a function to find all the 10-letter-long sequences \(substrings\) that occur more than once in a DNA molecule.

**Example:**

```text
Input:
 s = "AAAAACCCCCAAAAACCCCCCAAAAAGGGTTT"


Output:
 ["AAAAACCCCC", "CCCCCAAAAA"]
```

分析

用**一个定长的滑动窗口，每次去match**

2个set， 一个装不重复的，如果不能装入，就装入重复的set

难点是index

```text
class Solution:
    def findRepeatedDnaSequences(self, s: str) -> List[str]:
        nonrepeated = set()
        repeated = set()
        l = len(s)
        for i in range(0,l-9):#此处为Index
            temp = s[i:i+10] #此处为10???
            if temp in nonrepeated:
                repeated.add(temp)
            else:
                nonrepeated.add(temp) 
        return list(repeated)
```

