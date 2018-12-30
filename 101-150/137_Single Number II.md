Given a non-empty array of integers, every element appears three times except for one, which appears exactly once. Find that single one.

Note:

Your algorithm should have a linear runtime complexity. Could you implement it without using extra memory?

Example 1:
```
Input: [2,2,3,2]
Output: 3
```
Example 2:
```
Input: [0,1,0,1,0,1,99]
Output: 99
```
 
Difficulty:Medium  
Total Accepted:134.6K  
Total Submissions:314.9K  
Related Topics:Bit Manipulation

### 解题思路






---

不符合要求，但是accepted
#### Scala
```scala
object Solution {
    def singleNumber(nums: Array[Int]): Int = {
        var len = nums.length
        var record:Map[Int,Int] = Map()
        for(n <- nums){
            var temp = record.getOrElse(n,0)
            temp += 1
            record += (n -> temp)
        }
        var keys = record.keySet
        for(k <- keys){
            if(record.getOrElse(k,0)==1){
                return k
            }
        }
        0
    }
}
```
