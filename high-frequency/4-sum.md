# 4 Sum

题目：

Given an array S of n integers, are there elements a, b, c, and d in S such that a + b + c + d = target?

Find all unique quadruplets in the array which gives the sum of target.

分析：

先排序再去重复, 和3 sum一样，前俩遍历相加sum1,当做target和后俩相比。

解法：

```text
    public List<List<Integer>> fourSum(int[] numbers, int target) {
        List<List<Integer>> ret = new ArrayList<List<Integer>>();
        if(numbers == null || numbers.length < 4)
            return new ArrayList<List<Integer>>(ret);

        int n = numbers.length;
        Arrays.sort(numbers);
        for(int i = 0; i < n-3; i++){
            if(i > 0 && numbers[i] == numbers[i-1])
                    continue;
            for(int j = i + 1; j < n-2; j++){
                if(j > i + 1 && numbers[j] == numbers[j-1])
                    continue;
                int sum1 = numbers[i] + numbers[j];
                int start = j + 1, end = n-1;
                while(start < end){
                    int sum2 = numbers[start] + numbers[end];
                    if(sum2 > target - sum1){
                        end --;
                    }else if(sum2 < target - sum1){
                        start ++;
                    }else{
                        int third = numbers[start];
                        int fourth = numbers[end];

                        List<Integer> quad = new ArrayList<Integer>(Arrays.asList(numbers[i],numbers[j], third, fourth));
                        ret.add(quad);

                        while(start < end && numbers[start] == third) 
                            start ++;
                         while(start < end && numbers[end] == fourth) 
                            end --; 
                    }
                }

            }
        }
        return ret;
    }
```

