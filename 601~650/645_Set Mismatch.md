The set S originally contains numbers from 1 to n. But unfortunately, due to the data error, one of the numbers in the set got duplicated to another number in the set, which results in repetition of one number and loss of another number.

Given an array nums representing the data status of this set after the error. Your task is to firstly find the number occurs twice and then find the number that is missing. Return them in the form of an array.

Example 1:
```
Input: nums = [1,2,2,4]
Output: [2,3]
```
Note:  
The given array size will in the range [2, 10000].
The given array's numbers won't have any order.

Difficulty:Easy  
Total Accepted:25.4K  
Total Submissions:64.1K  
Related Topics:Hash Table, Math

### 解题思路
使用hash map记录数字出现的频率。然后遍历map，如果值等于0则记录到miss中，如果值等于2则记录到twice中。
#### Scala
```scala
object Solution {
    def findErrorNums(nums: Array[Int]): Array[Int] = {
        var len = nums.length
        var miss:Array[Int] = Array()
        var twice:Array[Int] = Array()
        var res:Array[Int] = Array()
        var record:Map[Int,Int] = Map()
        for(i <- 0 until len){
            var temp = record.getOrElse(nums(i),0)
            temp += 1
            record += (nums(i)->temp)
        }
        for(i <- 0 until len){
            var temp = record.getOrElse((i+1),0)
            if(temp == 0) miss = miss :+ (i+1)
            if(temp == 2) twice = twice :+ (i+1)
        }
        res = res ++: twice
        res = res ++: miss
        res
    }
}
```