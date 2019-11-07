# Expression Add Operators（dfs\)

Given a string that contains only digits`0-9`and a target value, return all possibilities to add**binary**operators \(not unary\)`+`,`-`, or`*`between the digits so they evaluate to the target value.

**Example 1:**

```text
Input:num = "123", target = 6Output: ["1+2+3", "1*2*3"]
```

**Example 2:**

```text
Input:num = "232", target = 8Output: ["2*3+2", "2+3*2"]
```

**Example 3:**

```text
Input:num = "105", target = 5Output: ["1*0+5","10-5"]
```

**Example 4:**

```text
Input:num = "00", target = 0Output: ["0+0", "0-0", "0*0"]
```

**Example 5:**

```text
Input:num = "3456237490", target = 9191Output: []
```

分析

**Complexity:**

O\(4^n\)

```text
T(n) = 3 * T(n-1) + 3 * T(n-2) + 3 * T(n-3) + ... + 3 *T(1);T(n-1) = 3 * T(n-2) + 3 * T(n-3) + ... 3 * T(1);Thus T(n) = 4T(n-1);
```

dfs 因为中间数字可以任何结合成为新数，start做dfs参数，end由for loop决定

这里pos,path都有，多了个prevn记录之前得数，是为了\*模仿栈

注意这里start end都包含在内

```text
class Solution:    def addOperators(self, num, target):        """        :type num: str        :type target: int        :rtype: List[str]        """        ret = []        def dfs(exp, eval, start, prevn):  # exp and eval看做路径，start是Pos,唯一多的这个Prevn是为了*            if start == len(num) and eval == target:                ret.append(exp)                return            for i in range(start, len(num)):                strcur = num[start:i + 1]                ncur = int(strcur)                if len(str(ncur)) != len(strcur):                    break  # 说明以0开头，这样这条路径后面情况也不必考虑                if start == 0:                    dfs(exp + strcur, ncur, i + 1, ncur)                else:                    dfs(exp + '+' + strcur, eval + ncur, i + 1, ncur)                    dfs(exp + '-' + strcur, eval - ncur, i + 1, -ncur)  # 这里-ncur是为了将来*，不需要记录之前的符号                    dfs(exp + '*' + strcur, eval - prevn + prevn * ncur, i + 1, prevn * ncur)        dfs('', 0, 0, 0)        return ret
```

