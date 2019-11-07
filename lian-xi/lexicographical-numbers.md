# Lexicographical Numbers

问题：

Given an integer n, return 1 - n in lexicographical order.

For example, given 13, return: \[1,10,11,12,13,2,3,4,5,6,7,8,9\].

Please optimize your algorithm to use less time and space. The input size may be as large as 5,000,000.

思路：

给出一个整数n，返回 1 到 n 的词典顺序。

比如，给出13，返回 \[1,10,11,12,13,2,3,4,5,6,7,8,9\]。

请优化你的代码来使用更少的时间和空间。输入范围会达到5000000。

分析

问题的关键在于理清“词典顺序”是什么样的。

词典顺序就是10比2靠前，101比11靠前，110比11靠后，你可以简单的尝试一下把数字都转换成字符串数组，然后对字符串数组进行 Arrays.sort\(\)，就会得到字符串下词典顺序的数字。但是这个方法因为用了排序，是会超时的。

所以我们的做法大致顺序如下：

1、如果一个数乘以十以后没有超过n，那它后面紧挨着的应该是它的十倍，比如1,10,100。

2、如果不满足1，那就应该是直接加一，比如n为13的时候，前一个数为12，120超过了n，那接着的应该是13。但是这里要注意如果前一个数的个位已经是9或者是它就是n了，那就不能加一了，比如 n = 25，前一个数为19，下一个数应该为2而不是19+1=20。25的下一个也没有26了。

3、如果不满足2，比如19后面应该接2而不是20，这时候应该将19除以10再加一，比如n=500，399的下一个应该是4，那就是除以十，个位还是9，继续除以10，得到3，加一得到4。

```text
class Solution:    def lexicalOrder(self, n):        """        :type n: int        :rtype: List[int]        """        cur = 1        ret = []        for i in range(n):            ret.append(cur)            if cur*10 <=n:                cur *= 10            elif cur%10!=9 and cur+1<=n:                cur += 1            else:                while (cur//10)%10 == 9:                    cur//=10                cur=(cur//10)+1        return ret
```

