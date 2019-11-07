# 3 Sum

题目： Given an array S of n integers, are there elements a, b, c in S such that a + b + c = 0? Find all unique triplets in the array which gives the sum of zero.

Elements in a triplet \(a,b,c\) must be in non-descending order. \(ie, a ≤ b ≤ c\) The solution set must not contain duplicate triplets.

分析：

这里是不重复的情况，重复的话可以算counter map，然后用排列组合计算

首先，他要求结果的triplets有顺序，所以肯定需要O\(nlogn\)的sort。

除此之外，要注意每个循环的最开始需要验证nums\[i\] != nums\[i - 1\]以保证不会出现重复的数据。

最后，因为题目是3Sum是否为0，所以需要取其中一个数作为target，然后对剩余两个数做2Sum。

```text
特别注意，在最外层做for循环的时候，i = 0 ~ size - 2是可以的，但是i = 2 ~ size是不行的，
因为你跳过重复i的时候不能保证前面的所有nums[i]都不会在被用到，所以会丢解。
```

解答：

```text
    public List<List<Integer>> threeSum(int[] nums) {
        List<List<Integer>> ret = new ArrayList<>();
        Arrays.sort(nums);
        for(int j = 0; j < nums.length - 2; j++){
            if(j == 0 || j > 0 && nums[j] != nums[j-1]){//i去duplicate
                int first = nums[j], start = j + 1, end = nums.length - 1;            
                while(start < end){
                    if(nums[start] + nums[end] < -first){
                        start ++;
                    }else if (nums[start] + nums[end] > -first){
                        end --;
                    }else{
                        List<Integer> triple = new ArrayList<Integer>();
                        triple.add(first);
                        int second = nums[start], third = nums[end];
                        triple.add(second);
                        triple.add(third);
                        ret.add(triple);
                        //剩下俩数去duplicate
                        while(start < end && second == nums[start]) 
                            start ++;
                        while(start < end && third == nums[end]) 
                            end --;    
                    }
                }
            }
        }        
        return ret;
    }
```

