# Majority Number II

题目：

Given an array of integers, the majority number is the number that occurs more than 1/3 of the size of the array.

分析：

3个数不一样就扔掉, 出现一个不一样的数，用新数抵消掉前俩数,注意最后还需要一个loop 比较2个candidates.

解法：

```text
    public int majorityNumber(ArrayList<Integer> nums) {        // write your code        int count1 = 0, count2 = 0, c1 = -1, c2 = -1;        for(int i = 0; i < nums.size(); i++){            if(nums.get(i) == c1){                count1++;            }else if(nums.get(i) == c2){                count2++;            }else if(count1 == 0){                c1 = nums.get(i);                count1 = 1;            }else if(count2 == 0){                c2 = nums.get(i);                count2 = 1;            }else {                count1--;                count2--;            }        }        //可能c1已经用来抵消掉前面很多数，所以count1<count2 所以要重新loop比较一次。        count1 = count2 = 0;        for (int i = 0; i < nums.size(); i++) {            if (nums.get(i) == c1) {                count1++;            } else if (nums.get(i) == c2) {                count2++;            }        }            return count1 > count2 ? c1 : c2;    }
```

