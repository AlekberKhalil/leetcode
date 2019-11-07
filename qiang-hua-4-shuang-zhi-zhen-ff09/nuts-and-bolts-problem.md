# Nuts & Bolts Problem

Given a set of\_n\_nuts of different sizes and\_n\_bolts of different sizes. There is a one-one mapping between nuts and bolts. Comparison of a nut to another nut or a bolt to another bolt is not allowed. It means nut can only be compared with bolt and bolt can only be compared with nut to see which one is bigger/smaller.

We will give you a compare function to compare nut with bolt.

**Example**

Given nuts =`['ab','bc','dd','gg']`, bolts =`['AB','GG', 'DD', 'BC']`.

Your code should find the matching bolts and nuts.

one of the possible return:

nuts =`['ab','bc','dd','gg']`, bolts =`['AB','BC','DD','GG']`.

we will tell you the match compare function. If we give you another compare function.

the possible return is the following:

nuts =`['ab','bc','dd','gg']`, bolts =`['BC','AA','DD','GG']`.

So you must use the compare function that we give to do the sorting.

`The order of the nuts or bolts does not matter. You just need to find the matching bolt for each nut.`

分析

partion的变种，数组内部不可排序，用外部元素来Partition，得到Index后，quick sort左右递归

答案

```text
/** * public class NBCompare { *     public int cmp(String a, String b); * } * You can use compare.cmp(a, b) to compare nuts "a" and bolts "b", * if "a" is bigger than "b", it will return 1, else if they are equal, * it will return 0, else if "a" is smaller than "b", it will return -1. * When "a" is not a nut or "b" is not a bolt, it will return 2, which is not valid.*/public class Solution {    /**     * @param nuts: an array of integers     * @param bolts: an array of integers     * @param compare: a instance of Comparator     * @return: nothing     */    public void sortNutsAndBolts(String[] nuts, String[] bolts, NBComparator compare) {        // write your code here        if(nuts == null || bolts == null)            return;        if(nuts.length != bolts.length)            return;        quickSort(nuts, bolts, compare, 0, nuts.length-1);    }    public void quickSort(String[] nuts, String[] bolts, NBComparator compare, int l, int r){        if(l >= r) return;        int index = partition(nuts, bolts[l], compare, l, r);        partition(bolts, nuts[index], compare, l, r);        quickSort(nuts, bolts, compare, l, index-1);        quickSort(nuts, bolts, compare, index + 1, r);    }    public int partition(String[] str, String pivot, NBComparator compare, int l, int u){        //find out index with matching nut        for (int i = l; i <= u; i++) {            if (compare.cmp(str[i], pivot) == 0 ||                compare.cmp(pivot, str[i]) == 0) {                swap(str, i, l);                break;            }        }        String now = str[l];        int left = l;        int right = u;        while(left < right){            while (left < right &&            (compare.cmp(str[right], pivot) == -1 ||            compare.cmp(pivot, str[right]) == 1)) {                right--;            }            str[left] = str[right];            while(left < right && (compare.cmp(str[left], pivot) == 1 || compare.cmp(pivot, str[left]) == -1)){                left ++;            }            str[right] = str[left];        }        str[left] = now;        return left;    }    private void swap(String[] str, int l, int r) {        String temp = str[l];        str[l] = str[r];        str[r] = temp;    }};
```

