# Stamps（多重带总数限制）

**Stamps**  
Given a set of N stamp values \(e.g., {1 cent, 3 cents}\) and an upper limit K to the number of stamps that can fit on an envelope, calculate the largest unbroken list of postages from 1 cent to M cents that can be created.

For example, consider stamps whose values are limited to 1 cent and 3 cents; you can use at most 5 stamps. It’s easy to see how to assemble postage of 1 through 5 cents \(just use that many 1 cent stamps\), and successive values aren’t much harder:

* 6 = 3 + 3
* 7 = 3 + 3 + 1
* 8 = 3 + 3 + 1 + 1
* 9 = 3 + 3 + 3
* 10 = 3 + 3 + 3 + 1
* 11 = 3 + 3 + 3 + 1 + 1
* 12 = 3 + 3 + 3 + 3
* 13 = 3 + 3 + 3 + 3 + 1.

However, there is no way to make 14 cents of postage with 5 or fewer stamps of value 1 and 3 cents. Thus, for this set of two stamp values and a limit of K=5, the answer is M=13.

The most difficult test case for this problem has a time limit of 3 seconds.

## PROGRAM NAME: stamps

## INPUT FORMAT

| Line 1: | Two integers K and N. K \(1 &lt;= K &lt;= 200\) is the total number of stamps that can be used. N \(1 &lt;= N &lt;= 50\) is the number of stamp values. |
| :--- | :--- |
| Lines 2..end: | N integers, 15 per line, listing all of the N stamp values, each of which will be at most 10000. |

## SAMPLE INPUT \(file stamps.in\)

```text
5 2
1 3
```

## OUTPUT FORMAT

| Line 1: | One integer, the number of contiguous postage values starting at 1 cent that can be formed using no more than K stamps from the set. |
| :--- | :--- |


## SAMPLE OUTPUT \(file stamps.out\)

```text
13
```

分析

初始化都是最大数，f0=0。loop先V 后分组的value

```text
class Stamps:
    def getMaxAmount(self,K,N,values):
        maxValue = max(values)*K
        f = [maxValue+1]*(maxValue+1)
        f[0] = 0


        for j in range(1,maxValue + 1):
            for v in values:
                if j>=v:
                    f[j] = min(f[j],f[j-v] + 1)
            if f[j] > K:
                return j-1

        return maxValue

obj = Stamps()
ret = obj.getMaxAmount(5,2,[1,3])
print(ret)
```

