# Filling Bookcase Shelves

We have a sequence of`books`: the`i`-th book has thickness`books[i][0]`and height`books[i][1]`.

We want to place these books**in order** onto bookcase shelves that have total width`shelf_width`.

We choose some of the books to place on this shelf \(such that the sum of their thickness is`<= shelf_width`\), then build another level of shelf of the bookcase so that the total height of the bookcase has increased by the maximum height of the books we just put down. We repeat this process until there are no more books to place.

Note again that at each step of the above process,the order of the books we place is the same order as the given sequence of books. For example, if we have an ordered list of 5 books, we might place the first and second book onto the first shelf, the third book on the second shelf, and the fourth and fifth book on the last shelf.

Return the minimum possible height that the total bookshelf can be after placing shelves in this manner.

**Example 1:**

![](https://assets.leetcode.com/uploads/2019/06/24/shelves.png)

```text
Input:
 books = [[1,1],[2,3],[2,3],[1,1],[1,1],[1,1],[1,2]], shelf_width = 4

Output:
 6

Explanation:

The sum of the heights of the 3 shelves are 1 + 3 + 2 = 6.
Notice that book number 2 does not have to be on the first shelf.
```

**Constraints:**

```text
1 <= books.length <= 1000
1 <= books[i][0] <= shelf_width <= 1000
1 <= books[i][1] <= 1000
```

分析

dp\[w\]表示最高高度。背包，可以放在当前行和上一行。

上一行的状态太多，无法得到最大height,干脆直接while loop。从当前书起while，i-&gt;j \(j&gt;0\) 本书能放在一个架子上。

```text
class Solution:
    def minHeightShelves(self, books: List[List[int]], shelf_width: int) -> int:
        n = len(books)
        dp = [0]*(n+1)
        for i in range(1,n+1):
            w = books[i-1][0]
            h = books[i-1][1]
            dp[i] = dp[i-1] + h
            j = i-1
            while j>0 and w + books[j-1][0]<=shelf_width: #实在无法用状态表示当前书架所有书时候，直接while loop吧
                w = w + books[j-1][0]
                h = max(h, books[j-1][1])
                dp[i] = min(dp[j-1]+h,dp[i])#注意是dp[j-1]，当前j的前一个状态
                j -= 1
        return dp[-1]
```

