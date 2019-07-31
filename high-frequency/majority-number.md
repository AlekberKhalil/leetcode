# Majority Number

题目：

Given an array of integers, the majority number is the number that occurs more than half of the size of the array. Find it.

分析：

扔掉俩不一样的数，剩下的数就是主元素

解法：

```text
public int majorityNumber(ArrayList<Integer> nums) {
        // write your code
        int count = 0, ret = -1;
        for(int i = 0; i < nums.size(); i++){
            if(count == 0){
                ret = nums.get(i);
                count = 1;
            }else if(nums.get(i) != ret){
                count--;
            }else{
                count++;
            }
        }
        return ret;
    }
```

