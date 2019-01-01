Given an integer n, return the number of trailing zeroes in n!.

Example 1:
```
Input: 3
Output: 0
Explanation: 3! = 6, no trailing zero.
```
Example 2:
```
Input: 5
Output: 1
Explanation: 5! = 120, one trailing zero.
```
Note: Your solution should be in logarithmic time complexity.

Difficulty:Easy  
Total Accepted:117.3K  
Total Submissions:317.1K  
Related Topics:Math

### 解题思路
这道题并没有什么难度，是让求一个数的阶乘末尾0的个数，也就是要找乘数中10的个数，而10可分解为2和5，而我们可知2的数量又远大于5的数量，那么此题即便为找出5的个数。仍需注意的一点就是，像25,125，这样的不只含有一个5的数字需要考虑进去。
#### Scala
```scala
object Solution {
    def trailingZeroes(n: Int): Int = {
        var temp = n
        var res = 0
        while(temp>0){
            res += temp/5
            temp/=5
        }
        res
    }
}
```