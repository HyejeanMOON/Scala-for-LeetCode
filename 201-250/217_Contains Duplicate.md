Given an array of integers, find if the array contains any duplicates. Your function should return true if any value appears at least twice in the array, and it should return false if every element is distinct.


### 解题思路
简单且经典的题。遍历数组，用Map记录value出现的次数。然后再次遍历key，如果key的value有大于等于2情况返回true。
#### Scala
```scala
object Solution {
    def containsDuplicate(nums: Array[Int]): Boolean = {
        var record:Map[Int,Int] = Map()
        //if(nums.length == 0) return false
        for(n <- nums){
            var temp = record.getOrElse(n,0)
            temp += 1
            record += (n -> temp)
        }
        var keys = record.keySet
        for(k <- keys){
            if(record.getOrElse(k,0) >= 2){
                return true
            }
        }
        false
    }
}
```