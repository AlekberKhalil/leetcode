# Flatten Nested List Iterator

Given a nested list of integers, implement an iterator to flatten it.

Each element is either an integer, or a list -- whose elements may also be integers or other lists.

**Example 1:**  
Given the list`[[1,1],2,[1,1]]`,

By callingnextrepeatedly untilhasNextreturns false, the order of elements returned bynextshould be:`[1,1,2,1,1]`.

**Example 2:**  
Given the list`[1,[4,[6]]]`,

By callingnextrepeatedly untilhasNextreturns false, the order of elements returned bynextshould be:`[1,4,6]`.

分析

Stack里可以存Iterator

可以边赋值边判断

不是很懂这题

```text
Stack<Iterator<Integer>>
if((nxt = s.peek().next()).isInteger())
```

```text
/**
 * // This is the interface that allows for creating nested lists.
 * // You should not implement it, or speculate about its implementation
 * public interface NestedInteger {
 *
 *     // @return true if this NestedInteger holds a single integer, rather than a nested list.
 *     public boolean isInteger();
 *
 *     // @return the single integer that this NestedInteger holds, if it holds a single integer
 *     // Return null if this NestedInteger holds a nested list
 *     public Integer getInteger();
 *
 *     // @return the nested list that this NestedInteger holds, if it holds a nested list
 *     // Return null if this NestedInteger holds a single integer
 *     public List<NestedInteger> getList();
 * }
 */
public class NestedIterator implements Iterator<Integer> {
    Stack<Iterator<NestedInteger>> s;
    NestedInteger nxt;
    public NestedIterator(List<NestedInteger> nestedList) {
        s = new Stack<Iterator<NestedInteger>>();
        s.push(nestedList.iterator());
    }

    @Override
    public Integer next() {
        return nxt != null ? nxt.getInteger() :  null;
    }

    @Override
    public boolean hasNext() {
        while(!s.isEmpty()){
            if(!s.peek().hasNext()){
                s.pop();
            }else if((nxt = s.peek().next()).isInteger()){
                return true;
            }else{
                s.push(nxt.getList().iterator());
            }
        }
        return false;
    }

}

/**
 * Your NestedIterator object will be instantiated and called as such:
 * NestedIterator i = new NestedIterator(nestedList);
 * while (i.hasNext()) v[f()] = i.next();
 */
```

