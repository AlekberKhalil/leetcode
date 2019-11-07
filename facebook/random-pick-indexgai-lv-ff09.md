# Random Pick Index\(概率）

Given an array of integers with possible duplicates, randomly output the index of a given target number. You can assume that the given target number must exist in the array.

**Note:**  
The array size can be very large. Solution that uses too much extra space will not pass the judge.

**Example:**

```text
int[] nums = new int[] {1,2,3,3,3};
Solution solution = new Solution(nums);

// pick(3) should return either index 2, 3, or 4 randomly. Each index should have equal probability of returning.
solution.pick(3);

// pick(1) should return 0. Since in the array only nums[0] is equal to 1.
solution.pick(1);
```

分析

就是选0的话，每次都是1/count的概率

```text
At first, let's get clear that count is used to count the target number in nums. Say we now we have nums=[1,5,5,6,5,7,9,0] and the target is 5.

Now let's focus on the loop. When i=1, we get the first target number, and by rnd.nextInt(++count) we select a random number between [0, 1), which means actually you could only select 0, so the probability of making result = 1 is 1.

Keep going. In the loop where i = 2, we get the second number. Now we have to get a random number in {0,1}. So what should we do if we want to keep result = 1? It's simple: we have to make sure that, at this time, the random number generated should be 1 rather than 0 (otherwise the value of result will be changed), so the probability of keeping result = 1 is 1 * 1/2.

It is similar when we get the third target number, i.e., i = 4. Now we have to get a random number in {0,1,2}. If we still wish to keep result = 1, the only way is to randomly get number 1 or 2 rather than 0, and the probability is 2/3. So the total probability of keeping result = 1 will be 1 * 1/2 * 2/3.

Since we have four target number 5 here, the final probability of keeping result = 1 would be 1 * 1/2 * 2/3 * 3/4 = 1/4, which means the probability of picking index 0 is 1/4 as the problem required. The probability is the same if you wish to pick another index.

You may ask what is the probability of picking the last possible index 4? Well, it simpler. You may ignore all operations before the loop where i = 4, and the only thing you have to do is to get the random number 0 among {0,1,2,3} in the loop where i = 4, so the probability is exactly 1/4.
```

python用random.randrange。

这里重点是ret = i if randx == 0 else ret. 概率来说得randx里每个数取得概率一样，包括0.所以0的时候返回index

```text
class Solution:

    def __init__(self, nums):
        """
        :type nums: List[int]
        """
        self.nums = nums

    def pick(self, target):
        """
        :type target: int
        :rtype: int
        """
        cnt = 0
        ret = -1
        for i,v in enumerate(self.nums):
            if v == target:
                cnt += 1
                x = random.randrange(cnt)
                ret = i if x == 0 else ret
        return ret
```

