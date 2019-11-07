# Longest Consecutive Sequence

Given an unsorted array of integers, find the length of the longest consecutive elements sequence.

For example,  
Given`[100, 4, 200, 1, 3, 2]`,  
The longest consecutive elements sequence is`[1, 2, 3, 4]`. Return its length:`4`.

Your algorithm should run in O\(n\) complexity.

分析

自己做的方法不好，用了Map和queue。可以用Hashset代替map和queue,先加入全部元素，然后再慢慢去除。

```text
class Solution {    public int longestConsecutive(int[] nums) {        Map<Integer, Integer> map = new HashMap<Integer, Integer>();        Queue<Integer> q = new LinkedList<Integer>();        int max = 0;        for(int n : nums){            q.offer(n);            if(!map.containsKey(n)){                map.put(n, 1);            }else{                map.put(n, map.get(n) + 1);            }                    }         while(!q.isEmpty()){            int cur = q.poll();            int len = 1;            int up = cur + 1;            while(map.containsKey(up)){                len ++;                q.remove(up);                up ++;            }            int down = cur - 1;             while(map.containsKey(down)){                len ++;                q.remove(down);                down --;            }             max = Math.max(max, len);        }        return max;    }}
```

用hashset做

```text
class Solution {    public int longestConsecutive(int[] nums) {        Set<Integer> s = new HashSet<>();        int max = 0;        for(int n : nums){            s.add(n);                }         for(int i : nums){ //这里loop nums,不是set，要不会有currentmodification错误                      int len = 1;            int up = i + 1;            while(s.contains(up)){                len ++;                s.remove(up ++);            }            int down = i - 1;             while(s.contains(down)){                len ++;                s.remove(down --);            }             max = Math.max(max, len);        }        return max;    }}
```

