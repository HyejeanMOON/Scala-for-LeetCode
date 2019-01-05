Given an array of numbers nums, in which exactly two elements appear only once and all the other elements appear exactly twice. Find the two elements that appear only once.

For example:
```
Given nums = [1, 2, 1, 3, 2, 5], return [3, 5].
```
Note:
The order of the result is not important. So in the above example, [5, 3] is also correct.
Your algorithm should run in linear runtime complexity. Could you implement it using only constant space complexity?

Difficulty:Medium  
Total Accepted:81.6K  
Total Submissions:153K  
Related Topics:Bit Manipulation

### 解题思路

### Scala
```scala


```

该方法符合线性时间复杂度，但空间复杂度不符合。
#### Scala
```scala
object Solution {
    def singleNumber(nums: Array[Int]): Array[Int] = {
        if(nums.isEmpty) return Array()
        var record:Map[Int,Int]=Map()
        var res:Array[Int] = Array()
        for(n <- nums){
            var temp = record.getOrElse(n,0)
            temp += 1
            record += (n -> temp)
        }
        for(k <- record.keySet){
            if(record.getOrElse(k,0)==1) res = res :+ k
        }
        res
    }
}
```