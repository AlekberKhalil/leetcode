# Pascal's Triangle

GivennumRows, generate the firstnumRowsof Pascal's triangle.

For example, givennumRows= 5,  
Return

```text
[     [1],    [1,1],   [1,2,1],  [1,3,3,1], [1,4,6,4,1]]
```

分析

recursive。每次从前面结果的最后一层计算出新层加入。 A\[i\] = A\[i-1\]+A\[i\],如果i-1或者i出界就用0。

用数组来初始化一个arraylist

```text
new ArrayList<Integer>(Arrays.asList(1,2,3,5,8,13,21));
```

```text
class Solution {    public List<List<Integer>> generate(int numRows) {        List<List<Integer>> ret = new ArrayList<>();        if(numRows < 1)            return ret;        if(numRows == 1){            ret.add(new ArrayList<Integer>(Arrays.asList(1)));            return ret;        }        List<List<Integer>> last = generate(numRows - 1);        List<Integer> level = last.get(last.size() - 1);        List<Integer> path = new ArrayList<Integer>();         for(int i = 0; i <= level.size(); i ++){            int prev = i - 1 < 0 ? 0 : level.get(i - 1);            int cur = i == level.size() ? 0 : level.get(i);            path.add(prev + cur);                    }        ret.addAll(last);        ret.add(path);        return ret;    }}
```

