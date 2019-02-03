You have a total of n coins that you want to form in a staircase shape, where every k-th row must have exactly k coins.

Given n, find the total number of full staircase rows that can be formed.

n is a non-negative integer and fits within the range of a 32-bit signed integer.

Example 1:
```
n = 5

The coins can form the following rows:
¤
¤ ¤
¤ ¤

Because the 3rd row is incomplete, we return 2.
```
Example 2:
```
n = 8

The coins can form the following rows:
¤
¤ ¤
¤ ¤ ¤
¤ ¤

Because the 4th row is incomplete, we return 3.
```
Difficulty:Easy  
Total Accepted:43.5K  
Total Submissions:119.5K  
Related Topics：Math, Binary Search

### 解题思路
循环累加，然后进行判断。  
判断规则是如果res等于n则把level直接返回，如果res大于n则返回level-1。 还有这里的res要设置成long，要不会溢出。
#### Scala
```scala
object Solution {
    def arrangeCoins(n: Int): Int = {
        var res:Long = 0
        var level = 0
        while(res<n){
            level += 1
            res += level
            if(res == n) return level
            else if(res > n) return level-1
        }
        0
    }
}
```