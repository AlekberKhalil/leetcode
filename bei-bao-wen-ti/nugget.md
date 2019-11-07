# nugget

**Beef McNuggets**  
**Hubert Chen**Farmer Brown's cows are up in arms, having heard that McDonalds is considering the introduction of a new product: Beef McNuggets. The cows are trying to find any possible way to put such a product in a negative light.

One strategy the cows are pursuing is that of \`inferior packaging'. \`\`Look,'' say the cows, \`\`if you have Beef McNuggets in boxes of 3, 6, and 10, you can not satisfy a customer who wants 1, 2, 4, 5, 7, 8, 11, 14, or 17 McNuggets. Bad packaging: bad product.''

Help the cows. Given N \(the number of packaging options, 1 &lt;= N &lt;= 10\), and a set of N positive integers \(1 &lt;= i &lt;= 256\) that represent the number of nuggets in the various packages, output the largest number of nuggets that can not be purchased by buying nuggets in the given sizes. Print 0 if all possible purchases can be made or if there is no bound to the largest number.

The largest impossible number \(if it exists\) will be no larger than 2,000,000,000.

## PROGRAM NAME: nuggets

## INPUT FORMAT

| Line 1: | N, the number of packaging options |
| :--- | :--- |
| Line 2..N+1: | The number of nuggets in one kind of box |

## SAMPLE INPUT \(file nuggets.in\)

```text
33610
```

## OUTPUT FORMAT

The output file should contain a single line containing a single integer that represents the largest number of nuggets that can not be represented or 0 if all possible purchases can be made or if there is no bound to the largest number.

## SAMPLE OUTPUT \(file nuggets.out\)

```text
17
```

分析

如果box里面的数的最大公约数不为1的话，那么所有组成的数，只可能是这个公约数的倍数，因此没有上限，输出为0。

```text
有个结论，有两个数p,q,且gcd(q,p)=1,则最大无法表示成px+qy（x>=0,y>=0)的数是pq-q-p（对于n>pq-q-p,都可以表示成px+qy；而pq-q-p,就无法表示成px+qy）。所以我们只需考虑小于pq-q-p的范围的最小值。对于一些无解的（全体最大公约数>1)，或无数解的（有一个‘1’），应提前判断。 其实我们可以干脆全取上界为256*256-256*2。直接进行背包就可以了。
```

多种背包

```text
can[j] = can[j-nuggets[i]] or can[j]
```

```text
class Nuggets:    def getMaxNum(self,N,nuggets):        sorted(nuggets)        maxValue = nuggets[-1]*nuggets[-2]        ngcd = nuggets[0]        for n in nuggets[1:]:            ngcd = gcd(ngcd,n)        if ngcd != 1:            return 0        can = [0]*(maxValue+1)        can[0] = 1        for i in range(N):            for j in range(nuggets[i], maxValue+1):                can[j] = can[j-nuggets[i]] or can[j]        for i in range(len(can)-1, -1,-1):            if not can[i]:                return i        return maxValuenuggets = [3,6,10]n = Nuggets()ret = n.getMaxNum(3,nuggets)print(ret)
```

