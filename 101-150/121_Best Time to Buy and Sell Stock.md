Say you have an array for which the ith element is the price of a given stock on day i.

If you were only permitted to complete at most one transaction (ie, buy one and sell one share of the stock), design an algorithm to find the maximum profit.

Example 1:
```
Input: [7, 1, 5, 3, 6, 4]
Output: 5

max. difference = 6-1 = 5 (not 7-1 = 6, as selling price needs to be larger than buying price)
```
Example 2:
```
Input: [7, 6, 4, 3, 1]
Output: 0

In this case, no transaction is done, i.e. max profit = 0.
```

Difficulty:Easy  
Total Accepted:276.8K  
Total Submissions:646.9K  
Related Topics: Array, Dynamic Programming

### 解题思路
遍历数组，一直在记录最小值，以及最大值。相减就是答案。
#### Scala
```scala
object Solution {
    def maxProfit(prices: Array[Int]): Int = {
        var buy = scala.Int.MaxValue
        var profit = 0
        for(p <- prices){
            //查找该数组中的最小值
            buy = scala.math.min(buy,p)
            //查找该数组中的最大值
            profit = scala.math.max(profit,p-buy)
        }
        profit
    }
}
```

#### Java
```java
class Solution {
    public int maxProfit(int[] prices) {
        int buy = java.lang.Integer.MAX_VALUE;
        int profit = 0;
        for(Integer p:prices){
            buy = Math.min(buy,p);
            profit = Math.max(profit,p-buy);
        }
        return profit;
    }
}
```