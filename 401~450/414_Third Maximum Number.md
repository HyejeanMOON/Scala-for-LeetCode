Given a non-empty array of integers, return the third maximum number in this array. If it does not exist, return the maximum number. The time complexity must be in O(n).

Example 1:
```
Input: [3, 2, 1]

Output: 1

Explanation: The third maximum is 1.
```
Example 2:
```
Input: [1, 2]

Output: 2

Explanation: The third maximum does not exist, so the maximum (2) is returned instead.
```
Example 3:
```
Input: [2, 2, 3, 1]

Output: 1
```
Explanation:  
Note that the third maximum here means the third maximum distinct number.
Both numbers with value 2 are both considered as second maximum.

Difficulty:Easy  
Total Accepted:56.6K  
Total Submissions:201.9K  

Related Topics : Array

### 解题思路
#### Scala
```scala
object Solution {
    def thirdMax(nums: Array[Int]): Int = {
        var first:Long = scala.Long.MinValue
        var second:Long = scala.Long.MinValue
        var third:Long = scala.Long.MinValue
        var count = 0
        for(n <- nums){
            if(n > first) {
                third = second
                second = first
                first = n
                count += 1
            }else if(n > second && n < first){
                third = second
                second = n
                count += 1
            }else if(n > third && n < second){
                third = n
                count += 1
            }
        }
        if(count >= 3) return third.toInt
        else return first.toInt
        third.toInt
    }
}
```