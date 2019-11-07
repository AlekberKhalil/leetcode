# Reorder Log Files

You have an array of`logs`. Each log is a space delimited string of words.

For each log, the first word in each log is an alphanumeric_identifier_. Then, either:

* Each word after the identifier will consist only of lowercase letters, or;
* Each word after the identifier will consist only of digits.

We will call these two varieties of logs_letter-logs\_and\_digit-logs_. It is guaranteed that each log has at least one word after its identifier.

Reorder the logs so that all of the letter-logs come before any digit-log. The letter-logs are ordered lexicographically ignoring identifier, with the identifier used in case of ties. The digit-logs should be put in their original order.

Return the final order of the logs.

**Example 1:**

```text
Input: 
["a1 9 2 3 1","g1 act car","zo4 4 7","ab1 off key dog","a8 act zoo"]
Output: 
["g1 act car","a8 act zoo","ab1 off key dog","a1 9 2 3 1","zo4 4 7"]
```

分析

字母数字拆成2个list，字母List排序后合并

```text
class Solution:
    def reorderLogFiles(self, logs: List[str]) -> List[str]:
        letters,nums = [],[]
        for l in logs:
            if l[-1].isdigit():
                nums.append(l)
            else:
                letters.append(l)
        letters.sort(key = lambda x: (x[x.find(' '):], x[: x.find(' ')]))

        return letters+nums
```

