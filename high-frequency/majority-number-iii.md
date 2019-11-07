# Majority Number III

题目：

Given an array of integers and a number k, the majority number is the number that occurs more than 1/k of the size of the array.

分析：

k数抵消，用大小为k-1的hashmap, 发现k数时，把前k-1的个数都减少一个

偷懒直接用了最大count的数

解法：

```text
    public int majorityNumber(ArrayList<Integer> nums, int k) {        // write your code        HashMap<Integer, Integer> h = new HashMap<Integer, Integer>();        int max = Integer.MIN_VALUE, maxNum= 0;        for(int i = 0; i < nums.size(); i++){            if(h.containsKey(nums.get(i))){                h.put(nums.get(i), h.get(nums.get(i))+1);            }else{                h.put(nums.get(i), 1);            }            if(max < h.get(nums.get(i))){                max = h.get(nums.get(i));                maxNum = nums.get(i);            }        }        return maxNum;    }
```

