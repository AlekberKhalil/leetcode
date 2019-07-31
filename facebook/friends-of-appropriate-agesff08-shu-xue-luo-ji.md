# Friends Of Appropriate Ages（数学逻辑

Some people will make friend requests. The list of their ages is given and `ages[i]` is the age of the ith person.

Person A will NOT friend request person B \(B != A\) if any of the following conditions are true:

* `age[B]`

  `<`

  `= 0.5 * age[A] + 7`

* `age[B]`

  `>`

  `age[A]`

* `age[B]`

  `>`

  `100`

  `&`

  `&`

  `age[A]`

  `<`

  `100`

Otherwise, A will friend request B.

Note that if A requests B, B does not necessarily request A. Also, people will not friend request themselves.

How many total friend requests are made?

**Example 1:**

```text
Input: [16,16]
Output: 2
Explanation: 2 people friend request each other.
```

**Example 2:**

```text
Input: [16,17,18]
Output: 2
Explanation: Friend requests are made 17 -> 16, 18 -> 17.
```

**Example 3:**

```text
Input: [20,30,100,110,120]
Output: 
Explanation: Friend requests are made 110 -> 100, 120 -> 110, 120 -> 100.
```

Notes:

```text
1 <= ages.length <= 20000.
1 <= ages[i] <= 120.
```

分析

方法1 年级120内，map存每个age的个数。然后2个for遍历所有数字，相乘（注意= 是\*cnt\(b\)-1\)

方法2 用array和和数学公式。a,b 之间范围的和相减，\[a, b = a/2 +7\]

```text
class Solution {
     public int numFriendRequests(int[] ages) {

        int map[] = new int[121];
        for(int age: ages){
            map[age] ++;
        }
        int ret = 0;
        for(int i = 1; i <= 120; i ++){
            for(int j = 1; j <= 120; j ++){//次数需要从1开始而不是从i， 因为朋友关系是相互的。所以需要前去后来
                if(valid(i,j)){
                    ret += map[i] * (i == j ? map[j] - 1 : map[j]);
                }
            }

        }
        return ret;
    }
    public boolean valid(int a, int b) {
        return !(b <= 0.5 * a + 7 || b > a || (b > 100 && a < 100)); //其实条件2和3重复了
    }
}
```

```text
class Solution {
    public int numFriendRequests(int[] ages) { //优化2，另一数组sums记录范围，这样计算count不用2 for，直接找范围内个数即可
        int[] nums = new int[121], sums = new int[121];
        for (int age : ages) nums[age]++; //记录每个年龄多少人
        for (int i = 1; i < sums.length; i++) sums[i] = sums[i - 1] + nums[i]; //相当于记录小于i的有多少人
        int res = 0;
        for (int i = 15; i < sums.length; i++) { //i / 2 + 7 < i -> i>14
            if (nums[i] == 0) continue; //0一定要跳过，否则后面是负数
            int count = sums[i] - sums[i / 2 + 7]; //(i/2+7, i] 有多少个
            res += (count - 1) * nums[i]; //不能和自身request
        }
        return res;
    }
}
```

