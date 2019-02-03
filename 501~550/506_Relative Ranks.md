Given scores of N athletes, find their relative ranks and the people with the top three highest scores, who will be awarded medals: "Gold Medal", "Silver Medal" and "Bronze Medal".

Example 1:
```
Input: [5, 4, 3, 2, 1]
Output: ["Gold Medal", "Silver Medal", "Bronze Medal", "4", "5"]
Explanation: The first three athletes got the top three highest scores, so they got "Gold Medal", "Silver Medal" and "Bronze Medal". 
For the left two athletes, you just need to output their relative ranks according to their scores.
```
Note:  
N is a positive integer and won't exceed 10,000.
All the scores of athletes are guaranteed to be unique.

### 解题思路
这道题可以用优先队列，但是我用的是熟悉的数组。用Map记录它们的排序，然后再次遍历参数nums的时候把它们排序加入到需要返回的数组即可。
#### Scala
```scala
object Solution {
    def findRelativeRanks(nums: Array[Int]): Array[String] = {
        var numSorted = nums.sorted
        var leng = numSorted.length
        var record:Map[Int,String] = Map()
        var count = -1
        for(i <- 0 until leng){
            count += 1
            if(count == leng-1){
                record += (numSorted(i) -> "Gold Medal")
            }else if(count ==leng-2){
                record += (numSorted(i) -> "Silver Medal")
            }else if(count == leng-3){
                record += (numSorted(i) -> "Bronze Medal")
            }else{
                record += (numSorted(i) -> (leng-i).toString)
            }
        }
        var res:Array[String] = Array()
        for(i <- 0 until leng){
            var temp = record.getOrElse(nums(i),"NONE")
            res = res :+ temp
        }
        res
    }
}
```