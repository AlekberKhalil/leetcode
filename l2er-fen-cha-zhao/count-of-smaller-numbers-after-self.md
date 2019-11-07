# Count of Smaller Numbers After Self

You are given an integer arraynumsand you have to return a newcountsarray. Thecountsarray has the property where`counts[i]`is the number of smaller elements to the right of`nums[i]`.

**Example:**

```text
Given nums = [5, 2, 6, 1]To the right of 5 there are 2 smaller elements (2 and 1).To the right of 2 there is only 1 smaller element (1).To the right of 6 there is 1 smaller element (1).To the right of 1 there is 0 smaller element.
```

Return the array`[2, 1, 1, 0]`.

分析

倒序开始，把每个数顺序二分插入一个数组，当前Index就是比它小的数字count.之所以倒序是因为要算该数右边的数组。

还可以用binary search tree 做

```text
class Solution {    public List<Integer> countSmaller(int[] nums) {        List<Integer> ret = new ArrayList<Integer>();        Integer[] temp = new Integer[nums.length];        List<Integer> sorted = new ArrayList<Integer>();        if(nums == null || nums.length == 0){            return ret;        }        for(int i = nums.length - 1; i >= 0; i --){            int index = find(sorted, nums[i]);            sorted.add(index, nums[i]);            temp[i] = index;        }        return Arrays.asList(temp);    }    private int find(List<Integer> nums, int target){        int n = nums.size();        if(n == 0)            return 0;        if(nums.get(0) > target){            return 0;        }         if(nums.get(n-1) < target){            return n;        }        int s = 0, e = n - 1;        while(s + 1 < e){            int m = s + (e - s)/2;            if(nums.get(m) < target){                s = m;            }else{                e = m;                            }        }        if(nums.get(e) >= target){            return e;        }        return s;    }}
```

