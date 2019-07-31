# Ugly Number

Write a program to check whether a given number is an ugly number.

Ugly numbers are positive numbers whose prime factors only include`2, 3, 5`. For example,`6, 8`are ugly while`14`is not ugly since it includes another prime factor`7`.

Note that`1`is typically treated as an ugly number.

分析

都是正数

```text
class Solution {
    public boolean isUgly(int num) {
        if(num < 1)
            return false;
        if(num == 1)
            return true;
        int[] arr = {2,3,5};
        while(num != 1){
            boolean canMul = false;
            for(int i : arr){
                if(num % i == 0){
                    num /= i;
                    canMul = true;
                }
            }
            if(!canMul)
                return false;
        }
        return true;
    }
}
```

