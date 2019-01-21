Given a non-negative integer n, count all numbers with unique digits, x, where 0 ≤ x < 10n.

Example:
```
Given n = 2, return 91. (The answer should be the total numbers in the range of 0 ≤ x < 100, excluding [11,22,33,44,55,66,77,88,99])
```
Credits:
Special thanks to @memoryless for adding this problem and creating all test cases.

Difficulty:Medium  
Total Accepted:48K  
Total Submissions:104.1K  
Related Topics:Math, Dynamic Programming, Backtracking

### 解题思路
这道题让我们找一个范围内的各位上不相同的数字，比如123就是各位不相同的数字，而11,121,222就不是这样的数字。那么我们根据提示中的最后一条可以知道，一位数的满足要求的数字是10个(0到9)，二位数的满足题意的是81个，[10 - 99]这90个数字中去掉[11,22,33,44,55,66,77,88,99]这9个数字，还剩81个。通项公式为f(k) = 9 * 9 * 8 * ... (9 - k + 2)，那么我们就可以根据n的大小，把[1, n]区间位数通过通项公式算出来累加起来即可。
#### Scala
```scala
object Solution {
    def countNumbersWithUniqueDigits(n: Int): Int = {
        if(n==0) return 1
        if(n==1) return 10
        var res = 10
        var count = 9
        for(i <- 2 to n){
            count *= (11-i)
            res += count
        }
        res
    }
}
```