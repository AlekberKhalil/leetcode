# 强化4\(双指针）

1. 一个数组，从两边往中间移动（对撞型）
2. 一个数组，同时向前移动（前向型）
3. 两个数组（并行型）

## 对撞型

* two sum类 -&gt;灌水类
* partion类

**partition** 

quick select -&gt; kth largest element 第K大（比如中位数）

heap（priority queue\)-&gt;前k大: O\(NlogK\)如果把heap size设为k的话。

top k smallest

* maxheap -cmp size k
* minheap pop k times

quick select vs quick sort

都要partition.quick select 是quick sort的一个步骤，quick select 每次都会丢一半 所以O（logn） quick sort 之后还要继续做partition操作，递归。 O（nlogn）

partition问题模板

```text
public int partition(int[] nums, int l, int r){
    int left = l, right = r, pivot = nums[left];
    while(left < right){
        while(left < right && nums[right] >= pivot){
            right --;
        }
        nums[left] = nums[right];
        while(left < right && nums[left] <= pivot){
            left ++;
        }
        nums[right] = nums[left];
    }
    nums[left] = pivot;
    return left;
}
```

## quick sort 模板

```text
public void sortIntegers2(int[] A) {
        quickSort(A, 0, A.length - 1);
    }

    private void quickSort(int[] A, int start, int end) {
        if (start >= end) {
            return;
        }

        int left = start, right = end;
        // key point 1: pivot is the value, not the index
        int pivot = A[(start + end) / 2];

        // key point 2: every time you compare left & right, it should be 
        // left <= right not left < right
        while (left <= right) {
            // key point 3: A[left] < pivot not A[left] <= pivot
            while (left <= right && A[left] < pivot) {
                left++;
            }
            // key point 3: A[right] > pivot not A[right] >= pivot
            while (left <= right && A[right] > pivot) {
                right--;
            }
            if (left <= right) {
                int temp = A[left];
                A[left] = A[right];
                A[right] = temp;

                left++;
                right--;
            }
        }

        quickSort(A, start, right);
        quickSort(A, left, end);
    }
```

## 前向型或者追击型

* 窗口类 -&gt;子串子数组可以往窗口类想 substring，subarray
* 快慢类

## 窗口类 vs sliding window

sliding window 的窗口大小固定.窗口类就是找个窗口 满足某条件，窗口最大或者最小

总结固定大小的窗口：[https://segmentfault.com/a/1190000012931296](https://segmentfault.com/a/1190000012931296)

固定长度模板：K-Substring with K different characters\(sliding window\)

for loop strs/nums长度，检测map或者数组长度，cnt ++/--

**不固定长度：**

窗口类的指针i,j 一直都是往前走， 都不回头，所以只遍历2n次，O（n）j永远在i前面，i在追，i,j围成窗口类。

窗口类指针移动模板

```text
for(int i = 0; i < n; i++){
    while(j < n){
        if(条件满足){
            j++;
            更新j状态
        }else（不满足条件）{
            break;
        }   
    }
    更新i状态
}
```

总结

* 优化思想通过两层for循环而来
* 外层指针依然是依次遍历
* 内侧指针证明是否需要回退

Tips:

Character.isLowerCase

Character.isUpperCase

```text
int[] copy = Arrays.copyOf(nums, n);
```

**带map的双指针**

**strStr和anagrams比较：**

相同点：就是len== t.length

不同点：

strStr 顺序需要，不要map。所以i,j初始就是t的间隔，每次比完一起走+

anagram 顺序不需要，所以**Map**

**用map类就是无序，有序的话可以用2个指针各指向一个arr开始比较。**

**min/max substring 双指针通用模板**

\*\*\*\*[**https://leetcode.com/problems/find-all-anagrams-in-a-string/discuss/92007/Sliding-Window-algorithm-template-to-solve-all-the-Leetcode-substring-search-problem.**](https://leetcode.com/problems/find-all-anagrams-in-a-string/discuss/92007/Sliding-Window-algorithm-template-to-solve-all-the-Leetcode-substring-search-problem.)\*\*\*\*

一个map存char count。头尾指针，尾前进到满足条件，头缩进到不满足条件。2个while一个头一个尾。注意min/max的位置

双指针模板：[https://leetcode.com/problems/find-all-anagrams-in-a-string/discuss/92007/Sliding-Window-algorithm-template-to-solve-all-the-Leetcode-substring-search-problem.](https://leetcode.com/problems/find-all-anagrams-in-a-string/discuss/92007/Sliding-Window-algorithm-template-to-solve-all-the-Leetcode-substring-search-problem.)

模板不能做这个Longest Substring with At Least K Repeating Characters（递归）

[Minimum Window Substring](https://leetcode.com/problems/minimum-window-substring/)

```text
int findSubstring(string s){
        vector<int> map(128,0);
        int counter; // check whether the substring is valid
        int begin=0, end=0; //two pointers, one point to tail and one  head
        int d; //the length of substring

        for() { /* initialize the hash map here */ }

        while(end<s.size()){

            if(map[s[end++]]-- ?){  /* modify counter here */ }//pre临界这里，完了就被减
,map和end都要update,只有counter在if里

            while(/* counter condition */){ 

                 /* update d here if finding minimum*/

                //increase begin to make it invalid/valid again

                if(map[s[begin++]]++ ?){ /*modify counter here*/ }//map和end都要update,只有counter在if里


            }  

            /* update d here if finding maximum*/
        }
        return d;
  }
```

leetcode:

904

总结做法：

**固定长度**且要求**顺序**，可以直接str比较str，注意loop坐标的取值，不能取到尾。

**固定程度不顺序**的话，可以用map和count

subarray-product-less-than-k 重要结论：每加入一个新数字，多出来e-s个数组，决定于起始数字位置。unique-letter-string也用了这个结论，dp里每次多个数字，就多e-s个新数组。

Subarrays with K Different Integers：1用atmost K做:f\(exactly K\) = f\(atMost K\) - f\(atMost K-1\).

2达到合格K的i,j之间有x个num/char重复，res+= x+1

